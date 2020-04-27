import sys
from tkinter import *
import tkinter.font
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BOARD)
GPIO.setup(11,GPIO.OUT)
GPIO.output(11,0)
Alphabet = {'A': '.-','B': '-...','C': '-.-.','D': '-..','E': '.','F': '..-.','G': '--.','H': '....','I': '..','J': '.---','K': '-.-','L': '.-..','M': '--','N': '-.','O': '---','P': '.--.','Q': '--.-','R': '.-.','S': '...','T': '-','U': '..-','V': '...-','W': '.--','X': '-..-','Y': '-.--','Z': '--..','0': '-----','1': '.----','2': '..---','3': '...--','4': '....-','5': '.....','6': '-....','7': '--...','8': '---..','9': '----.',' ' : '.-.-.-.-.-',' ' : ' '}
def dot():
    GPIO.output(11,1)
    time.sleep(0.3)
    GPIO.output(11,0)
    time.sleep(1)

def dash() :
    GPIO.output(11,1)
    time.sleep(1)
    GPIO.output(11,0)
    time.sleep(1)
    
def space():
    GPIO.output(11,0)
    time.sleep(0.5)
    
def dotranslate():
    textzz = outputtext.get()
    listzz =[]
    counter = 0
    for char in textzz :
        counter += 1
    if counter <= 12 :
        for char in textzz:
            listzz.append(Alphabet[char.upper()])
    else :
        print("Your input is larger than 12 letter, please try again")
        
        
    for unit in listzz :
        print(unit)
        for char in unit :
            if ( char == "." ):
                dot()
            elif (char == "-"):
                dash()
            elif (char == " "):
                space()

win = Tk()
outputtext = StringVar()
win.title("Morse")
myFont = tkinter.font.Font(family = "Helvetica", size = 15, weight = "bold")



def close():
    GPIO.cleanup()

label = Label(win, text = "Enter letter here ( max 12 )").pack()

button = Button(win,font = myFont,text = "ok", command = dotranslate,fg = "black", bg = "white").pack()
entry = Entry(win, textvariable=outputtext).pack()
