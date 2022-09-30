# Perfect-Pour-Bar
Do you want to modernize your home bar experience while still maintaining that bar style feel? Here is a versatile project that can be easily modified to meet your own design. The goal of this project is to bring together a raspberry pi, touch screen, diaphragm pumps, and various electrical components to automatically pour six different drinks. Each of the six options can be quickly poured to either 0.5oz, 1oz, 2oz, and a free flow.

This project serves as a great beginners guide to programming graphical user interfaces(GUI) and learning to control mechanical components with digital call outs.

# Setting up the Raspberry Pi 3A+

1. Download Raspberry Pi OS -----> https://www.raspberrypi.com/software/
2. Make sure to have the most resent vesion of Python Downloaded 
3. Install Package installer for Python (pip) -----> https://www.raspberrypi.com/documentation/computers/os.html
4. Download GPIO Zero -----> https://gpiozero.readthedocs.io/en/stable/installing.html
5. Download GUI Zero -----> https://lawsie.github.io/guizero/
6. Run code on Boot (Use method 3 for running startup with GUI) -----> https://www.makeuseof.com/how-to-run-a-raspberry-pi-program-script-at-startup/

# Setting up Touch Screen
To set up the screen follow the following instructions.
(This may change depending on size and manufacturer of touch screen)

In terminal type:

    git clone https://github.com/yoyojacky/52Pi.git
    cd~/52Pi
    chmod +x restool.sh
    ./restool.sh

Follow the steps and select the screen type you have and the correct resolution.

# Run "Perfect Pour Code"

Copy, paste, and run the following code in Thonny: 

Note: The 18 lines with "sleep(xx)" indicate the ammount of time the pumps will run. You will need to calibrate these with your hardware to get the desired pour quantity. For reference I found: 0.5oz = 1.1sec, 1oz = 2.2sec, and 2oz = 4.4sec.

    from guizero import App, Window, PushButton, Text
    from gpiozero import LED, Button
    from time import sleep
    import sys
    import threading

    def open_window():
        window.show()
    def open_window2():
        window2.show()
    def open_window3():
        window3.show()
    def open_window4():
        window4.show()    
    def open_window5():
        window5.show()
    def open_window6():
        window6.show()
   
    def close_window():
        window.hide()
    def close_window2():
        window2.hide()
    def close_window3():
        window3.hide()
    def close_window4():
        window4.hide()
    def close_window5():
        window5.hide()
    def close_window6():
        window6.hide()
   
    #def toggleLED():
    #led.toggle()

    def do_nothing():
        return 0

   
    app = App(title="Smart Bar", height=480, width=800, layout="grid", bg="white")

    text0 = Text(app, text="", grid=[0,0], size=20)
    text1 = Text(app, text="Drink", grid=[4,1], size=23)
    text2 = Text(app, text="Selection", grid=[6,1], size=23)
    text0 = Text(app, text="", grid=[0,2], size=20)

    open_button = PushButton(app, text="Whiskey", command=open_window, grid=[0,3], height=8, width=6)
    open_button.text_size=20
    open_button.bg="brown"
    open_button.text_color="white"
    text0 = Text(app, text="", grid=[1,3], size=20)

    open_button2 = PushButton(app, text="Vodka", command=open_window2, grid=[2,3], height=8, width=6)
    open_button2.text_size=20
    open_button2.bg="green"
    open_button2.text_color="white"
    text0 = Text(app, text="", grid=[3,3], size=20)

    open_button3 = PushButton(app, text="Tequila", command=open_window3, grid=[4,3], height=8, width=6)
    open_button3.text_size=20
    open_button3.bg="orange"
    open_button3.text_color="white"
    text0 = Text(app, text="", grid=[5,3], size=20)

    open_button4 = PushButton(app, text="Rum", command=open_window4, grid=[6,3], height=8, width=6)
    open_button4.text_size=20
    open_button4.bg="blue"
    open_button4.text_color="white"
    text0 = Text(app, text="", grid=[7,3], size=20)

    open_button5 = PushButton(app, text="Gin", command=open_window5, grid=[8,3], height=8, width=6)
    open_button5.text_size=20
    open_button5.bg="red"
    open_button5.text_color="white"
    text0 = Text(app, text="", grid=[9,3], size=20)

    open_button6 = PushButton(app, text="Bourbon", command=open_window6, grid=[10,3], height=8, width=6)
    open_button6.text_size=20
    open_button6.bg="purple"
    open_button6.text_color="white"

    window = Window(app, title = "Amount of Whiskey", height=480, width=800, layout="grid", bg="white")
    window.hide()
    window2 = Window(app, title = "Amount of Vodka", height=480, width=800, layout="grid", bg="white")
    window2.hide()
    window3 = Window(app, title = "Amount of Tequila", height=480, width=800, layout="grid", bg="white")
    window3.hide()
    window4 = Window(app, title = "Amount of Rum", height=480, width=800, layout="grid", bg="white")
    window4.hide()
    window5 = Window(app, title = "Amount of Gin", height=480, width=800, layout="grid", bg="white")
    window5.hide()
    window6 = Window(app, title = "Amount of Bourbon", height=480, width=800, layout="grid", bg="white")
    window6.hide()

    text0 = Text(window, text="", grid=[0,0], size=23)
    text4 = Text(window, text="Quantity", grid=[5,1], size=23)
    text0 = Text(window, text="", grid=[0,2], size=23)
    text0 = Text(window, text="", grid=[0,3], size=23)
    text0 = Text(window, text="", grid=[0,4], size=23)

    led= LED(24)

    def led_flash1():
        led.on()
        sleep(1.1)
        led.off()

    button1 = PushButton(window, command=led_flash1, text="0.5oz", grid=[1,3], height=5, width=8)
    button1.text_size=20
    button1.bg="brown"
    button1.text_color="white"
    text0 = Text(window, text="", grid=[2,3], size=20)

    def led_flash2():
        led.on()
        sleep(2.2)
        led.off()

    button2 = PushButton(window, command=led_flash2, text="1oz", grid=[3,3], height=5, width=8)
    button2.text_size=20
    button2.bg="brown"
    button2.text_color="white"
    text0 = Text(window, text="", grid=[4,3], size=20)

    def led_flash3():
        led.on()
        sleep(4.4)
        led.off()

    button3 = PushButton(window, command=led_flash3, text="2oz", grid=[5,3], height=5, width=8)
    button3.text_size=20
    button3.bg="brown"
    button3.text_color="white"
    text0 = Text(window, text="", grid=[6,3], size=20)

    def toggleLED():
        led.toggle()

    button4 = PushButton(window, command=toggleLED, text="Free Flow", grid=[7,3], height=5, width=8)
    button4.text_size=20
    button4.bg="brown"
    button4.text_color="white"
    text0 = Text(window, text="", grid=[8,3], size=20)


    text0 = Text(window2, text="", grid=[0,0], size=23)
    text4 = Text(window2, text="Quantity", grid=[5,1], size=23)
    text0 = Text(window2, text="", grid=[0,2], size=23)
    text0 = Text(window2, text="", grid=[0,3], size=23)
    text0 = Text(window2, text="", grid=[0,4], size=23)

    led2= LED(23)

    def led_flash5():
        led2.on()
        sleep(1.1)
        led2.off()

    button5 = PushButton(window2, command=led_flash5, text="0.5oz", grid=[1,3], height=5, width=8)
    button5.text_size=20
    button5.bg="green"
    button5.text_color="white"
    text0 = Text(window, text="", grid=[2,3], size=20)

    def led_flash6():
        led2.on()
        sleep(2.2)
        led2.off()

    button6 = PushButton(window2, command=led_flash6, text="1oz", grid=[3,3], height=5, width=8)
    button6.text_size=20
    button6.bg="green"
    button6.text_color="white"
    text0 = Text(window, text="", grid=[4,3], size=20)

    def led_flash7():
        led2.on()
        sleep(4.4)
        led2.off()

    button7 = PushButton(window2, command=led_flash7, text="2oz", grid=[5,3], height=5, width=8)
    button7.text_size=20
    button7.bg="green"
    button7.text_color="white"
    text0 = Text(window, text="", grid=[6,3], size=20)

    def toggleLED8():
        led2.toggle()

    button8 = PushButton(window2, command=toggleLED8, text="Free Flow", grid=[7,3], height=5, width=8)
    button8.text_size=20
    button8.bg="green"
    button8.text_color="white"
    text0 = Text(window, text="", grid=[8,3], size=20)


    text0 = Text(window3, text="", grid=[0,0], size=23)
    text4 = Text(window3, text="Quantity", grid=[5,1], size=23)
    text0 = Text(window3, text="", grid=[0,2], size=23)
    text0 = Text(window3, text="", grid=[0,3], size=23)
    text0 = Text(window3, text="", grid=[0,4], size=23)

    led3= LED(18)

    def led_flash9():
        led3.on()
        sleep(1.1)
        led3.off()

    button9 = PushButton(window3, command=led_flash9, text="0.5oz", grid=[1,3], height=5, width=8)
    button9.text_size=20
    button9.bg="orange"
    button9.text_color="white"
    text0 = Text(window, text="", grid=[2,3], size=20)

    def led_flash10():
        led3.on()
        sleep(2.2)
        led3.off()

    button10 = PushButton(window3, command=led_flash10, text="1oz", grid=[3,3], height=5, width=8)
    button10.text_size=20
    button10.bg="orange"
    button10.text_color="white"
    text0 = Text(window, text="", grid=[4,3], size=20)

    def led_flash11():
        led3.on()
        sleep(4.4)
        led3.off()

    button11 = PushButton(window3, command=led_flash11, text="2oz", grid=[5,3], height=5, width=8)
    button11.text_size=20
    button11.bg="orange"
    button11.text_color="white"
    text0 = Text(window, text="", grid=[6,3], size=20)

    def toggleLED12():
        led3.toggle()

    button12 = PushButton(window3, command=toggleLED12, text="Free Flow", grid=[7,3], height=5, width=8)
    button12.text_size=20
    button12.bg="orange"
    button12.text_color="white"
    text0 = Text(window, text="", grid=[8,3], size=20)


    text0 = Text(window4, text="", grid=[0,0], size=23)
    text4 = Text(window4, text="Quantity", grid=[5,1], size=23)
    text0 = Text(window4, text="", grid=[0,2], size=23)
    text0 = Text(window4, text="", grid=[0,3], size=23)
    text0 = Text(window4, text="", grid=[0,4], size=23)

    led4= LED(25)

    def led_flash13():
        led4.on()
        sleep(1.1)
        led4.off()

    button13 = PushButton(window4, command=led_flash13, text="0.5oz", grid=[1,3], height=5, width=8)
    button13.text_size=20
    button13.bg="blue"
    button13.text_color="white"
    text0 = Text(window, text="", grid=[2,3], size=20)

    def led_flash14():
        led4.on()
        sleep(2.2)
        led4.off()

    button14 = PushButton(window4, command=led_flash14, text="1oz", grid=[3,3], height=5, width=8)
    button14.text_size=20
    button14.bg="blue"
    button14.text_color="white"
    text0 = Text(window, text="", grid=[4,3], size=20)

    def led_flash15():
        led4.on()
        sleep(4.4)
        led4.off()

    button15 = PushButton(window4, command=led_flash15, text="2oz", grid=[5,3], height=5, width=8)
    button15.text_size=20
    button15.bg="blue"
    button15.text_color="white"
    text0 = Text(window, text="", grid=[6,3], size=20)

    def toggleLED16():
        led4.toggle()

    button16 = PushButton(window4, command=toggleLED16, text="Free Flow", grid=[7,3], height=5, width=8)
    button16.text_size=20
    button16.bg="blue"
    button16.text_color="white"
    text0 = Text(window, text="", grid=[8,3], size=20)


    text0 = Text(window5, text="", grid=[0,0], size=23)
    text4 = Text(window5, text="Quantity", grid=[5,1], size=23)
    text0 = Text(window5, text="", grid=[0,2], size=23)
    text0 = Text(window5, text="", grid=[0,3], size=23)
    text0 = Text(window5, text="", grid=[0,4], size=23)

    led5= LED(12)

    def led_flash17():
        led5.on()
        sleep(1.1)
        led5.off()

    button17 = PushButton(window5, command=led_flash17, text="0.5oz", grid=[1,3], height=5, width=8)
    button17.text_size=20
    button17.bg="red"
    button17.text_color="white"
    text0 = Text(window, text="", grid=[2,3], size=20)

    def led_flash18():
        led5.on()
        sleep(2.2)
        led5.off()

    button18 = PushButton(window5, command=led_flash18, text="1oz", grid=[3,3], height=5, width=8)
    button18.text_size=20
    button18.bg="red"
    button18.text_color="white"
    text0 = Text(window, text="", grid=[4,3], size=20)

    def led_flash19():
        led5.on()
        sleep(4.4)
        led5.off()

    button19 = PushButton(window5, command=led_flash19, text="2oz", grid=[5,3], height=5, width=8)
    button19.text_size=20
    button19.bg="red"
    button19.text_color="white"
    text0 = Text(window, text="", grid=[6,3], size=20)

    def toggleLED20():
        led5.toggle()

    button20 = PushButton(window5, command=toggleLED20, text="Free Flow", grid=[7,3], height=5, width=8)
    button20.text_size=20
    button20.bg="red"
    button20.text_color="white"
    text0 = Text(window, text="", grid=[8,3], size=20)


    text0 = Text(window6, text="", grid=[0,0], size=23)
    text4 = Text(window6, text="Quantity", grid=[5,1], size=23)
    text0 = Text(window6, text="", grid=[0,2], size=23)
    text0 = Text(window6, text="", grid=[0,3], size=23)
    text0 = Text(window6, text="", grid=[0,4], size=23)

    led6= LED(16)

    def led_flash21():
        led6.on()
        sleep(1.1)
        led6.off()

    button21 = PushButton(window6, command=led_flash21, text="0.5oz", grid=[1,3], height=5, width=8)
    button21.text_size=20
    button21.bg="purple"
    button21.text_color="white"
    text0 = Text(window, text="", grid=[2,3], size=20)

    def led_flash22():
        led6.on()
        sleep(2.2)
        led6.off()

    button22 = PushButton(window6, command=led_flash22, text="1oz", grid=[3,3], height=5, width=8)
    button22.text_size=20
    button22.bg="purple"
    button22.text_color="white"
    text0 = Text(window, text="", grid=[4,3], size=20)

    def led_flash23():
        led6.on()
        sleep(4.4)
        led6.off()

    button23 = PushButton(window6, command=led_flash23, text="2oz", grid=[5,3], height=5, width=8)
    button23.text_size=20
    button23.bg="purple"
    button23.text_color="white"
    text0 = Text(window, text="", grid=[6,3], size=20)

    def toggleLED24():
        led6.toggle()

    button24 = PushButton(window6, command=toggleLED24, text="Free Flow", grid=[7,3], height=5, width=8)
    button24.text_size=20
    button24.bg="purple"
    button24.text_color="white"
    text0 = Text(window, text="", grid=[8,3], size=20)

    close_button = PushButton(window, text="Close", command=close_window, grid=[9,5], height= 1, width=5)
    close_button.text_size=20
    close_button.bg="black"
    close_button.text_color="white"
    text0 = Text(app, text="", grid=[1,3], size=20)

    close_button = PushButton(window2, text="Close", command=close_window2, grid=[9,5], height=1, width=5)
    close_button.text_size=20
    close_button.bg="black"
    close_button.text_color="white"
    text0 = Text(app, text="", grid=[1,3], size=20)

    close_button = PushButton(window3, text="Close", command=close_window3, grid=[9,5], height=1, width=5)
    close_button.text_size=20
    close_button.bg="black"
    close_button.text_color="white"
    text0 = Text(app, text="", grid=[1,3], size=20)

    close_button = PushButton(window4, text="Close", command=close_window4, grid=[9,5])
    close_button.text_size=20
    close_button.bg="black"
    close_button.text_color="white"
    text0 = Text(app, text="", grid=[1,3], size=20)

    close_button = PushButton(window5, text="Close", command=close_window5, grid=[9,5])
    close_button.text_size=20
    close_button.bg="black"
    close_button.text_color="white"
    text0 = Text(app, text="", grid=[1,3], size=20)

    close_button = PushButton(window6, text="Close", command=close_window6, grid=[9,5])
    close_button.text_size=20
    close_button.bg="black"
    close_button.text_color="white"
    text0 = Text(app, text="", grid=[1,3], size=20)

    app.display()
