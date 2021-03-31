# iEat

``iEat`` -- a food stock app


## Criteria A: Planning
- ### Context of the problem
My client Isabel wants to have an app which includes a database to help her better organize her food stock. She used to record on an online note but she seldom 
updated due to the usability of the online note and things were not recorded in neat. Therefore, by using this app, she wants to get a clear overview of
what food she has and the expired date of the food as well as keep track on the calories she intakes for every meal.

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
- ###  .py

## Criteria D: Functionality
- ### Success Criteria


## Criteria E: Evaluation 
- ### Alpha testing
- ### Beta testing


- [ ] this is an incomplete item


