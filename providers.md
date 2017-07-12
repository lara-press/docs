# Providers

Required
- ControllerServiceProvider
- HashServiceProvider
- MailServiceProvider - Document override_wordpress Why is this?
- MetaBoxServiceProvider - Required for TemplateAndSidebarServiceProvider
- PostServiceProvider
- SupportServiceProvider
- WordPressAuthServiceProvider
    
Suggested:
- CommandServiceProvider
- MenuServiceProvider - Register Menus
- PostTypeServiceProvider - Register Post Types
- SidebarServiceProvider - Register Sidebars
- ShortcodeServiceProvider - Register Shortcode. Checks for method, then view/shortcodes folder.
- TemplateAndSidebarServiceProvider - Registers Template and Sidebar
- ViewServiceProvider - Register View Composers - $view->composer('partials.header', Header::class); extended class doesn't do anything
- WidgetServiceProvider - Register Widgets
    
Optional:
- AdminPageServiceProvider - Register Admin Pages
- AssetServiceProvider
- HtmlServiceProvider
- TaxonomyServiceProvider