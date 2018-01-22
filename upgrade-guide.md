# Update Guide

- [Upgrading to 5.5.1 from 5.5.0](#upgrading-to-5.5.1-from-5.5.0)

## Upgrading to 5.5.1 from 5.5.0

This update changes templates to work with [ACF](https://www.advancedcustomfields.com/) fields. 

For Models implementing the CustomPostType interface, change the `customPostTypeData` method to a static method from instance method.

If you were using the Template & Sidebar metabox from the TemplateAndSidebarServiceProvider, templates are now handled with WordPress meta. In models implementing the CustomPostType interface, return an array of available templates from the static `getAvailableTemplates` method. Use the updated [SideBarServiceProvider](https://github.com/lara-press/larapress/blob/5.5.1/app/Providers/SidebarServiceProvider.php) to create a sidebar metabox.
