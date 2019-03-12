---
layout: post
title: Alzheimer's Context Clock - Roadmap and Brainstorming
redirect_from:
  - /blog/posts/alzheimers-context-clock-roadmap-and-brainstorming/
---

This project is one I've been toying with for a long while. It's appeal contains a rare combination of programming, device/hardware, physical construction and sentimental aspects.

A little background: my grandmother is somewhere in the early-mid stages of Alzheimer's. For the most part, she remembers people and places when she sees them but definitely has a hard time drawing connections in the abstract. For example, if I'm in front of her she usually recognizes me (although it may take a bit), but if I'm not in the room "Jason" doesn't always register. Like others in her condition, it's not constant and some days are better than others.

She has always been an important part of my life and has been deeply involved for my entire life from childhood on into adulthood. It makes it all the more frustrating to watch her deteriorate and feel like you can't do anything about it. Of course I'm a maker so my initial reaction is to build a solution.

## First Attempt

A few years ago I wanted to build something that would assist her condition, preferably both entertaining and helping to reinforce connections in her brain. My idea was to make a website for family members to post photos and events (essentially a private family social network), which she could view on a stripped-down tablet customized for only viewing this website.
In hindsight, my heart might have been in the right place but I ignored virtually everything I've learned when it comes to design, user experience and adoption. There was no content because it required effort on behalf of people who never really "bought in". I tried integrating with Facebook but that opened up all sorts of problems in itself. On the other side, the tablet was still harder for her to use than I expected. Most of the time she would just forget it existed, and I didn't consider that even "simple" controls like touch (or a stylus) still aren't native to someone from her generation--and that's before even considering Alzheimer's.

## A New Direction

Taking what I learned from my previous failure, I looked heavily at what did and didn't work. Essentially:

**Good**

- Pretty pictures
- Associations (i.e. picture of "Jason" plus text to help connect the dots)

**Bad**

- User input of any kind
- Out of sight, out of mind
- Stale or limited content

While shopping around for gifts for Alzheimer's patients I was largely underwhelmed. One of the products that stood out was a clock that provided special context for the viewer. Instead of just displaying "3:30 pm" you would see "Wednesday afternoon" because afternoon has a much stronger association than the numbers themselves. This feature really clicked with me but I thought the product itself was incredibly expensive for something that really only showed one screen all the time.

It took no time at all to realize I could do something better with a Raspberry Pi, and it was amazing how quickly improvements came to mind. Why not show rotating slides with more than just time of day? What about seasonal or holiday context? Can I connect to it remotely and add slides periodically? It very quickly spiraled into a whole suite of features that acknowledged everyone of my previous mistakes or successes.

Pretty pictures? Check. Associations? Loads of them, in a wide variety User input? None at all, it will run itself Out of sight? Nope, it will look great sitting in a prominent spot. Fresh content? Absolutely.

## Roadmap

I see this project as having 3 main directions:

1. Hardware - the screen and Pi setup
2. Script - the python program that will handle the slideshow, and possible remote interaction
3. Enclosure - the actual case or frame to house the hardware

Hardware was largely a no brainer. A Raspberry Pi is more than capable, has plenty of storage space, low power consumption and the HDMI port opens up many display opportunities. For the display I quickly fell in love with this HDMI 4 Pi 10.1" Display at Adafruit. There are cheaper options but the IPS screen (1280x800) and HDMI input give it the size and clarity that I find critical. It needs to be big enough with a high resolution to be legible, but not so much that it's bulky and would be hard to find a home (i.e. a monitor). Housed properly it can be aesthetically pleasing as well and easy to integrate with the decor.

The enclosure has actually been the greatest challenge in the planning stage. The screen is roughly 6"x9" with some mounting tabs scattered around the edges. Unfortunately that size doesn't correlate to common picture frames, which was my first idea. I wanted something like a shadow box that would have the depth to house the components. After a lot of searching I stumbled across this Adafruit Tutorial where they mention building your own custom frame, which is what I have settled on for now. It will essentially be crown molding with about 2 inches of "box" behind it. I just picked up my materials and will have to post progress on that later.

The script is fun to build so far. Most of my Python experience is with web (Django) projects so I'm learning new things like TKinter and imaging tools. The script will have its own dedicated post(s) but in a nutshell I'm working towards:

- A base `/Images` directory which will contain all the different types of slides

- A dice roll determines the type of slide to show i.e. "Holiday", "Family" or "Seasonal"

- That type will have date range restrictions to determine which _sub-categories_ are "eligible" i.e. only show Christmas slides in December

- Another dice roll picks a random slide from the appropriate folder and shows it in fullscreen mode

- After ~20 seconds: Rinse. Repeat.

With my slide "types" being:
**Holidays** Pretty holiday themed photos with context text

**Seasons** Similar to holidays but covering a larger date range

**Family** Photos of family members with context, i.e. "Jason, your grandson"

**Locations** Important places from her life with text

**Time of Day** As noted before, "Wednesday afternoon"

**Hard Events** Static set of slides like "Your daughter's birthday"

**Scheduled Events** Can change over time i.e. "Your doctor appointment is this afternoon"

**Inspirational Quotes**, biblical slides or other positive affirmations that are eligible year-round

**Wish list / Things to learn**

- Programmatically drawn slides for things like time of day or reminders
- Event driven slides i.e. "It's Wednesday afternoon, you will be getting a haircut soon"
- Remote access for adding slides periodically
- Periodically poll a page on my site for new events to download in JSON format

That's pretty much where I'm at for now. I'll post my progress along the way.
