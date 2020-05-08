# assitent
#a bit of like jarvis in iron man movie,
import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser
import os
import random
import smtplib
import pyautogui
import cv2
engine = pyttsx3.init("sapi5")
voices = engine.getProperty("voices")
engine.setProperty("voices",voices[0].id)

def speak(audio):
    engine.say(audio)
    engine.runAndWait()
def wishme():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("good morning sir")
    elif hour>=12 and hour<18:
        speak("good afternoon sir")
    else:
        speak("good evening sir")
    speak("i am jarvis. tell me what can i do for you")
def takeCommand():
# It takes microphone input from the user and returns string output

    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        r.energy_threshold = 300
        audio = r.listen(source)
    try:
        print("Recognizing..")
        query =r.recognize_google(audio,language="en-in")
        print(f'you said: {query}\n')
    except Exception as e:
        # print(e)
        print("Say that again please...")
        return "None"
    return query



if __name__ == '__main__':
    # speak("hello Mr. Adhikar Rastogi, i am your servant. tell me what can i do for you")
    wishme()
    while True:
        query = takeCommand().lower()
        # Logic for executing tasks based on query
        if 'wikipedia' in query:
            query = query.replace('wikipedia',"")
            results = wikipedia.summary(query,sentences = 2)
            speak("According to Wikipedia")
            print(results)
            speak(results)
        elif 'open youtube' in query:
            webbrowser.open('youtube.com')
        elif 'open facebook' in query:
            webbrowser.open('facebook.com')
        elif 'open google' in query:
            webbrowser.open('google.com')
        elif 'open stackoverflow' in query:
            webbrowser.open('stackoverflow.com')
        elif 'calculator' in query:
            webbrowser.open("x.com")


        elif 'play music' in query:
            music_dir = "F:\\audios\\english"
            songs = os.listdir(music_dir)
            print(songs)
            os.startfile(os.path.join(music_dir,songs[random.randint(0,7)]))

        elif 'time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"sir, the time is {strTime}")
        elif "jump"  in query: # i wrote this line to play chrome dino game.
            pyautogui.press('up')

        elif 'email' in query:
            speak("sir tell me the sender mail address")
            sender_mail = input(takeCommand().lower())
            speak("sir now told me whom you want to send  i mean The receivers_mail"
                  "address")
            receivers_mail = input(takeCommand().lower())
            speak("sir tell the message ")
            message = input(takeCommand().lower())
            try:
                speak("sir i want you to type your password by your own")

                password=input("enter the password")
                smtpObj = smtplib.SMTP('gmail.com',587)
                smtpObj.sendmail(sender_mail,receivers_mail,message)
                speak("ho gaya kaam ")
            except Exception:
                speak("sorry sir i could not send this email by my own,"
                      "i need your help adhikar sir")





