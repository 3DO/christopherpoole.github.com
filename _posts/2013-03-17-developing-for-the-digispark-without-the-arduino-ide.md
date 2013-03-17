---
layout: minimal_post
title: Developing for the Digispark without using the Aduino IDE 
published: True
comments: True 
introduction: If you want to compile and upload to your digispark without the Arduino IDE, this is how you do it. 
---

Digisparks run the [micronucleus](https://github.com/Bluebie/micronucleus-t85.git) bootloader.
To upload code to a digispark you will need the micronucleus upload utility:

    git clone https://github.com/Bluebie/micronucleus-t85.git
    cd micronucleus/commandline
    make
    sudo make install

Next, the headers and libraries for using the various onboard devices (Serial and so on) are required.
[DigisparkArduinoIntegration]( https://github.com/digistump/DigisparkArduinoIntegration.git) does the trick, to which I have added a modified Arduino Makefile as well as a no IDE example:

    $> git clone https://github.com/christopherpoole/DigisparkArduinoIntegration.git
    $> DigisparkArduinoIntegration/examples/Digispark_Examples/NoIDEBlink/
    $> make
    $> sudo make dsupload
    micronucleus --run build-cli/main.hex
    > Please plug in the device ... 
    > Press CTRL+C to terminate the program 

The only thing that is different to normal Arduino like development is the inclusion of `main`:

    void setup () {
    }

    void loop() {
    }

    int main(void) {
        init();
        setup();
        for (;;) {
            loop();
        }
    }

At minimum you need this in your Makefile:

    DIGISPARK_DIR = <path to DigisparkArduinoIntegration>

    TARGET                 = main
    #DIGISPARK_LIBS         = <Serial and so one> 
    MCU                    = attiny85
    F_CPU                  = 16000000L

    include $(DIGISPARK_DIR)/Arduino.mk

