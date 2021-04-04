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
(Need to explain the layouts and different elements, widgets used)

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
The following is for the UI for the login screen. It looks like this:
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/login.png" width = "900" height = "700">

Figure 5. Login Screen

```
<LoginScreen>:
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


            MDTextField:
                id: username_input
                hint_text:"Username"
                max_text_length: 20
                color_mode: "primary"
                helper_text:"Invalid username"
                helper_text_mode:"on_error"
                icon_right:"account-box"
                required:True

            MDTextField:
                id: email_input
                hint_text:"Email"
                max_text_length: 50
                color_mode:"primary"
                icon_right:"email"
                helper_text:"Invalid email"
                helper_text_mode:"on_error"
                required: True

            MDTextField:
                id: password_input
                hint_text:"Password"
                max_text_length: 50
                color_mode: "primary"
                icon_right:"lock"
                helper_text:"Invalid password"
                helper_text_mode:"on_error"
                required: True
                password: True
        MDBoxLayout:
            id: content
            adaptive_height: True
            orientation:"horizontal"
            padding: dp(30)
            spacing: dp(20)

            MDRaisedButton:
                text:"Log in"
                size: 150,100
                pos_hint:{"center_x":0.8,"bottom":1}
                on_release:
                    root.try_login()

            MDBoxLayout:
                id: content
                elevation:10
                adaptive_height: True
                orientation:"vertical"
                padding: dp(30)
                spacing: dp(20)

            MDRaisedButton:
                text: "Register Here"
                size: 150,100
                pos_hint:{"center_x":0.4,"bottom":1}
                on_release:
                    root.parent.current = "RegisterScreen"

```
The following is the UI for the register screen.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/register.png" width = "900" height = "700">

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
                on_release:
                    root.try_register()
                    root.parent.current = "LoginScreen"

    FloatLayout:
        MDFillRoundFlatButton:
            text:"Back"
            halign:"center"
            valign:"center"
            text_size: self.size
            size_hint: 0.08,0.08
            pos_hint:{"x":0.055,"top":0.54}
            background_color: 138/255,69/255,19/255,0.4
            on_release:
                root.parent.current = "LoginScreen"
```
The following is the UI for the home screen.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_home.png" width = "900" height = "700">

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
The following is the UI for the add screen.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_add.png" width = "900" height = "700">

Figure 8.1 Add Screen
As expected, there is a calendar for date picking.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_calendar.png" width = "900" height = "700">

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

        MDBoxLayout:

            orientation:"horizontal"
            spacing:dp(20)

            MDRectangleFlatIconButton:
                icon: 'calendar'
                text: "Select expired date"
                size:dp(58)*3, dp(50)
                pos_hint: {'center_x': .15, 'center_y': .5}
                on_release:
                    root.show_date_picker()



        MDFillRoundFlatButton:
            text:"   save   "
            pos_hint:{"center_x":0.5,"center_y":0.75}
            on_release:
                root.add_item()
                root.parent.current = "HomeScreen"




    FloatLayout:
        MDIconButton:
            icon: "keyboard-backspace"
            theme_text_color: "Custom"
            pos_hint: {"center_x": 0.33, "top": 0.7}
            text_color: app.theme_cls.primary_color
            on_press:
                root.parent.current = "HomeScreen"

```
The following is the UI for the store screen.
<img src = "https://github.com/cathymonkey/Unit_3/blob/main/iEat_foodStockApp/t_storage.png" width = "900" height = "700">
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

            #        Column 1
                    MDLabel:
                        id: col1
                        text: "Item"
                        font_style: "Subtitle1"
                        halign: "center"

            #        Column 2
                    MDLabel:
                        id: col2
                        text: "Calories"
                        font_style: "Subtitle1"
                        halign: "center"

            #        Column 3
                    MDLabel:
                        id: col3
                        text: "Expired Date"
                        font_style: "Subtitle1"
                        halign: "center"

```
- ###  .py

## Criteria D: Functionality
- ### Success Criteria
| Criteria                                                                                                           | Expected outcome                                                                                                           | Met? |
|--------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|------|
| 1.The app has a login/register system.                                                                             | The user can register and then login the system successfully.                                                              | Met  |
| 2.The app has two databases. One is for users' information and  the other is for food storage.                     | New users and new food items can be added.                                                                                 |      |
| 3.There is a table linked to the food storage database in the  app UI to show the items,calories and expired date. | The user can see the three attributes of saved food item(s) in the storage screen in the form of a table.                  |      |
| 4.There are multiple screens for clear navigation.                                                                 | The user can see a login screen, a register screen, a homescreen, a food storage screen and a add-item screen.             | Met  |
| 5. When adding the items, there is a calendar for the user to pick the date.                                       | The user can use the calendar to pick the date.                                                                            |      |
| 6. The data in the database is not redundant.                                                                      | The user can see "user already exists" when registering by using the same username or email or password as other people's. | Met  |

## Criteria E: Evaluation 
- ### Alpha testing

- ### Beta testing


- [ ] this is an incomplete item


