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

INSERT INTO users(username,age,email)
VALUES('monkeyking',5000,'monkeyking@gmail.com');

INSERT INTO users(username,age,email)
VALUES('isabear',38,'isabear.wow@gmail.com');

INSERT INTO users(INSERT INTO users(username,age,email)
VALUES('mochi',8,'mochidoesmaths@math.com');


```

- ## ORM ##
```.mysql
from sqlalchemy import Column, String, Integer)
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker


base = declarative_base()
engine = create_engine('sqlite:///genericApp.sqlite')
session = sessionmaker(bind=engine)

class Users(base):
    __tablename__ = 'users'
    id = Column(Integer,primary_key= True)
    username = Column(String)
    age = Column(Integer)
    email = Column(String)
 

base.metadata.create_all(engine)

user = Users('BananaEater',20,'greatbanana@sales.com')
session.add(user)
session.commit()

- ## Hash Function ##

