!SLIDE subsection
# #3 - Percentise

!SLIDE
# Always the same thing
    @@@ ruby
    def principal_percentage
      if total_amount > 0
        100.0 * principal_amount / total_amount
      end
    end
    
!SLIDE
# That's ok

!SLIDE
# But this is nicer
    @@@ ruby
    def principal_percentage
      Percentise(principal_amount, total_amount)
    end
    
!SLIDE
# gem "percentise"
    @@@ ruby
    Percentise(50, 100)
    # => 50.0 %
    
    Percentise(0,0)
    # => 0.0 %
    
    Percentise.diff(50, 100)
    # => -50.0 %