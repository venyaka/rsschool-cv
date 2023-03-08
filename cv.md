# Veniamin Ilkov
## My contacts:

__Mobile-Phone:__ +7 771 535 3963

__e-mail:__ [elannushka912@gmail.com](mailto:elannushka912@gmail.com)

## About Me
I have been programming for several years, I have a little experience of teamwork on a common project and also twice won a prize in a programming hackathon from the Step Academy.
I'm learning fast.

## Skills:
* HTML/CSS
* Javascript
* C/C++ for microcontrollers
* С# for Unity
* Python

## Code examples:
A small program with which you can start the timer on the desktop image of the computer, for this you need to hold down the Ctrl + alt keys, then the timer time and enter:
```python
import ctypes
import os
from PIL import Image, ImageDraw, ImageFont
import keyboard
import time
from screeninfo import get_monitors
from wallpaperInfo import Wallpaper


class mainTimer():
    imagePath = 'images/wallpaper2.png'
    fontSize = 80                                                   # размер текста на экране
    textFont = ImageFont.truetype("arial.ttf", fontSize)
    fontName = "Montserrat-Black"

    def start(textFont, fontSize, fontName):                        # создает папки images и font при их отсутствии перед выполнением программы
        print('start')
        if (os.path.exists('images') == False):
            print('create folder image')
            os.mkdir("images")

        if (os.path.exists('fonts') == False):
            os.mkdir("fonts")
            print('create folder fonts')

        if (os.path.isfile('fonts/' + fontName + '.ttf')):
            mainTimer.textFont = ImageFont.truetype('fonts/' + fontName + '.ttf', fontSize)

        Wallpaper.copy("images/", "wallpaper.png")                  # копирует изображение рабочего стола c названием "wallpaper.jpg" в папку проекта

    def getTime():                                                  # возвращает числа записанные после нажатия залипания клавиш "Ctrl + alt" 
        keys = keyboard.record(until='enter')
        print(keys)
        firstKey = ""
        secondKey = ""

        for i in range(0, len(keys) - 1, 1):
            if keys[i].event_type == "down" and keys[i].name.isdigit():
                firstKey = keys[i].name
                break
        for i in range(len(keys) - 1, 0, -1):
            if keys[i].event_type == "down" and keys[i].name.isdigit():
                secondKey = keys[i].name
                break
        if ((str(firstKey) + str(secondKey)).isdigit()):
            return str(firstKey) + str(secondKey)
        return '0'


def main():
    # параметры экрана:
    backgroundWidth = get_monitors()[0].width
    backgroundHeight = get_monitors()[0].height
    
    white = (255, 255, 255)
    imagePath = mainTimer.imagePath

    mainTimer.start(mainTimer.textFont, mainTimer.fontSize, mainTimer.fontName)

    setTimer = True

    while setTimer:
        if keyboard.is_pressed("ctrl + alt"):
            timerTime = mainTimer.getTime()
            
            stopTimer = False
            timerMin = int(timerTime)
            Time = 0
            step = 0.1

            image = Image.open('images/wallpaper.png')
            image = image.convert(mode='RGBA')
            image = image.resize((backgroundWidth, backgroundHeight))

            while stopTimer == False:
                if timerMin >= 0:
                    if time.time() > Time:
                        alphaImage = Image.new(mode = "RGBA", size = (backgroundWidth, backgroundHeight), color = (255, 255, 255, 0))
                        editedImage = ImageDraw.Draw(alphaImage)

                        editedImage.text((backgroundWidth - mainTimer.fontSize * 2, backgroundHeight / 100), str(timerMin), font = mainTimer.textFont, fill = white)
                        alphaImage.save(imagePath)
                        alphaImage = Image.alpha_composite(image, alphaImage)
                        alphaImage.save(imagePath) 

                        ctypes.windll.user32.SystemParametersInfoA(20, 0, os.path.abspath('images/wallpaper2.png').encode(), 0)
                        Time = time.time() + step
                        timerMin = timerMin - 1
                else:
                    stopTimer = True
                    ctypes.windll.user32.SystemParametersInfoA(20, 0, os.path.abspath('images/wallpaper.png').encode(), 0)
                    keyboard.send("win + d")

                if keyboard.is_pressed("ctrl + break"):
                    timerMin = 0
                    stopTimer = True
                    ctypes.windll.user32.SystemParametersInfoA(20, 0, os.path.abspath('images/wallpaper.png').encode(), 0)
                    break
main()
```

## Experience:
* telegram bot for playing the game "words", and communicating with him.
* Arduino projects:
  * remote control of the computer via the remote control (mouse, keyboard, media) via a microcontroller connected via Usb
  * modification of lighting in the apartment for remote control
* A program that changes slides for another program

## English
I am studying English at Karaganda Technical University. My current level is A2 (Pre-Intermediate).
