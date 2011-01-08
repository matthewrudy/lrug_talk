!SLIDE title-slide
# Building a Financial App in Rails #
## and all the gems I made along the way ##

!SLIDE bullets incremental
# Who am I?
* [Matthew Rudy Jacobs](http://matthewrudy.com)
* @[MatthewRudy](http://twitter.com/matthewrudy)
* [Thought-Sauce.com](http://thought-sauce.com)

!SLIDE bullets incremental
# The Story
* I was working in Cambridge
* I got an email
* "Come help us...
*  in Hong Kong...
*  immediately"

!SLIDE bullets incremental
# So
* I flew over there
* 2 days later

!SLIDE bullets incremental
# The Mess
* Started in Groovy and Grails
* Built as a part-time project
* The developer had run away

!SLIDE bullets incremental
# The Business
* Targeting SMEs
* *Unsecured* loans
* 'secured against credit card receivables'
* Repaid *daily*

!SLIDE bullets incremental
# The App
* Two Phases
* 1. Risk Analysis
* 2. Loan Management

!SLIDE bullets incremental
# 1. Risk Analysis
* 6 months financial history
* Statistics
* Trend Analysis
* Sector-wide comparison

!SLIDE bullets incremental
# 1. Risk Analysis
## Objective
* Define a "credit limit"

!SLIDE bullets incremental
# 2. Loan Management
* From Request to Disbursement
* Daily Direct Debits
* Handle Reversed Payments
* Ongoing Risk Analysis

!SLIDE subsection
# Technology

!SLIDE bullets incremental
# Language
* Groovy wasn't working
* Ruby is comfortable
* Rewrite took 5 days
* Could switch to jRuby in the future

!SLIDE bullets incremental
# Framework
* uh...
* Rails
* ... 3

!SLIDE bullets incremental
# Database
* Expected to use SQLServer
* A big mess of stored procedures?
* A Windows deployment?

!SLIDE bullets incremental
# Postgres!
* Feels enterprisey
* Fully featured
* Numerous encryption solutions

!SLIDE bullets incremental
# My favourite bits
* CHECK constraints
* ALTER TABLE loans ADD CONSTRAINT usuary_check CHECK (interest_rate < 60);
* Partial Indexes
* CREATE UNIQUE INDEX one_loan_per_client ON loans (client_id) WHERE status='disbursed';

!SLIDE bullets incremental
# OS
* Ubuntu 10.04 LTS
* Familiarity vs Optimisation

!SLIDE bullets incremental
# Architecture
## How do we model a loan?

!SLIDE
# My First thought
> Banks have got it wrong
> Let's do it OO

!SLIDE bullets incremental
# First attempt
    @@@ ruby
    class Loan
      property :total_principal,     Bignum
      property :total_interest,      Bignum
      property :collected_principal, Bignum
      property :collected_interest,  Bignum
    end

!SLIDE bullets incremental
# Add more
    @@@ ruby
    class Loan
      property :total_fees,     Bignum
      property :collected_fees, Bignum
    end

!SLIDE bullets incremental
# And more
    @@@ ruby
    class Loan
      property :early_repayment_balance, Bignum
      property :arrears_amount, Bignum
    end

!SLIDE bullets incremental
# And then they say
> We need to add interest daily

!SLIDE bullets incremental
# We need to rethink

!SLIDE bullets incremental
# Fees, Repayments and such are objects
    @@@ ruby
    class Loan
      has_many :fees
      has_many :repayments
    end

!SLIDE bullets incremental
    @@@ ruby
    class Fee
      property :total_amount, Bignum
      property :collected_amount, Bignum
    end

!SLIDE bullets incremental
    @@@ ruby
    class Repayment
      property :date, Date
      property :collected_amount, Bignum
      property :principal_amount, Bignum
      property :interest_amount,  Bignum
      property :fee_amount,       Bignum
    end

!SLIDE bullets incremental
# This escalated!
* different ways to pay
* Reversals
* Partial repayments
* Transfers

!SLIDE bullets incremental
# This works
* its normalised
* everything is traceable

!SLIDE bullets incremental
# But
* we have to work to produce a statement
* number of models rapidly increasing

!SLIDE
# Time to rethink

!SLIDE
# What if our loan structure looked just like a statement?

!SLIDE
## Like a "ledger"
> isn't that what all the banks do?

!SLIDE
> "you're optimising for what you care about"

!SLIDE bullets incremental
# A new model
    @@@ ruby
    class Loan
      has_many :loan_ledgers
      delegate :total_principal, :outstanding_principal, :collected_principal, :to => :loan_ledgers
      ...
    end

!SLIDE bullets incremental
# A loan is just a balance of ledgers
* Amount Disbursed - 100,000 HKD
* Initial Interest -  15,000 HKD
* Repayment 1      -  -1,000 HKD
* Late repayment fee -   100 HKD

!SLIDE
# LoanLedger
    @@@ ruby
    class LoanLedger
      property :code, String
      property :principal_amount, BigInt
      property :interest_amount,  BigInt
      property :fee_amount,       BigInt
      property :rounding,         Decimal
    end


