!SLIDE subsection
# #10 - WhitelistMailProxy

!SLIDE bullets incremental
# Staging
* Must behave like production
* All features must be tested
* Must not send emails to clients

!SLIDE
# Hack ActionMailer?

!SLIDE smaller
# gem "whitelist_mail_proxy"
    @@@ ruby
    # load the production environment
    require File.dirname(__FILE__)+"/production.rb"

    # then make any changes
    Merlot::Application.configure do
      config.action_mailer.delivery_method = :whitelist_proxy
      config.action_mailer.whitelist_proxy_settings = {
        :delivery_method =>:smtp,
        :domain => ["thought-sauce.com", "advanced-pay.com"]}
    end
    
!SLIDE
# Raises an error
    @@@ ruby
    rescue_from WhitelistMailProxy::BlockedDelivery do |exception|
      flash[:error] = "Email Blocked"
      message = "<h1>WhitelistMailProxy::BlockedDelivery</h1>\n<p>#{ exception.message }></p>"
      render :inline => message, :layout => "application"
   end