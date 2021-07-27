# Social Media Database Design Using MySQL

## INTRODUCTION:

This project is about building instagram database clone! And that's actually an exaggeration we're only ***cloning the database*** And even then we're only doing like 7 or 8 
tables not you know 20 or 50 Instagram tables but still we're doing the basics the important stuff photos and comments and users and likes and follow you know follower
following relationships hashtags all that fun stuff all the relationships between them and then all those joints.


We're going to focus on a bit of a case study. We're going to work with a site that you're probably familiar with **Instagram** and we're going to try and clone the database for 
some of the basic functionality so we're not going to be diving into like advertising and keeping track of our users data and all that. We're really focusing on the main big
entities to a site like Instagram things like photos and comments and users and so on. So again we're not really scratching the surface as to how Instagram actually stores
everything. So we will talk a little bit about performance but this is really more about how do you design a schema for something that has (in our example) at least seven or eight
tables in Instagram. The real app there's probably dozens of tables but either way it's a big step up from two tables or three tables Max. For this, We are going to design schemas
for that 7 to 8 tables and then inserting a huge clone data(made for this project) which is provided in the dataset.txt file and finally will run different queries on that
database which are more real world and not traditional direct mentioned.

## SCHEMA DESIGN:
 
![IG_Clone Database Design_1](https://user-images.githubusercontent.com/75497581/124498945-d28d0b80-ddda-11eb-9348-52ba1ffb4e53.jpg)


## Ceating Database: 

I used MySQL Command line Client for this project one can use MySQL Workbench too for this or any other SQL tool/language they comfartable in.

Open command line client/workbench and type following lines to create and use database.

*************************************************************************************
CREATE DATABASE ig_clone;

USE ig_clone;

*************************************************************************************


## Creating tables:

### users table:

CREATE TABLE users (
    id INTEGER AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

*************************************************************************************

### photos table:

 CREATE TABLE photos (
    id INTEGER AUTO_INCREMENT PRIMARY KEY,
    image_url VARCHAR(255) NOT NULL,
    user_id INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    FOREIGN KEY(user_id) REFERENCES users(id)
);

*************************************************************************************

### comments table:

CREATE TABLE comments (
    id INTEGER AUTO_INCREMENT PRIMARY KEY,
    comment_text VARCHAR(255) NOT NULL,
    photo_id INTEGER NOT NULL,
    user_id INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    FOREIGN KEY(photo_id) REFERENCES photos(id),
    FOREIGN KEY(user_id) REFERENCES users(id)
);

*************************************************************************************

### likes table:

CREATE TABLE likes (
    user_id INTEGER NOT NULL,
    photo_id INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    FOREIGN KEY(user_id) REFERENCES users(id),
    FOREIGN KEY(photo_id) REFERENCES photos(id),
    PRIMARY KEY(user_id, photo_id)
);

*************************************************************************************

### follows table:

CREATE TABLE follows (
    follower_id INTEGER NOT NULL,
    followee_id INTEGER NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    FOREIGN KEY(follower_id) REFERENCES users(id),
    FOREIGN KEY(followee_id) REFERENCES users(id),
    PRIMARY KEY(follower_id, followee_id)
);

*************************************************************************************

### tags table:

CREATE TABLE tags (
  id INTEGER AUTO_INCREMENT PRIMARY KEY,
  tag_name VARCHAR(255) UNIQUE,
  created_at TIMESTAMP DEFAULT NOW()
);

*************************************************************************************

### photo_tags table:

CREATE TABLE photo_tags (
    photo_id INTEGER NOT NULL,
    tag_id INTEGER NOT NULL,
    FOREIGN KEY(photo_id) REFERENCES photos(id),
    FOREIGN KEY(tag_id) REFERENCES tags(id),
    PRIMARY KEY(photo_id, tag_id)
);


## Inserting Data into Tables:

We created different tables above and we have our ***ig_dataset.txt*** file with us which is attached above just copy paste that data and create our ig_clone dataset!


## Running Different Queries

Now, Its time for using our database for different real life queries! Attached above a text file named ***ig_queries.txt*** which contains some real life queries along with its solution first of all try out by your own.

Try with your own queries and share herewith! 

