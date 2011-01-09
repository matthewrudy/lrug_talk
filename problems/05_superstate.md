!SLIDE subsection
# #5 - SuperState

!SLIDE bullets incremental
# Manage State everywhere
* Loans
* Repayments
* Reconciliations
* ...

!SLIDE
# AASM is too bulky for some things

!SLIDE
# I want
    @@@ ruby
    job.start_processing
    # changes state, and calls :save
    
    job.start_processing!
    # changes state and calls :save!
    
!SLIDE
# SuperState
    @@@ ruby
    include SuperState

    super_state :pending, :initial => true
    super_state :processing
    super_state :completed
    
    super_state_group :outstanding, ["pending", "processing"]
  
    state_transition :start_processing, :pending => :processing
    state_transition :complete_processing, :processing => :completed
    state_transition :complete, :pending => :completed

!SLIDE
# SuperState::CommonStates
   @@@ ruby
   class MyClass < ActiveRecord::Base
     include SuperState::CommonStates
   end