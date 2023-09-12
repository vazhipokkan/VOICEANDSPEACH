# VOICEANDSPEACH
This is a code in python to convert voice to speech and speech to voice.

#This will recorgnise the speech and text will be printed in English

import speech_recognition as sr

def translate():
    r = sr.Recognizer()
    with sr.Microphone() as source:

        print('Listening')
        r.pause_threshold = 0.7
        audio = r.listen(source)
        try:
            print("Recognizing")
            Query = r.recognize_google(audio, language='en-In')

            # for listening the command in indian english
            print("the query is printed='", Query, "'")


        except Exception as e:
            print(e)
            print("Say that again sir")
            return "None"
        return Query


# call the function
translate()



#This will convert the speech and convert write it in text and text will convert into speech with a GUI (Tkinter)

from tkinter import *
from tkinter.messagebox import showinfo
from gtts import gTTS
import speech_recognition as sr
import os
mainwindow= Tk()
mainwindow.title('Text-To-Speech and Speech-To-Text Converter')
mainwindow.geometry('500x500')
mainwindow.resizable(0, 0)
mainwindow.configure(bg='yellow')


def say(text1):
    language = 'en'
    speech = gTTS(text=text1, lang=language, slow=False)
    speech.save("text.mp3")
    os.system("start text.mp3")


def recordvoice():
    while True:
        r = sr.Recognizer()
        with sr.Microphone() as source:
            audio = r.listen(source)
            try:
                text1 = r.recognize_google(audio, language="en-IN") #or "Ml-IN"
            except:
                pass
            return text1


def TextToSpeech():
    texttospeechwindow = Toplevel(mainwindow)
    texttospeechwindow.title('Text-to-Speech Converter')
    texttospeechwindow.geometry("500x500")
    texttospeechwindow.configure(bg='Blue')

    Label(texttospeechwindow, text='Text-to-Speech Converter by DataFlair', font=("Times New Roman", 15),
          bg='Blue').place(x=50)

    text = Text(texttospeechwindow, height=5, width=30, font=12)
    text.place(x=7, y=60)

    speakbutton = Button(texttospeechwindow, text='listen', bg='coral', command=lambda: say(str(text.get(1.0, END))))
    speakbutton.place(x=140, y=200)


def SpeechToText():
    speechtotextwindow = Toplevel(mainwindow)
    speechtotextwindow.title('Speech-to-Text Converter')
    speechtotextwindow.geometry("500x500")
    speechtotextwindow.configure(bg='pink')

    Label(speechtotextwindow, text='Speech-to-Text Converter ', font=("Comic Sans MS", 15),
          bg='IndianRed').place(x=50)

    text = Text(speechtotextwindow, font=12, height=3, width=30)
    text.place(x=7, y=100)

    recordbutton = Button(speechtotextwindow, text='Record', bg='Sienna',
                          command=lambda: text.insert(END, recordvoice()))
    recordbutton.place(x=140, y=50)


Label(mainwindow, text='Text-To-Speech and Speech-To-Text Converter',
      font=('Times New Roman', 16), bg='red', wrap=True, wraplength=450).place(x=25, y=0)

texttospeechbutton = Button(mainwindow, text='Text-To-Speech Conversion', font=('Times New Roman', 16), bg='Purple',
                            command=TextToSpeech)
texttospeechbutton.place(x=100, y=150)

speechtotextbutton = Button(mainwindow, text='Speech-To-Text Conversion', font=('Times New Roman', 16), bg='Purple',
                            command=SpeechToText)
speechtotextbutton.place(x=100, y=250)

mainwindow.update()
mainwindow.mainloop()

