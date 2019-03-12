---
layout: post
title: Alzheimer's Clock - The Code
redirect_from:
  - /blog/posts/alzheimers-clock-the-code/
---

I recently added my [Python Slideshow for Raspberry Pi](https://github.com/jb1b84/RasPy-Slideshow) to GitHub, and wanted to walk through a few key points. This is a slightly modified version of the script powering my Dynamic Alzheimer's Clock and if you want the blow-by-blow details of how to get it running for your own use I would recommend checking out the repository page. This post will only be highlighting a few of the key features that make it run.

## File Structure

A core design tenet was to make the slideshow simple to maintain and add/remove new slides. With the folder structure I setup, the script code can find the appropriate folder (i.e. Family) and just pick a random file. I originally experimented some with indexing and a database implementation, but for this project a simple random draw works well thanks to Python's ability to select random files and folders through the `random.choice` method.
My file tree looks something like this:

```
Images/
    Family/
    Holidays/
        Christmas/
        Thanksgiving/
        ...
    Seasons/
        Fall/
        Winter/
        ...
    Inspiration/
```

## Slide Dictionary

A simple Python nested dictionary lays out the mesh for interacting with this folder structure. There are actually two separate dictionaries that handle slides available any day of the year `self.group_static` and slides that are only eligible at certain times `self.group_seasonal`. Each day this second dictionary gets pared down based on date restrictions and then appended to the first to define our eligible slides to randomly draw from.
The dictionary itself is structured as such:

```
{
    'category': CATEGORY_NAME,
    'method': IMAGE_OR_DRAW,
    'slides': {
                    1 : { 'name': SLIDE_NAME, 'path': PATH_TO_FOLDER },
                    ...
                }
}
```

The method can be either `'image'` (simply grabs an image from the path for display) or `'draw'` (programmatically created at runtime).

## Drawn Slides

Some slides will be different every time they come up, such as Time of Day or Weather Context. To support this I added the capability for slides to identify a callback function in their dictionary listing.
For example, the weather slides will call the drawWeather() function, which begins by preparing weather data fetched from a web API. This particular function will pull a random image from the folder system based on whether it is rainy, sunny, snowing etc. Then it draws the temperature on the screen for a final touch.
