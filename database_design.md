# Database Design

## Adlister Application
Let's design the database for AdLister! The adlister is a small scale craigslist clone where users can post ads for items.

### Specifications

* Users sign up for the site with an email and password
* Users create ads with a title and description and category.
* Each ad is associated with the user that created it.
* An ad can be in one or more categories (for example, "help wanted", "giveaway", or "furniture")

#### Users sign up for the site with an email and password

For this we will need a users table in the database with 3 columns:

* id
* email
* password

#### Users create ads with a title and description and category.

For this we will need a ads table in the database with 4 columns:

* id 

#### Each ad is associated with the user that created it.

#### An ad can be in one or more categories (for example, "help wanted", "giveaway", or "furniture")

### Creation

#### First let's sketch out the database:

![Sketch of adlister database that shows the relationships between the tables](adlister_database_sketch.jpg)

## Queries

Write SQL queries to answer the following questions:

1. For a given ad, what is the email address of the user that created it?
2. For a given ad, what category, or categories, does it belong to?
3. For a given category, show all the ads that are in that category.
4. For a given user, show all the ads they have posted.