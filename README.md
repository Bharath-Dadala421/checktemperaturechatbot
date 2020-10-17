# checktemperaturechatbot
import requests,json
def greet():
    #greet
    try:
        return str(input("Hey there, this is temperature reporter. May I know your name?"))
    except:
        print("Only characters")
def welcome(name):
    #greet with name
    greets='''Wanna check what time is it in other countries or Wanna know what is the weather condition in our India???'''
    print("Hey ",name,greets," Just follow me ...")
def show_menu():
    print("1. To know the temperature of different states in India ")
    print("2. To know the time of different countries ")        
    print("3. End this chat")
    try:
        return int(input("Enter your choice : "))
    except:
        print("Only numbers in [1-3]")
        return 0
def question(ques):
    if ques=="what can you do " or ques=="what will you do":
        show_menu()
    else:
        print("ask question")
def weather_in_place(CITY):
    BASE_URL = "https://api.openweathermap.org/data/2.5/weather?"
    # City Name CITY = "Hyderabad"
    # API key API_KEY = "Your API Key"
    # upadting the URL
    URL = BASE_URL + "q=" + CITY + "&appid=" + "1d0fdde520d4cb39c12c77e46601fcdd"
    # HTTP request
    response = requests.get(URL)
    # checking the status code of the request
    if response.status_code == 200:
        data = response.json()
        # getting the main dict block
        main = data['main']
        # getting temperature
        temperature = main['temp']
        report = data['weather']
        print(f"Temperature: {temperature}")
    else:
        print("The city is not found.Please enter correct name")
def chatbot():
    name=greet()
    welcome(name)
    q=input()
    question(q)
    option=show_menu()
    place=input("Enter place")
    while option!=3:
        if option==1:
            print("Time")
        elif option==2:
            weather_in_place(place)
            break
chatbot()
