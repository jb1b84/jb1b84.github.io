---
layout: post
title: Arduino BBQ Sensor - Code
redirect_from:
  - /blog/posts/arduino-bbq-sensor-code/
---

After several briskets and pork butts I think that I have the Arduino BBQ Sensor running smoothly. It is mostly a hybrid of the [Wifi Web Client Repeating](https://www.arduino.cc/en/Tutorial/WiFiWebClientRepeating) script and [Adafruit's MAX31855 Tutorial](https://learn.adafruit.com/thermocouple/using-a-thermocouple).

The Arduino code really only needs to do two things:

1. Fetch the temperature from the K-type thermocouple

2. Send a GET request to a web page, passing in the temperature in the URL parameters

There are some complexities with translating the thermocouple readings into usable temperatures but the provided library handles all of that. If you want to download or fork this into your own project most of your efforts will go into setting up a web page to handle these requests and store the data. I did this originally with PHP and later on ported it to Python+Django. The process is largely the same either way--grab the temperature from a URL parameter and save it to the database of your choosing along with a timestamp.

To prepare for your own use you will need to change:

- Line 21 - enter your Wifi network name

- Line 22 - enter your network password

- Line 36 - (optional) adjust the posting interval to suit your needs, in milliseconds. Defaults to 1 request every 30 seconds

- Lines 31, 127 and 128 - adjust to match your domain and the path to your web page that will capture the temperature logs

{% gist a55d261b2583210ebc5c %}
