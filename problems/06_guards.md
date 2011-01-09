!SLIDE subsection
# #6 - Guards

!SLIDE
# Guard method execution
    @@@ ruby
    def payoff_now!(user)
      transaction do
        self.payoff!(user)
      end
    end
    guard :payoff_now!, :only => :disbursed?