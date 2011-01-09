!SLIDE subsection
# #2 - Currency

!SLIDE bullets incremental
# How do we store them? #
* Float?
* Decimal?
* Integer?

!SLIDE
# Currency gem
    @@@ ruby
    class Loan
      currency_field :principal_amount
    end
    loan.principal_amount_as_currency
    # 100,000.00 HKD
    loan.as_currency(123_456_78)
    # 123,456.78 HKD