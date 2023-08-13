import pyttsx3 
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
#print(voices[0].id)
engine.setProperty('voice',voices[0].id)
def speak(audio):
    engine.say(audio)
    engine.runAndWait()
def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour >= 0 and hour < 12:
        speak("Good Morning")

    elif hour>= 12 and hour < 18:
        speak("Good afternoon!")

    else:
        speak("Good evening!")

def takeCommand():
    # it takes microphone from the user and returns string output

    r = sr.Recognizer()
    with sr.Microphone() as source :
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)
        print("Recognizing...")
        query = r.recognize_google(audio , language = 'en-in')
        print(f"User said:{query}\n")

       # print("Say that again please...")
        return query

if __name__ == "__main__":
    wishMe()
speak("Hello Mam i am norby your AI voice assistant . Please tell me how may i help you ?")
while True:
        query = takeCommand().lower()

        if 'wikipedia' in query:
            print('Will you search in wikipedia')
            speak("Searching wikipedia...")
            query = query.replace("wikipedia","")
            results = wikipedia.summary(query, sentences = 2)
            speak("According to wikipedia")
            print("Results")
            speak(results)
        elif 'open youtube' in query:
            webbrowser.open("youtube.com")
        elif 'open google' in query:
            webbrowser.open("google.com")
        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f" Mam, the time is{strTime}")
        elif 'open code' in query:
            cp1 = "C:\\Users\\jessi\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(cp1)
        elif 'open microsoft word' in query:
            cp2 = "C:\\Program Files\\Microsoft Office\\root\\Office16\\WINWORD.EXE"
            os.startfile(cp2)
        elif 'open microsoft edge' in query:
            cp3 = "C:\\Program Files (x86)\\Microsoft\\Edge\\Application\\msedge.exe"
            os.startfile(cp3)
        elif 'quit' in query:
            speak("Thanks for using me mam...")
            SystemExit()
