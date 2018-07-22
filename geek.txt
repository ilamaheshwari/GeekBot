import speech_recognition as sr
from time import ctime
import os
import re
import time
import webbrowser
import wikipedia
from gtts import gTTS
from selenium import webdriver
import imaplib
import email
import getpass
import urllib2
import json
from bs4 import BeautifulSoup
import urllib
#Password
"""def passwordrecord():
    # Record Audio
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Tell me the password!")
        speak("Tell me the password!")
        audio = r.listen(source)
        
    # Speech recognition using Google Speech Recognition
    password = ""
    try:
        password = r.recognize_google(audio, language='en-US')
        print("You said: " + password)
    except sr.UnknownValueError:
        print("Google Speech Recognition could not understand audio")
    except sr.RequestError as e:
        print("Could not request results from Google Speech Recognition service; {0}".format(e))
    return password
"""

def speak(audioString):
    print(audioString.encode("utf-8"))
    tts = gTTS(text=audioString.encode("utf-8"), lang='en')
    tts.save("audio1.mp3")
    os.system("start audio1.mp3")

    
def recordAudio():
    # Record Audio
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Say something!")
        audio = r.listen(source)
 
# Speech recognition using Google Speech Recognition
    data = ""
    try:
        data = r.recognize_google(audio, language='en-US')
        print("You said: " + data)
    except sr.UnknownValueError:
        print("Google Speech Recognition could not understand audio")
    except sr.RequestError as e:
        print("Could not request results from Google Speech Recognition service; {0}".format(e))
    return data
 
def jarvis(data):
    if "good morning" in data:
        speak("Good Morning sir!")
    # Automatically geolocate the connecting IP
        f = urllib2.urlopen('http://freegeoip.net/json/')
        json_string = f.read()
        f.close()
        location = json.loads(json_string)
        location_city = location['city']
        #print(location_city)
        #location_state = location['region_name']
        #print(location_state)
        location_country = location['country_name']
        #print(location_country)
        data = urllib.urlopen('https://www.timeanddate.com/weather/'+location_country+'/'+location_city)
        soup = BeautifulSoup(data)
        div = soup.find('div',id="qlook")
        div1= soup.find('div',{'class':'h2'}).string
        speak("TEMPERATURE:"+div1)
        time.sleep(3)
        div2= str(div)
        soup1 = BeautifulSoup(div2)
        [s.extract() for s in soup1('span')]
        p = soup1.find_all('p')
        a=[]
        for each in p:
            a.append(each)
        b = str(a[0])
        c = str(a[1])
        x = b.replace('<p>','').replace('</p>','').replace('<br/>','\n')
        y = c.replace('<p>','').replace('</p>','').replace('<br/>',',')
        z = y.decode("utf-8")
        speak(x)
        time.sleep(2)
        speak(z)
        time.sleep(14)
        
    elif "good afternoon" in data:
        speak("Good afternoon sir!")
    # Automatically geolocate the connecting IP
        f = urllib2.urlopen('http://freegeoip.net/json/')
        json_string = f.read()
        f.close()
        location = json.loads(json_string)
        location_city = location['city']
        #print(location_city)
        #location_state = location['region_name']
        #print(location_state)
        location_country = location['country_name']
        #print(location_country)
        data = urllib.urlopen('https://www.timeanddate.com/weather/'+location_country+'/'+location_city)
        soup = BeautifulSoup(data)
        div = soup.find('div',id="qlook")
        div1= soup.find('div',{'class':'h2'}).string
        speak("TEMPERATURE:"+div1)
        time.sleep(3)
        div2= str(div)
        soup1 = BeautifulSoup(div2)
        [s.extract() for s in soup1('span')]
        p = soup1.find_all('p')
        a=[]
        for each in p:
            a.append(each)
        b = str(a[0])
        c = str(a[1])
        x = b.replace('<p>','').replace('</p>','').replace('<br/>','\n')
        y = c.replace('<p>','').replace('</p>','').replace('<br/>',',')
        z = y.decode("utf-8")
        speak(x)
        time.sleep(2)
        speak(z)
        time.sleep(14) 
        
    elif "good evening" in data:
        speak("Good evening sir!")
    # Automatically geolocate the connecting IP
        f = urllib2.urlopen('http://freegeoip.net/json/')
        json_string = f.read()
        f.close()
        location = json.loads(json_string)
        location_city = location['city']
        #print(location_city)
        #location_state = location['region_name']
        #print(location_state)
        location_country = location['country_name']
        #print(location_country)
        data = urllib.urlopen('https://www.timeanddate.com/weather/'+location_country+'/'+location_city)
        soup = BeautifulSoup(data)
        div = soup.find('div',id="qlook")
        div1= soup.find('div',{'class':'h2'}).string
        speak("TEMPERATURE:"+div1)
        time.sleep(3)
        div2= str(div)
        soup1 = BeautifulSoup(div2)
        [s.extract() for s in soup1('span')]
        p = soup1.find_all('p')
        a=[]
        for each in p:
            a.append(each)
        b = str(a[0])
        c = str(a[1])
        x = b.replace('<p>','').replace('</p>','').replace('<br/>','\n')
        y = c.replace('<p>','').replace('</p>','').replace('<br/>',',')
        z = y.decode("utf-8")
        speak(x)
        time.sleep(2)
        speak(z)
        time.sleep(14)
        
        
    elif "hello" in data:
        speak("Hi sir, what can I do for you?")
    elif "how are you" in data:
        speak("I am fine")
    elif "how old are you" in data:
        speak("just born sir ")
    elif "what time is it" in data:
        speak(ctime())
    elif "good bye" in data:
        speak("goodbye sir,have a nice day")  

    # Calculator    
    elif "open calculator" in data:
        speak("calculator is open now!")
        time.sleep(2)
        class cal():
            def __init__(self,a,b):
                self.a=a
                self.b=b
            def add(self):
                return self.a+self.b
            def mul(self):
                return self.a*self.b
            def div(self):
                return float(self.a)/float(self.b)
            def sub(self):
                return self.a-self.b
        choice=1
        while choice!=0:
            print "##############################"
            print("0. Exit")
            print("1. Addition")
            print("2. Subtraction")
            print("3. Multiplication")
            print("4. Division")
            speak("Choose your operation!")
            data = recordAudio()
            if "addition" in data:
                choice = 1
            elif "subtraction" in data:
                choice = 2
            elif "multiplication" in data:
                choice = 3
            elif "division" in data:
                choice = 4
            elif "exit" in data:
                choice = 0
                print("calculator is closed.....")
                speak("Calculator is closed")
                print("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~")
                break
            else:
                print("Invalid choice!!")
                speak("Invalid choice!!")
                time.sleep(2)
                print("calculator is closed.....")
                speak("Calculator is closed")
                print("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~")
                break
            speak("tell me two numbers")
            data = recordAudio()
            list1 = re.findall(r"[-+]?\d*\.\d+|\d+", data)
            a = int(list1[0])
            b = int(list1[1])
            obj=cal(a,b)
            time.sleep(2)
            if choice==1:
                print("Result: ",obj.add())
                speak("Your Result is  "+str(obj.add()))
                time.sleep(5)
            elif choice==2:
                print("Result: ",obj.sub())
                speak("Your Result is  "+str(obj.sub()))
                time.sleep(5)
            elif choice==3:
                print("Result: ",obj.mul())
                speak("Your Result is  "+str(obj.mul()))
                time.sleep(5)
            elif choice==4:
                print("Result: ",(obj.div()))
                speak("Your Result is  "+str((obj.div())))
                time.sleep(5)
            elif choice==0:
                print("Exiting!")
            else:
                print("Invalid choice!!")
                choice = 0
    
    #Search Video
    elif "play video" in data:
        speak("video searching is open now!")
        print("#################################")
        time.sleep(3)
        speak("tell me the video you want to play")
        data = recordAudio()
        time.sleep(5)
        if not data:
            speak("you said nothing.")
        else:
            speak("Wait sir ,I will show you the result")
            driver = webdriver.Firefox()
            driver.get("https://www.youtube.com/results?search_query="+data)
            elem = driver.find_element_by_class_name("yt-uix-tile-link")
            elem.click()
            time.sleep(10)
    
    #Check mail
    elif "check mail" in data:
        username = raw_input("Enter your e-mail address:")
        password = getpass.getpass()
        mail = imaplib.IMAP4_SSL('imap.gmail.com')
        mail.login(username, password)
        mail.list()
        mail.select('inbox')
        typ, dataset = mail.search(None, 'UNSEEN')
        ids = dataset[0]
        id_list = ids.split()
        #get the most recent email id
        latest_email_id = int( id_list[-1] )
        #iterate through 15 messages in decending order starting with latest_email_id
        #the '-1' dictates reverse looping order
        for i in range( latest_email_id, latest_email_id-15, -1 ):
           typ, dataset = mail.fetch( i, '(RFC822)' )
           for response_part in dataset:
               if isinstance(response_part, tuple):
                   msg = email.message_from_string(response_part[1])
                   Subject = msg['subject']
                   From = msg['from']
       #remove the brackets around the sender email address
           From = From.replace('<', '')
           From = From.replace('>', '')
           if "UTF" in Subject:
               speak("you have mail from !   "+From.split()[0])
               print '\n[' + From.split()[-1] + '] ' + Subject +"\n"   
               print "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"
               time.sleep(5)
           elif "utf" in Subject:
               speak("you have mail from !   "+From.split()[0])
               print '\n[' + From.split()[-1] + '] ' + Subject +"\n"   
               print "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"
               time.sleep(5)
           else:
               speak(From.split()[0]+  "  send you a mail having subject !  " +Subject)
               print '\n[' + From.split()[-1] + '] ' + Subject +"\n"   
               print "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"
               time.sleep(12)         
        mail.close()
        mail.logout()
    
    #Search MAP    
    elif "where is" in data:
        data = data.split(" ")
        location =""
        location = location.split(" ")
        for i in range(2,len(data)):
            location.append(data[i])
        str1 = "  ".join(location)
        speak("Hold on sir, I will show you where " + str1 + " is.")
        webbrowser.open("https://www.google.nl/maps/place/" + str1 )
        time.sleep(5)
        
    elif "who is" in data:
        data = data.split(" ")
        name =""
        name = name.split(" ")
        for i in range(2,len(data)):
            name.append(data[i])
        str1 = "  ".join(name)
        speak("Hold on sir, I will show you about " + str1 )
        wiki =  wikipedia.summary(str1, sentences=2)
        str2 = wiki.encode('ascii', 'ignore').decode('ascii')
        speak(str2)
        time.sleep(25)
        webbrowser.open("https://www.google.com/search?q=" +str1)
        time.sleep(5)
    
    elif "what is" in data:
        data = data.split(" ")
        name =""
        name = name.split(" ")
        for i in range(2,len(data)):
            name.append(data[i])
        str1 = "  ".join(name)
        speak("Hold on sir, I will show you about " + str1 )
        wiki =  wikipedia.summary(str1, sentences=2)
        str2 = wiki.encode('ascii', 'ignore').decode('ascii')
        speak(str2)
        time.sleep(25)
        webbrowser.open("https://www.google.com/search?q=" +str1)
        time.sleep(5)
        
    elif not data:
        speak("Sorry sir,I could not understand audio please say again")
        time.sleep(5)
    
    #Searching on Google
    else:
        speak("Wait sir ,I will show you the result")
        webbrowser.open("https://www.google.com/search?q=" +data)
        time.sleep(5)

# initialization
data =""
time.sleep(2)
#password =""
#time.sleep(2)
#password = passwordrecord()
#if "" in password:
print("########...WELCOME...############")
#speak("CORRECT PASSWORD")
while (data!="goodbye"):
    data = recordAudio()
    jarvis(data)
#else:
#    speak("Wrong Password sir!")
#    print ("Wrong password......")