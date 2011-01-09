!SLIDE subsection
# #7 - Locking

!SLIDE bullets incremental
# We want
* avoid simultaneous execution
* avoid running twice
* minimise lock time

!SLIDE bullets incremental
# The process
* grab a db lock
* reload
* push a state change

!SLIDE
# Like this?
    @@@ ruby
    def process!
      # grab a lock
      transaction do
        lock!
        reload
        start_processing!
      end
      # in a new transaction
      transaction do
        # do our stuff
      end
      # completed
      complete_processing!
    end
      