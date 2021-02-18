# Generic application 
- ## ER & UML Diagram ##
    [ER & UML Diagram](https://lucid.app/lucidchart/7f5717f1-6e19-45b9-b386-3edb2a63f7c8/edit?beaconFlowId=0377A30A9A8E3BED&page=0_0#?folder_id=home&browser=icon) 

- ## SQL Script ##
```.mySQL
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
```.mySQL
from sqlalchemy import Column, String, Integer
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
```

- ## Hash Function ##

Hash function is a function that converts a given series of numbers or a piece of data (password, private messages) into a fixed-size value. There are two characteristcs about hashing. One is irreversibility, which means there is no way back when the data is hashed; the other one is uniqueness, refering that there are no same hash values for two different data pieces. Because of these two characterics, the security of important or private data is greatly increased. Unlike simple encrytion, the hash function performs much more complicated for decoding(almost impossible) and can save memory for the users. 

To get the the hash value of a set length(usually 160-512 bits), we need to input data into fixed-size blocks. These blocks are called ["data blocks"](https://cheapsslsecurity.com/blog/wp-content/uploads/2017/09/hashing-function-structure.png). The size of the data block(s) differs from one algorithm to another. But for a particular algorithm, it remains the same. So, if the message is exactly of 512-bit length, the hash function runs only once (80 rounds in case of SHA-1). Similarly, if the message is 1024-bit, it’s divided into two blocks of 512-bit and the hash function is run twice. However, 99% of the time, the message won’t be in the multiples of 512-bit. For such cases (almost all cases), a technique called Padding is used. Using a **padding technique**, the entire message is divided into fixed-size data blocks. The hash function is repeated as many times as the number of data blocks. [Image to show how it works](https://cheapsslsecurity.com/blog/wp-content/uploads/2017/09/the-avalanche-effect-in-hashing.png)  

[References](https://cheapsslsecurity.com/blog/decoded-examples-of-how-hashing-algorithms-work/)
