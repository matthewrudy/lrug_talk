!SLIDE 
# Building a Financial App #
# in Rails #
## and all the gems I made along the way ##

!SLIDE bullets incremental
# Who am I?
* Matthew Rudy Jacobs
* @MatthewRudy
* Thought-Sauce.com

!SLIDE bullets
# My summons
* December 30th 2009
* "come help us out"

!SLIDE
# The problem
## Started in Groovy and Grails
## Lack of documentation and community

!SLIDE bullets incremental
# The Application
* Client comes to us for a loan
* 6 months of bank and credit card statements
* Regression and trend analysis

!SLIDE bullets incremental
# 1. Database
* I had only ever used MySQL
* They wanted SQLserver
* A big mess of stored procedures?

!SLIDE bullets incremental
# They Needed 3 "tions"
* Encryption
* Replication
* Referential Integration

!SLIDE bullets incremental
# They Thought They Needed
* SQLServer
* A windows deployment?

!SLIDE bullets incremental
# I didn't plan to give them that

!SLIDE bullets incremental
# The Answer
* Postgres

!SLIDE bullets incremental
# Cool stuff
* CHECK constraints
* ALTER TABLE loans ADD CONSTRAINT usuary_check CHECK (interest_rate < 60);
* Partial Indexes
* CREATE UNIQUE INDEX one_loan_per_client ON loans (client_id) WHERE status='disbursed';

!SLIDE bullets incremental
* Encryption
* (or at least the documentation says you can do it)
* http://www.wikivs.com/wiki/MySQL_vs_PostgreSQL

!SLIDE
# Gem #1 Currency

!SLIDE bullets
## Everything has a currency ##
* Loans
* Repayments
* Bank Statements

!SLIDE bullets incremental
## How do we store them? ##
* Float?
* Decimal?
* Integer?

!SLIDE bullets incremental
# Integer #
## We store ##
* "23 USD" => 2300
* "23 MOP" => 230
* "23 KRW" => 23
* [ISO 4217](http://en.wikipedia.org/wiki/ISO_4217)

!SLIDE bullets incremental
# The Gem should #
* display an integer as a currency
* handle simple arithmetic

 


   
