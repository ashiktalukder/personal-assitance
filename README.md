# personal-assitance
it's a python language AI concept for a PA
import speech_recognition as sr
import pyttsx3
import datetime
import pywhatkit
import wikipedia
import pyjokes

listener = sr.Recognizer()
mama = pyttsx3.init()

voices = mama.getProperty('voices')
mama.setProperty('voice',voices[2].id)
def talk(text):
    mama.say(text)
    mama.runAndWait()

def take_command():
    try:
        with sr.Microphone() as source:
            print('Lisening....')
            voice = listener.listen(source)
            command= listener.recognize_google(voice)
            print(command)
            command = command.lower()
            if 'mama' in command:
                print(command)
                command = command.replace('mama','')


    except:
        talk('again try ok')

    return  command


def run_mama():
    command = take_command()
    if 'time' in command:
        time= datetime.datetime.now().strftime('%I:%M')
        print(time)
        talk('Current time is' + time)
    elif 'play' in command:
        song = command.replace('play','')
        talk('playing..'+ song)
        pywhatkit.playonyt(song)
    elif 'about' in command:
        look_for= command.replace('tell me about','')
        info = wikipedia.summary(look_for,1)
        talk('acoroding to wiki' + info)
    elif 'joke' in command:
        talk(pyjokes.get_joke())
    else:
        talk('i do not get it but i can search for you wait a few minit ')
        pywhatkit.search(command)

while True:
    run_mama()
