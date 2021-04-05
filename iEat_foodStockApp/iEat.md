# iEat

``iEat`` -- a food stock app


## Criteria A: Planning
- ### Context of the problem
My client Isabel wants to have an app which includes a database to help her better organize her food stock. She used to record on an online note but she seldom 
updated due to the usability of the online note and things were not recorded in neat. Therefore, by using this app, she wants to get a clear overview of
what food she has and the expired date of the food as well as keep track on the calories she intakes for every meal. The following is one of the conversations we 
had.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/evidence.png" width = "600" height = "500" >

Fig 0. Interview evidence


- ### Justification of the problem
To solve the problem, I am going to use python and its kivy library and SQL Alchemy to create a program to fulfill the following functionalities:
 1) a login/register system for validating the user and protecting the privacy of the user;
 2) an activity that allows the user to add items into the food stock;
 3) a table shown in the app UI recording items, calories and the expired date.

The reason why I choose python and kivy is because firstly, I had experience with python before so it will be more comfortable for me to develop with the language 
I am more familiar with and it will take less time for the user to wait. The second reason is that kivy supports cross platform operation so even if my client 
changes to another OS system, the program will still work hopefully. Another reason is because of the popularity of python usage and for any further updates of the 
app, learning resources can be easily found and instructors who know Python will be more available.


## Criteria B: Design

- ### Sketch
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/sketch.jpeg" width = "600" height = "500" >

Fig 1. sketch for GUI

- ### System Flow Diagram
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_systemFlow.png" width = "800" height = "360">

Fig 2. System Flow Diagram 

- ### UML Diagram
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_UML.png" width = "650" height = "350">

Fig 3. UML Diagram

- ### ER Diagram
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_ERdiagram.png" width = "900" height = "350">

Fig 4. ER Diagram for the system ( One to one relationship between the user and the food storage database)

- ### Normalised Tables
**Table 1: User**
| id |  username |       email      | password |
|:--:|:---------:|:----------------:|:--------:|
|  1 |    test   |  test@gmail.com  |   test   |
|  2 |   monkey  | monkey@gmail.com | mmmmmm:) |
|  3 | is_a_bear |  isabear@isak.jp | bearbear |

**Table 2: User and food storage**
| id | user_id |       item      | calorie(kcal) | expired date |
|:--:|:-------:|:---------------:|:-------------:|--------------|
|  1 |    1    |     1 banana    |      105      | 2021.4.2     |
|  2 |    1    |     1 apple     |       95      | 2021.4.10    |
|  3 |    1    | soy milk(100ml) |       54      | 2021.5.25    |


## Criteria C: Development


The following is the code for the program.

- ###  .kv


The following is for creating the screens included in the app. The app includes a login screen, a register screen, a home screen, a storage screen and an add-item 
screen.
```
ScreenManager:
    id: scr_manager

    LoginScreen:
        name:"LoginScreen"

    RegisterScreen:
        name:"RegisterScreen"

    HomeScreen:
        name:"HomeScreen"

    StoreScreen:
        name:"StoreScreen"

    AddScreen:
        name:"AddScreen"

```
The following is for the UI for the login screen. The login screen should allow the user to type in personal information to log in. Also, there is a button `Register Here` to guide the user to the register if the user hasn't had an account yet. It looks like this:
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/login.png" width = "720" height = "560">

Figure 5. Login Screen

```
<LoginScreen>:
    BoxLayout:
        orientation:'vertical'
        size: root.height,root.width

        FitImage:
            source:'login_regis.jpeg'
# Create the first MDCard in the screen to show the name of the app
    MDCard:
        size_hint:0.2,0.15
        elevation: 30
        pos_hint:{"center_x":.5,"center_y":.7}
        orientation:"vertical"
        # next is to change the background color of the MDCard by using R,G,B,T(ransparency) and it will be commonly used througout the program.
        md_bg_color:[255/255,255/255,255/255,0.4]

        MDLabel:
            text:"iEat"
            font_style:"H3"
            halign:"center"
            theme_text_color: "Custom"
            text_color: 128, 0, 0, 1
 # Create a second MDCard to show the input textfields and buttons for directing other screens 
    MDCard:
        size_hint:0.6,0.586
        elevation: 10
        pos_hint:{"center_x":.505,"center_y":.27}
        orientation:"vertical"
        md_bg_color:[255/255,255/255,255/255,0.4]

        MDBoxLayout:
            id: content
            adaptive_height: True
            orientation:"vertical"
            padding: dp(30)
            spacing: dp(25)

           ## Create textfields for users to input the info
            MDTextField:
                id: username_input
                hint_text:"Username"
                # set up the maximum length for valid input
                max_text_length: 20
                color_mode: "primary"
                # turn on the `helper_text_mode` to show the reason of errors when the user inputs info inproperly
                helper_text:"Invalid username"
                helper_text_mode:"on_error"
                # set up an icon on the very right of the textfield to help visualize what information the user should provide
                icon_right:"account-box"
                # Set up that the textfield is required to fill out.
                required:True

            MDTextField:
                id: email_input
                hint_text:"Email"
                # set up the maximum length for a valid email
                max_text_length: 50
                color_mode:"primary"
                icon_right:"email"
                helper_text:"Invalid email"
                helper_text_mode:"on_error"
                required: True

            MDTextField:
                id: password_input
                hint_text:"Password"
                # set up the maximum length for a valid password 
                max_text_length: 50
                color_mode: "primary"
                icon_right:"lock"
                helper_text:"Invalid password"
                helper_text_mode:"on_error"
                required: True
                password: True
        # Create a horizontal and a vertical BoxLayout to horizontally align the two buttons -- Register Here and Log in        
        MDBoxLayout:
            id: content
            adaptive_height: True
            orientation:"horizontal"
            padding: dp(30)
            spacing: dp(20)
            # button
            MDRaisedButton:
                text:"Log in"
                size: 150,100
                pos_hint:{"center_x":0.8,"bottom":1}
                # connect to the .py, validating the user
                on_release:
                    root.try_login()

            MDBoxLayout:
                id: content
                elevation:10
                adaptive_height: True
                orientation:"vertical"
                padding: dp(30)
                spacing: dp(20)
           # button
            MDRaisedButton:
                text: "Register Here"
                size: 150,100
                pos_hint:{"center_x":0.4,"bottom":1}
                # connect to the .py, starting registration
                on_release:
                    root.parent.current = "RegisterScreen"

```
The following is the UI for the register screen. It's pretty similar to the login screen but the user need to confirm their passwords by typing twice and there is 
a button `submit` for uploading the information to the database. `Back`button is for people who accidentally click `Register Here`to return to the login screen. 
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/register.png" width = "720" height = "560">

Figure 6. Register Screen

```
<RegisterScreen>:
    BoxLayout:
        orientation:'vertical'
        size: root.height,root.width

        FitImage:
            source:'login_regis.jpeg'

    MDCard:
        size_hint:0.2,0.15
        elevation: 30
        pos_hint:{"center_x":.5,"center_y":.7}
        orientation:"vertical"
        md_bg_color:[255/255,255/255,255/255,0.4]

        MDLabel:
            text:"iEat"
            font_style:"H3"
            halign:"center"
            theme_text_color: "Custom"
            text_color: 128, 0, 0, 1
    MDCard:
        size_hint:0.6,0.588
        elevation: 10
        pos_hint:{"center_x":.5,"center_y":.27}
        orientation:"vertical"
        md_bg_color:[255/255,255/255,255/255,0.4]

        MDBoxLayout:
            id: content
            adaptive_height: True
            orientation:"vertical"
            padding: dp(30)
            spacing: dp(14)

           # Create textfields to allow the user to input info 
            MDTextField:
                id: regis_username_input
                hint_text:"Username"
                max_text_length: 20
                color_mode: "primary"
                helper_text:"Invalid username( length should be at least 6.)"
                helper_text_mode:"on_error"
                icon_right:"account-box"
                required:True

            MDTextField:
                id: regis_email_input
                hint_text:"Email"
                max_text_length: 50
                color_mode:"primary"
                icon_right:"email"
                helper_text:"Invalid email( length should be at least 6 with @)"
                helper_text_mode:"on_error"
                required: True

            MDTextField:
                id: regis_password_input
                hint_text:"Password"
                max_text_length: 50
                color_mode: "primary"
                icon_right:"eye"
                helper_text:"Invalid password( length should be at least 6.)"
                helper_text_mode:"on_error"
                required: True
                password: True

            MDTextField:
                id: password_check
                hint_text:"Confirm password"
                max_text_length: 50
                color_mode:"primary"
                icon_right:"eye"
                helper_text:"Invalid password(passwords do not match.)"
                helper_text_mode:"on_error"
                required: True
                password: True

            MDRaisedButton:
                text:"Submit"
                size: 120,80
                # connect to the .py, registering 
                on_release:
                    root.try_register()
                    root.parent.current = "LoginScreen"
                    
    # Create a special layout for the buttons to freely positioned
    FloatLayout:
        MDFillRoundFlatButton:
            text:"Back"
            halign:"center"
            valign:"center"
            text_size: self.size
            size_hint: 0.08,0.08
            pos_hint:{"x":0.055,"top":0.54}
            #set up the background color of the button 
            background_color: 138/255,69/255,19/255,0.4
            # connect to the.py, returning to the login screen 
            on_release:
                root.parent.current = "LoginScreen"
```
The following is the UI for the home screen. It contains two buttons `Go to Your Food Storage` and `Add Food`.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_home.png" width = "720" height = "560">

Figure 7. Home Screen

```
<HomeScreen>:
    BoxLayout:
        orientation: "vertical"
        size: root.height, root.width
        FitImage:
            source:"home.png"
        MDBoxLayout:
            id:content
            adaptive_height:True
            orientation:"horizontal"
            padding:dp(10)
            spacing:dp(20)

        MDBoxLayout:
            id: content
            adaptive_height: True
            orientation:"vertical"
            padding: dp(20)
            spacing: dp(20)


            MDRaisedButton:
                text:"Go to Your Food Storage"
                halign:"center"
                font_style: "H2"
                pos_hint:{"left":.7,"center_y":.5}
                on_release:
                    root.parent.current = "StoreScreen"

        MDBoxLayout:
            id: content
            adaptive_height: True
            orientation:"vertical"
            padding: dp(20)
            spacing: dp(20)

            MDRaisedButton:
                text:"Add Food"
                halign:"center"
                font_style:"H2"
                pos_hint:{"left":.7,"center_y":.5}
                on_release:
                    root.parent.current = "AddScreen"

    FloatLayout:
        MDIconButton:
            icon: "keyboard-backspace"
            theme_text_color: "Custom"
            pos_hint: {"center_x": 0.03, "top": 0.25}
            text_color: app.theme_cls.primary_color
            on_press:
                root.parent.current = "LoginScreen"

```
The following is the UI for the add screen. There are two textfields for users to input and one button for picking the food expired date.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_add.png" width = "720" height = "560">

Figure 8.1 Add Screen

As expected, there is a calendar for date picking.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_calendar.png" width = "720" height = "560">

Figure 8.2 Add Screen - calendar
```
<AddScreen>:
    BoxLayout:
        id:container1
        orientation: "vertical"
        size: root.height, root.width
        FitImage:
            source:"storage.jpeg"

    MDCard:
        size_hint: 0.35, 0.6
        elevation: 0
        padding: dp(30)
        spacing: dp(20)
        pos_hint: {"center_x": 0.5, "top": 0.64}
        orientation: "vertical"
        md_bg_color:[255/255,255/255,255/255,0.55]
 # Create a label first to show the title of the screen 
        MDLabel:
            text:"ADD NEW ITEM"
            text_color: 128, 0, 0, 1
            font_style:"H5"
            pos_hint:{"center_x":0.68,"center_y":0.8}

        MDTextField:
            pos_hint:{"center_x":.5,"center_y":.7}
            id: item_input
            hint_text: "New item"
            icon_right: "bookmark-plus"
            helper_text: "Required to fill out"
            helper_text_mode: "on_error"
            required: True

        MDTextField:
            pos_hint:{"center_x":.5,"center_y":.6}
            id:calorie_input
            hint_text:"Calories"
            icon_right:"fire"
            helper_text:"Required to fill out"
            helper_text_mode:"on_error"
            required: True
       # Create another MDBoxLayout to align the buttons with the textfields above 
        MDBoxLayout:

            orientation:"horizontal"
            spacing:dp(20)

            MDRectangleFlatIconButton:
                icon: 'calendar'
                text: "Select expired date"
                size:dp(58)*3, dp(50)
                pos_hint: {'center_x': .15, 'center_y': .5}
                # connect to the.py, showing the calendar
                on_release:
                    root.show_date_picker()



        MDFillRoundFlatButton:
            text:"   save   "
            pos_hint:{"center_x":0.5,"center_y":0.75}
            #connect to the .py, uploading new item to the database and then back to the homescreen
            on_release:
                root.add_item()
                root.parent.current = "HomeScreen"
                
       MDLabel:
           id: date_picker_label
           size_hint: None, None
           size: dp(48)*3, dp(48)
           pos_hint: {'center_x': .25, 'center_y': .5}




    FloatLayout:
        MDIconButton:
            icon: "keyboard-backspace"
            theme_text_color: "Custom"
            pos_hint: {"center_x": 0.33, "top": 0.7}
            text_color: app.theme_cls.primary_color
            on_press:
                root.parent.current = "HomeScreen"

```
The following is the UI for the store screen. It will display the user's food stock in the form of a table showing the name, calories and expired date of each 
item.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_storage.png" width = "720" height = "560">

Figure 9. Store Screen

```
<StoreScreen>:
    BoxLayout:
        orientation: "vertical"
        size: root.height, root.width
        FitImage:
            source:"storage.jpeg"
        ScrollView:

            MDCard:
                size_hint: 1, 0
                elevation: 0
                pos_hint: {"center_x": 0.5, "top": 1}
                orientation: "vertical"

                MDCard:
                    size_hint: 1, 0.1
                    elevation: 0
                    padding: 30
                    pos_hint: {"center_x": 0.5, "top": 0.8}
                    orientation: "horizontal"

                    MDIconButton:
                        icon: "keyboard-backspace"
                        theme_text_color: "Custom"
                        pos_hint: {"center_x": 0.1, "top": 0.6}
                        text_color: app.theme_cls.primary_color
                        on_press:
                            root.parent.current = "HomeScreen"

                    MDIconButton:
                        icon: "refresh"
                        theme_text_color: "Custom"
                        pos_hint: {"center_x": 0.1, "top": 0.6}
                        text_color: app.theme_cls.primary_color
                        on_press:
                            root.print_data()


                GridLayout:
                    id: container
                    cols: 3
                    padding: 50
                    spacing: 30
                    row_default_height: 60
                    row_force_default: True
                    pos_hint_y: 0

            #        Column 1 item
                    MDLabel:
                        id: col1
                        text: "Item"
                        font_style: "Subtitle1"
                        halign: "center"

            #        Column 2 caloreis
                    MDLabel:
                        id: col2
                        text: "Calories"
                        font_style: "Subtitle1"
                        halign: "center"

            #        Column 3 expired date
                    MDLabel:
                        id: col3
                        text: "Expired Date"
                        font_style: "Subtitle1"
                        halign: "center"

```
- ###  .py

### Preset
The following is to set the window size of the app. Since the app window is not responsive, custom size of the window may ruin the visual experience of using the 
app as the designed layout will be messed up.

```.py
from kivy.config import Config
from kivy.properties import partial, Clock, BooleanProperty

Config.set('graphics', 'resizable', '0')  ##0 being off 1 being on as in true/false
Config.set('graphics', 'width', '900')
Config.set('graphics', 'height', '700')

```
### Modules and libraries
The following is to import modules and different libraries we will be using later. 
```.py
from kivy.lang import Builder
from kivy.uix.behaviors import ButtonBehavior
from kivymd.app import MDApp
from kivymd.uix.label import MDLabel
from kivy.uix.boxlayout import BoxLayout
from kivymd.uix.screen import MDScreen
from kivy.properties import ObjectProperty

from kivy.metrics import dp
from kivy.uix.anchorlayout import AnchorLayout
from kivymd.app import MDApp
from kivymd.uix.picker import MDDatePicker
from kivy.uix.widget import Widget

import sqlite3
from sqlalchemy import Column, String, Integer, ForeignKey, DateTime, desc
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
```
### Database
Create database for users and foodstock.
```.py
Base = declarative_base()

# ORM 
class User(Base):
    __tablename__ = 'User'
    id = Column(Integer, primary_key=True, autoincrement=True)
    username = Column(String(20)) # 20 means the max. length of username is 20 characters.
    email = Column(String(50))
    password = Column(String(50))

    def __init__(self, username, email, password):
        self.username = username
        self.email = email
        self.password = password
        
class Storage(Base):
    __tablename__ = "Storage"
    id = Column(Integer,primary_key = True,autoincrement=True)
    User_id = Column(Integer,ForeignKey('User.id'))
    item_name = Column(String)
    calories = Column(String)
    expired_date = Column(DateTime)

    def __init__(self,User_id,item_name,calories,expired_date):
        self.item_name = item_name
        self.calories = calories
        self.expired_date = expired_date
        self.User_id = User_id

# Connect to SQL 
engine = create_engine('sqlite:///foodstock.sqlite')
session = sessionmaker()
session.configure(bind=engine)
Base.metadata.create_all(engine)

```
### Log in
Create a class for login screen
```.py
class LoginScreen(MDScreen):
    User_id = None
    stored_password = None
```
Then create two functions to validate the users and password before people actually login in. *Note: passwords have been hashed and we will go through this later.
```.py
def verify_password(stored_password, provided_password):
        """Verify a stored password against one provided by user"""
        salt = stored_password[:64]
        stored_password = stored_password[64:]
        pwdhash = hashlib.pbkdf2_hmac('sha256',
                                      provided_password.encode('utf-8'),
                                      salt.encode('ascii'),
                                      100000)
        pwdhash = binascii.hexlify(pwdhash).decode('ascii')
        return pwdhash == stored_password

def validate_user(self):
    self.ids.password_input.error = True
    self.ids.password_input.helper_text = "Incorrect username or password"
    print(self.ids.username_input.error)
    print(self.ids.username_input.helper_text)

```
Create a function for login that include the two functions `validate_user` and `verify_ password`we mentioned before.
```.py
def try_login(self):
        # engine = create_engine('sqlite:///foodstock.sqlite')
        username = self.ids.username_input.text
        email = self.ids.email_input.text
        password = self.ids.password_input.text
        session = sessionmaker(bind=engine)
        s = session()
        validate_user = s.query(User).filter_by(username=username, email=email).one_or_none()
        if validate_user:
            print("User exists")
            LoginScreen.User_id = validate_user.id
            stored_password = s.query(User).get(validate_user.id).password

            if LoginScreen.verify_password(stored_password,password) == True:
                self.parent.current = 'HomeScreen'

        else:
            print("User does not exist")
            self.validate_user()
        s.close()

```
### Buttons 
The following is to create a class for all the buttons we used in kivy.
```.py
class ButtonLabel(ButtonBehavior, MDLabel):
    pass
```
### Register
Create a class for the register screen. When the user inputs the password, the password will be recorded in the database as well as the auto-generated user id, 
inputed username and email address. However, we don't want users' password being recorded directly without encryption; so, we also need to use `hash` and add 
a`salt number` which is a random hashed number to encrypt the password into a constant 512 bits string stored in our database. This can largely help protect the 
privacy of the app users.

Here is what `hash` looks like in the database: 
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_hash_password.png" width = "800" height = "120" >

```.py
class RegisterScreen(MDScreen):

    def hash_password(self):
        password = self.ids.regis_password_input.text
        """Hash a password for storing."""
        #hashing a ramdom sequence with 60 bits: produces 256 bits or 64 hex chars
        salt = hashlib.sha256(os.urandom(60)).hexdigest().encode('ascii')
        
        pwdhash = hashlib.pbkdf2_hmac('sha256', password.encode('utf-8'),
                                      salt, 100000)
        #hashing the password with the salt producing 256 bits or 64 hex chars                              
        pwdhash = binascii.hexlify(pwdhash)
        return (salt + pwdhash).decode('ascii') #total lenght is 128 chars or 512 bits
```

Then create a function for registering. In our register system, we set several rules for our users:
*For user 1, it's for very basic testing and more quickly logging into the app so it won't be applied by the rules following

1. A valid username, email or password should be all at least 6 characters long.
2. The user is required to fill out every textfield shown in the app.
3. The user has to input the password twice to confirm the password.
4. The user cannot register with nothing.
5. The maximum length for each textfield is shown in the app. The characters are counted automatically, so if the length excceeds, the textfield will turn red.
*(Rule 5 can be fullfilled in .kv)*
6. A valid email has to contain "@".
7. The user cannot register again withe the same username.
```.py
def try_register(self):
        newUsername = self.ids.regis_username_input.text
        newEmail = self.ids.regis_email_input.text
        newPassword = self.ids.regis_password_input.text
        Password_check = self.ids.password_check.text
        hash_password = RegisterScreen.hash_password(self)
        
       # Rule 3
       if newPassword == Password_check:  
            s = session()
            #  Rule 7
            user_check = s.query(User).filter_by(username=newUsername, email=newEmail, password=newPassword).first()

            if user_check:
                print("User already exists")
            # Rule 6
            elif "@" not in newEmail:
                self.ids.regis_email_input.error = True
                self.ids.regis_email_input.helper_text = "Invalid email without @"
                print("Invalid email without @")            
            ''' Rule 1,2,4'''
            elif len(newUsername) < 6:
                self.ids.regis_username_input.error = True
                self.ids.regis_username_input.helper_text = "Length is not enough. It should be at least 6."
                print("Length for username is not enough. It should be at least 6.")
            elif len(newEmail) < 6:
                self.ids.regis_email_input.error = True
                self.ids.regis_email_input.helper_text = "Length for email is not enough. It should be at least 6."
                print("Length for email is not enough. It should be at least 6.")
            elif len(newPassword) < 6:
                self.ids.regis_password.error = True
                self.ids.regis_password_input.helper_text = "Password is too short.It should be at least 6."
                print("Length for password is too short. It should be at least 6.")
            else:
                self.ids.regis_email_input.error = False
                self.ids.regis_username_input.error = False
                self.ids.regis_password.error = False
  
                # add new user in the database
                newUsr = User(username=newUsername, email=newEmail,password=hash_password)
                s.add(newUsr)
                print("User created")
                s.commit()
                s.close()
        else:
            RegisterScreen.hash_password(newPassword)
            s = session()
            s.close()
            print("The passwords do not match.")

```
### Home 
```.py
class HomeScreen(MDScreen):
    pass
```
#### Storage 
Create a class for the storage screen. The main element on a storage screen is the tables to show the food our users have. By using loop, the items, calories and expired date will be fetched from the database to be printed out.

```.py
class StoreScreen(MDScreen):
    def print_data(self):

        s = session()

        self.ids.container1.clear_widgets()
        show_date = MDLabel(text="Expired date:",font_style="Subtitle1",halign="center")

        self.ids.container1.add_widget(show_date)
        storage = s.query(Storage).order_by(desc('expired_date')).filter_by(User_id=LoginScreen.User_id).all()
        item = MDLabel(text="Item", font_style="Subtitle1", halign="center")
        self.ids.container1.add_widget(item)
        calories = MDLabel(text="Calories", font_style="Subtitle1", halign="center")
        self.ids.container1.add_widget(calories)
        date = MDLabel(text="Expired Date", font_style="Subtitle1", halign="center")
        self.ids.container1.add_widget(date)

        for i in storage:
            item = MDLabel(text=str(storage.item), halign="center")
            self.ids.container.add_widget(item)
            calories = MDLabel(text=str(storage.calories), halign="center")
            self.ids.container.add_widget(calories)
            date = MDLabel(text=str(storage.expired_date), halign="center")
            self.ids.container.add_widget(date)
            print("print data")

```
Create a class for the add-item screen. The followin is to create a calendar for picking the expired date of the items.
```.py
class AddScreen(MDScreen):
    item_name = None
    calories = None
    select_date = None

    def on_save(self, instance, value, date_range):
        '''
        Events called when the "OK" dialog box button is clicked.

        :type instance: <kivymd.uix.picker.MDDatePicker object>;

        :param value: selected date;
        :type value: <class 'datetime.date'>;

        :param date_range: list of 'datetime.date' objects in the selected range;
        :type date_range: <class 'list'>;
        '''

        print(value)
        AddScreen.select_date = value
        #create value so I can recall in another method

    def on_cancel(self, instance, value):
        '''Events called when the "CANCEL" dialog box button is clicked.'''
        print("cancel")

    def show_date_picker(self):
        date_dialog = MDDatePicker(self)
        date_dialog.bind(on_save=self.on_save, on_cancel=self.on_cancel)
        date_dialog.open()
        #method to create datePicker widget
   
```
Create a function to allow the users to add the items to their own foodstock.
```.py
def add_item(self):
        User_id = LoginScreen.User_id
        item_name = self.ids.item_input.text
        calories = self.ids.calorie_input.text
        expired_date = AddScreen.expired_date

        AddScreen.item_name = item_name
        AddScreen.calories = calories
        AddScreen.expired_date = expired_date


        s = session()
        NewItem = Storage(User_id=User_id,item_name=item_name,calories = calories,expired_date = expired_date)
        s.add(NewItem)
        s.commit()
        s.close()
        print("Successfully add the item!")

```
### Set up the app 
```.py
class MainApp(MDApp):
    def build(self):
    # set up the theme color
        self.theme_cls.primary_palette = 'Brown'
    # set up the icon as Figure 10 shown    
        self.icon = "icon.png"
        return

MainApp().run()
```
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_icon.png" width = "230" height = "300" >

Figure 10. Custom Icon



## Criteria D: Functionality
- ### Success Criteria
| Criteria                                                                                                           | Expected outcome                                                                                                           | Met? |
|--------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|------|
| 1.The app has a login/register system.                                                                             | The user can register and then login the system successfully.                                                              | Met  |
| 2.The app has two databases. One is for users' information and  the other is for food storage.                     | New users and new food items can be added.                                                                                 |  Met    |
| 3.There is a table linked to the food storage database in the  app UI to show the items,calories and expired date. | The user can see the three attributes of saved food item(s) in the storage screen in the form of a table.                  |   Met   |
| 4.There are multiple screens for clear navigation.                                                                 | The user can see a login screen, a register screen, a homescreen, a food storage screen and a add-item screen.             | Met  |
| 5. When adding the items, there is a calendar for the user to pick the date.                                       | The user can use the calendar to pick the date.                                                                            |  Met    |
| 6. The data in the database is not redundant.                                                                      | The user can see "user already exists" when registering by using the same username or email or password as other people's. | Met  |

## Criteria E: Evaluation 
- ### Alpha testing

| Step No. | Step                                                                                                                                                                               | Expected Outcome                                                                                                                                                                                                                                                                                                                       | Success Criteria | Success? |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------|
| 1.       | Click "Register Here" and input the username, email and password. Click "submit".                                                                                                  | After clicking "submit", it will show "User created" in the console. Then the user will be directed to login screen.                                                                                                                                                                                                                   | 1                | Success  |
| 2.       | Type all required information and log in.                                                                                                                                          | Log in successfully and be directed to the home screen.                                                                                                                                                                                                                                                                                | 1                | Success  |
| 3.       | Check the database in pyCharm.                                                                                                                                                     | There are two databases: User and Storage.                                                                                                                                                                                                                                                                                             | 2                | Success  |
| 4.       | Click the "Add Food" button and input information needed. Click"select expired date" to the choose the date by using a calendar. Then click "save" and check the Storage database. | The screen will be directed to the add-item screen showing two textfields for the users to input the item and calories. There will be a calendar popping up to allow the user to pick the date. After clicking "Save", the added item and its info can be seen in the Storage database and the screen will go back to the home screen. | 5                | Success  |
| 5.       | Click "Go to Your Food Storage" and click refresh button to check the food stock.                                                                                                  | The screen will be directed to the storage screen showing a table with the item we just added.                                                                                                                                                                                                                                         | 3                | Success  |
| 6.       | Go back to the login screen and register with the same username or email again. Click "submit".                                                                                    | It will show "User already existed" in the console.                                                                                                                                                                                                                                                                                    | 6                | Success  |
| 7.       | So far, we have multiple screens included in the app.                                                                                                                              | Screens switch among each other.                                                                                                                                                                                                                                                                                                       | 4                | Success  |

- ### Beta testing

- ### Unit testing

- ### App Improvements
- Cloud backup
- Functionalities 
  - allow the user to edit the amount of the food like the picture shows(amazon) and edit the table in general
  <img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_opt_amount.png" width = "330" height = "180" >        <img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_amount.png" width = "300" height = "280" >
  
  - Toast functions to show the error more clearly to the user
  - logo on the desktop when opening the app
  - make it responsive
  - add more functions to the app
  - stregthen the interaction with the user. eg."Welcome xxxx!" 
  - etc.
  - 
- [ ] this is an incomplete item


