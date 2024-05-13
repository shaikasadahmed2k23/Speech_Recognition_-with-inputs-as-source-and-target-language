import speech_recognition as sr
import os
from googletrans import LANGUAGES
from tkinter import *
from tkinter import ttk, messagebox
import googletrans
import textblob
from googletrans import Translator
import os
from gtts import gTTS
import speech_recognition as sr
from langdetect import detect

def get_language_code(language_name):
    #print("X")
    for code, name in LANGUAGES.items():
        if name.lower() == language_name.lower():
            print(code)
            return code

def recognize_speech():
    # Initialize recognizer
    recognizer = sr.Recognizer()

    # Initialize microphone
    microphone = sr.Microphone()

    # Adjust the recognizer sensitivity to ambient noise
    recognizer.energy_threshold = 300

    # Adjust the microphone sensitivity to ambient noise
    microphone.energy_threshold = 300

    # Listen to the user's input
    with microphone as source:
        print("Listening...")
        audio = recognizer.listen(source)

    # Use Google's Speech Recognition API to recognize the audio
    try:
        print("Recognizing...")
        text = recognizer.recognize_google(audio)

        # Use Google Translate to detect the language
    
    #    translator = Translator()
     #   lang = translator.detect(text).lang
      #  lang_confidence = translator.detect(text).confidence
       
        #print(f"Detected language: {lang} with confidence {lang_confidence}")
        print(f"Text: {text}")
        return text

    except sr.UnknownValueError:
        print("Could not understand audio")
    except sr.RequestError as e:
        print(f"Could not request results: {e}")

def translate_now(text1, x, y):
    try:
        text_ = text1
        source_lang = get_language_code(x)  # Detect the source language
        target_lang = get_language_code(y) # Target language
        print("Source language:", source_lang)
        print("Target language:", target_lang)

        if text_:
            translator = Translator()
            print("Original Text : ",text_)
            translation = translator.translate(text_, src=source_lang, dest=target_lang)
            print("Translated text : ", translation.text)

    except Exception as e:
        print("Translation failed. Error:", e)
        messagebox.showerror("Error", "Translation failed. Please try again.")

# Example usage
x = input("Enter the language name u are going to speak : ")
y = input("Enter the language name u want the text to be translated : ")
text1 = recognize_speech()
translate_now(text1,x,y)
#wste stuff below
"""
def translate_now(text1,x,y):
    try:
        text_ = text1
        #source_lang = combo1.get()
        target_lang = get_language_code(y)
        source_lang = get_language_code(x)
        print(target_lang)
        if text_:
            translator = Translator(to_lang=target_lang, from_lang=source_lang)
            print (target_lang + source_lang)
            translation = translator.translate(text_)
            #text2.delete(1.0, END)
            print("xx")
            #text2.insert(END, translation)
            #if translation:
             #   tts=gTTS(text=translation, lang=target_lang)
              #  tts.save("output.mp3")
               # # Play the saved audio file
                #os.system("start output.mp3")
           # else:
            #    print("Nothing to speak.")

            #
            #print(text2)
            print(translation)
            print(text_)
            #print
    except Exception as e:
        print("Translation failed. Error:", e)
        messagebox.showerror("Error", "Translation failed. Please try again.")

import speech_recognition as sr
from googletrans import Translator
"""

