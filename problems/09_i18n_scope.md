!SLIDE subsection
# #9 - I18nScope

!SLIDE
# Bored of
    @@@
    <h2>
      <%= t('some.aspect.title) %>
    </h2>
    
    <%= link_to(
      t('some.aspect.link.apples'),
      apples_path) %>
    
!SLIDE
# Just gets more complicated
## I18n.t("something.about.something.you.know")


!SLIDE
# Why not?
## I18n.scoped.something.about.something.you.know

!SLIDE
# gem "i18_scope"
    @@@
    <% i18n = I18n.scoped.some.aspect %>
    
    <h2>
      <%= i18n.title %>
    </h2>
    <%= link_to(
      i18n.link.apples,
      apples_path) %>
    
    