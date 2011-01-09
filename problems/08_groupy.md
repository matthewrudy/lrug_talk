!SLIDE subsection
# #8 - Groupy

!SLIDE
# Categorisation
    @@@ ruby
    class User
      ROLES = %w( superadmin sales_agent data_entry )
      
      def superadmin?
        self.role == "superadmin"
      end
      scope :superadmin, where(:role => "superadmin")
      
      def non_superadmin?
        !superadmin?
      end
      scope :non_superadmin, where(["role != ?", "superadmin"])
    end

!SLIDE
# gem "groupy"
    @@@ ruby
    class User
      include Groupy
      groupy :role do
        value :superadmin
        group :non_superadmin do
          value :sales_agent
          value :data_entry
        end
      end
    end
    
    