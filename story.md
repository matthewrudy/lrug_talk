# Building a Financial App in Rails #
## and all the gems I made along the way ##

# Who am I?
* [Matthew Rudy Jacobs](http://matthewrudy.com)
* @[MatthewRudy](http://twitter.com/matthewrudy)
* [Thought-Sauce.com](http://thought-sauce.com)

# The Story
* I was working in Cambridge
* I got an email
* "Come help us...
*  in Hong Kong...
*  immediately"

# So
* I flew over there
* 2 days later

# The Mess
* Started in Groovy and Grails
* Built as a part-time project
* The developer had run away

# The Business
* Targeting SMEs
* *Unsecured* loans
* 'secured against credit card receivables'
* Repaid *daily*

# The App
* Two Phases
* 1. Risk Analysis
* 2. Loan Management

# 1. Risk Analysis
* 6 months financial history
* Statistics
* Trend Analysis
* Sector-wide comparison

# 1. Risk Analysis
## Objective
* Define a "credit limit"

# 2. Loan Management
* From Request to Disbursement
* Daily Direct Debits
* Handle Reversed Payments
* Ongoing Risk Analysis

# Technology

# Language
* Groovy wasn't working
* Ruby is comfortable
* Rewrite took 5 days
* Could switch to jRuby in the future

# Framework
* uh...
* Rails
* ... 3

# Database
* Expected to use SQLServer
* A big mess of stored procedures?
* A Windows deployment?

# Postgres!
* Feels enterprisey
* Fully featured
* Numerous encryption solutions

# My favourite bits
* CHECK constraints
* ALTER TABLE loans ADD CONSTRAINT usuary_check CHECK (interest_rate < 60);
* Partial Indexes
* CREATE UNIQUE INDEX one_loan_per_client ON loans (client_id) WHERE status='disbursed';

# OS
* Ubuntu 10.04 LTS
* Familiarity vs Optimisation

# Architecture
## How do we model a loan?

# First attempt
Loan
- principal amount
- interest amount
- principal collected
- interest collected

# Add more
- fees added
- fees collected

# Or maybe
Loan
- has many :fees
- has many :repayments

  @@@ ruby
  def loan.outstanding_principal
    self.principal_amount - self.repayments.sum(:principal_amount)
  end

# This escalated!
* different ways to pay
* Reversals
* Partial repayments
* Transfers

# A new model

