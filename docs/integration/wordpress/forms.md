# Displaying Public Forms in WordPress Frontend Sites

CiviCRM includes the ability to present online contribution pages, event information pages and registration forms, and profile forms to users and visitors of the 'front-end' of your WordPress sites.

## Create the contribution page, profile, or event

Refer to the main [Profiles Admin](http://wiki.civicrm.org/confluence/display/CRMDOC41/Profiles+Admin) page for an overview and general information on creating Profiles.

## View your public page from the link in the administrative interface

CiviCRM provides links from the administrative interface to the public forms that you generate. When you follow the link, the content of the page is shown within the admin area. This URL will be be basis of the URL for public pages. Here are a few examples:

**Event info:**
 http://your-wordpress-site.org/wp-admin/admin.php?page=CiviCRM&q=civicrm/event/info?reset=1&id=X

**Contribution:**
 http://your-wordpress-site.org/wp-admin/admin.php?page=CiviCRM&q=civicrm/contribute/transact&reset=1&id=X

**Profile "create mode":**
 http://your-wordpress-site.org/wp-admin/admin.php?page=CiviCRM&q=civicrm/profile/create&reset=1&gid=X

## Modify your URL for the front end

CiviCRM displays the pages it generates by appropriating the base URL and replacing the content with CiviCRM content. To start with, just delete the text "wp-admin/admin.php" from the middle of a url, keeping everything before and after it:

**http://your-wordpress-site.org/** wp-admin/admin.php **?page=CiviCRM&q=civicrm/profile/create&reset=1&gid=X**

becomes

**http://your-wordpress-site.org/?page=CiviCRM&q=civicrm/profile/create&reset=1&gid=X**

Try that in your browser (replacing X with the profile ID number), and you will see the front page of your site with the content replaced by the form for CiviCRM profile X. This may be sufficient, and you can typically stop here.

On the other hand, you don't really have control over what else is going on in the page. Maybe you want a different template file or submenu to display. While it's quirky that CiviCRM simply swaps out a page's content for CiviCRM content, you can use this to your advantage.

The page at the URL

**http://your-wordpress-site.org/ ?page=CiviCRM&q=civicrm/profile/create&reset=1&gid=X**

can be thought of as being the page

**http://your-wordpress-site.org/**

overlaid with the CiviCRM content generated by the arguments

**?page=CiviCRM&q=civicrm/profile/create&reset=1&gid=X**

## Use a custom template for CiviCRM front end pages

As described above, CiviCRM public pages are built by overlaying the WordPress front page with CiviCRM content, thus using the front page's template. To use a different template, we must tell Civi to use a different page as a starting point. Follow these steps:

* Add a new WordPress page. We can call it anything, but let's give it a permalink of 'civi'.
* Leave the body blank (it won't be used anyway).
* Select the desired theme template for the page.
* Click Publish.
* Edit your base page through the admin menu at Administer/Settings/CMS Database Integration

Note the legacy method was to define it in the wp-content/plugins/civicrm/civicrm.settings.php file - e.g by setting define( 'CIVICRM_UF_WP_BASEPAGE', 'civi');

URLs that were previously written like:

```
http://yoursite.org/?page=CiviCRM&q=civicrm/contribute/transact&reset=1&id=X
```

[will now be written like:](http://yoursite.org/?page=CiviCRM&q=civicrm/contribute/transact&reset=1&id=X)

```
http://yoursite.org/civi?page=CiviCRM&q=civicrm/contribute/transact&reset=1&id=X
```

For more details, check the issue: [CRM-10682](http://issues.civicrm.org/jira/browse/CRM-10682)