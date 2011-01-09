!SLIDE subsection
# #4 - Reportify

!SLIDE bullets
# Every Report
* html view
* pdf download
* csv export

!SLIDE
# Boring!

!SLIDE
# Reportify!
    @@@ ruby
    list :details do
      property "Date", report.date, :type => :date
      property "Territory", report.territory
      property "VAT rate", report.vat, :type => :percentage
    end
    
!SLIDE
    @@@ ruby
    table :summary do
      header do
        line do
          value "date"
          value "amount"
        end
      end
      body do
        line do
          value settlement.date, :type => :date
          value settlement.amount_as_currency, :type => :currency
        end
      end
      footer do
        line :type => :currency do
          value "total"
          value report.total_as_currency, :type => :currency
        end
      end
    end
    
!SLIDE
    @@@ ruby
    report = MyReport.new
    report.to_html # returns a builder object
    report.to_pdf  # returns a prawn object
    report.to_csv  # returns some csv