# Generic application 
- ## ER Diagram ##
    [ER Diagram](https://lucid.app/lucidchart/7f5717f1-6e19-45b9-b386-3edb2a63f7c8/edit?beaconFlowId=0377A30A9A8E3BED&page=0_0#?folder_id=home&browser=icon) 

- ## SQL Script ##
```.mysql
CREATE TABLE IF NOT EXISTS users(
    id integer primary key autoincrement not null,
    username VARCHAR(20),
    age INTEGER,
    email VARCHAR(60),
);

INSERT INTO users(username,age,email,phone)
VALUES('monkeyking',5000,'monkeyking@gmail.com',15087420901);

INSERT INTO email(email)
VALUES('monkeyking@gmail.com');

INSERT INTO users(username,age,email,phone)
VALUES('isabear',38,'isabear.wow@gmail.com',13389032571);

```

ORM


- ## Hash Function ##

