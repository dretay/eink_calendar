## Eink display powered by Office365 screen scraping ##

### Overview ###
At work folks frequently want to know where I'm at (since I'm so rarely at my desk). I'd been looking for an excuse to hack around with EINK displays (think Amazon Kindle), and so I had the idea to build a desktop calendar powered. The overall project ended up being broken down into three separate projects as listed below:

- [waveshare_7.5_epaper](https://github.com/dretay/waveshare_7.5_epaper): 
-- I decided to base the graphical rendering on top of [uGFX](https://ugfx.io/). Unfortunatly this library did not have any kind of built-in support for the display panel I was using. Thus the first task was to write a driver for this board based on its [datasheet](https://www.waveshare.com/wiki/7.5inch_e-Paper_HAT). 
- [stm32f4_eink](https://github.com/dretay/stm32f4_eink): once the driver was built I then needed to build a microcontroller-based project to actually leverage the driver and render the display. Based on the memory requirements to render 4-bit greyscale at 640x384, I decided to base the project on an STM32F407VG processor. This project consumes protocolbuffer-encoded messages sent to it and renders the corresponding data onto the display. 
- [stm32f4_eink_sender](https://github.com/dretay/stm32f4_eink_sender): Finally I needed the ability to collect O365 data and send it to the display. Office recently deprecated its BASIC Auth APIs and requires that you use an OATH-based system that has to be approved by your IT administrator. Rather than dealing with that I wrote some python code based on selenium.webdriver and running on a rasperry pi to connect once a day to O365 and screen-scrape the page. 


### Main Features ###
![](https://raw.githubusercontent.com/dretay/eink_calendar/master/IMG_4445.jpg)
- 
