!SLIDE subsection
# Technology

!SLIDE bullets incremental
# How did I get to use Ruby?
* Groovy wasn't working
* Ruby is comfortable
* Rewrite took 5 days
* Could switch to jRuby in the future

!SLIDE bullets incremental
# Other technology
* Postgres
* Ubuntu 10.04 LTS
* Rails 2.3 -> 3.0beta -> 3.0

!SLIDE bullets incremental
# Postgres Faves
* CHECK constraints
* ALTER TABLE loans ADD CONSTRAINT usuary_check CHECK (interest_rate < 60);
* Partial Indexes
* CREATE UNIQUE INDEX one_loan_per_client ON loans (client_id) WHERE status='disbursed';

!SLIDE
# We work on or near Rails edge

!SLIDE bullets incremental
# Do we push our changes back?
* I try
* But "Lighthouse is a ghetto"