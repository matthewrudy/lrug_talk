!SLIDE subsection
# #1 - How to model a loan

!SLIDE
# Version 1
    @@@ ruby
    class Loan
      property :total_principal,     Bignum
      property :total_interest,      Bignum
      property :collected_principal, Bignum
      property :collected_interest,  Bignum
    end
    
!SLIDE
# Gets bigger
    @@@ ruby
    class Loan
      property :total_principal,     Bignum
      property :total_interest,      Bignum
      property :collected_principal, Bignum
      property :collected_interest,  Bignum
      property :total_fees,          Bignum
      property :collected_fees,      Bignum
    end

!SLIDE
# And bigger
    @@@ ruby
    class Loan
      property :total_principal,     Bignum
      property :total_interest,      Bignum
      property :collected_principal, Bignum
      property :collected_interest,  Bignum
      property :total_fees,          Bignum
      property :collected_fees,      Bignum
      property :early_payment_balance, Bignum
      property :arrears_amount,      Bignum
    end
    
!SLIDE
# Version 2
    @@@ ruby
    class Loan
      has_many :fees
      has_many :repayments
    end

    class Fee
      property :total_amount, Bignum
      property :collected_amount, Bignum
    end
    
!SLIDE
# Repayments are pretty complex
    @@@ ruby
    class Repayment
      property :date, Date
      property :collected_amount, Bignum
      property :principal_amount, Bignum
      property :interest_amount,  Bignum
      property :fee_amount,       Bignum
    end
    
!SLIDE
# Time to rethink

!SLIDE
# A loan is just a balance of ledgers

> Amount Disbursed: 100,000 HKD

> Initial Interest:  15,000 HKD

> Repayment:         -1,000 HKD

> Late repayment fee:   100 HKD

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

!SLIDE
# LoanLedger
    @@@ ruby
    class LoanLedger
    
      def self.total_principal
        self.creative_codes.sum(:principal_amount)
      end
      
      def self.outstanding_principal
        self.sum(:principal_amount)
      end
      
!SLIDE
# The accountants got it right
