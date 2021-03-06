=== Shibboleth ===
Contributors: willnorris, mitchoyoshitaka, mr7clay
Tags: shibboleth, authentication, login, saml
Requires at least: 2.8
Tested up to: 3.1.1
Stable tag: 1.4

Allows WordPress to externalize user authentication and account creation to a
Shibboleth Service Provider.

Note: This is a temporary fork of the official Shibboleth plugin available at
http://wordpress.org/extend/plugins/shibboleth/

== Description ==

This plugin is designed to support integrating your WordPress or WordPress MU
blog into your existing identity management infrastructure using a
[Shibboleth][] Service Provider.  

WordPress can be configure so that all standard login requests will be sent to
your configured Shibboleth Identity Provider or Discovery Service.  Upon
successful authentication, a new WordPress account will be automatically
provisioned for the user if one does not already exist.  User attributes
(username, first name, last name, display name, nickname, and email address)
can be synchronized with your enterprise's system of record each time the user
logs into WordPress.  

Finally, the user's role within WordPress can be automatically set (and
continually updated) based on any attribute Shibboleth provides.  For example,
you may decide to give users with an eduPersonAffiliation value of *faculty*
the WordPress role of *editor*, while the eduPersonAffiliation value of
*student* maps to the WordPress role *contributor*.  Or you may choose to limit
access to WordPress altogether using a special eduPersonEntitlement value.

[Shibboleth]: http://shibboleth.internet2.edu/

== Installation ==

First and foremost, you must have the Shibboleth Service Provider [properly
installed][] and working.  If you don't have Shibboleth working yet, I assure
you that you won't get this plugin to work.  This plugin expects Shibboleth to
be configured to use "lazy sessions", so ensure that you have Shibboleth
configured with requireSession set to "false".  Upon activation, the plugin
will attempt to set the appropriate directives in WordPress's .htaccess file.
If it is unable to do so, you can add this manually:

    AuthType Shibboleth
    Require Shibboleth

= For single-user WordPress =

Upload the `shibboleth` folder to your WordPress plugins folder (probably
`/wp-content/plugins`), and activate it through the WordPress admin panel.
Configure it from the Shibboleth settings page.

= For Multisite =

Shibboleth works, but there is a big limitation in that the settings are
network-wide. This has several implications: 1) only "super" network admins can 
access/change Shibboleth settings. 2) the plugin will only assign roles if the 
user has already been added to the site (e.g. by an admin). 3) in any site the
user has been added to, shibboleth will assign her that role (if your an editor,
you'll be an editor in every site you're added it).

== Frequently Asked Questions ==

= What is Shibboleth? =

From [the Shibboleth homepage][]: 

> The Shibboleth System is a standards based, open source software package for
> web single sign-on across or within organizational boundaries. It allows
> sites to make informed authorization decisions for individual access of
> protected online resources in a privacy-preserving manner.

[the Shibboleth homepage]: http://shibboleth.internet2.edu/

= Can I extend the Shibboleth plugin to provide custom logic? =

Yes, the plugin provides a number of new [actions][] and [filters][] that can
be used to extend the functionality of the plugin.  Search `shibboleth.php` for
occurances of the function calls `apply_filters` and `do_action` to find them
all.  Then [write a new plugin][] that makes use of the hooks.  If your require
additional hooks to allow for extending other parts of the plugin, please
notify the plugin authors via the [support forum][].

Before extending the plugin in this manner, please ensure that it is not
actually more appropriate to add this logic to Shibboleth.  It may make more
sense to add a new attribute to your Shibboleth Identity Provider's attribute
store (e.g. LDAP directory), or a new attribute definition to the  Identity
Provider's internal attribute resolver or the Shibboleth Service Provider's
internal attribute extractor.  In the end, the Shibboleth administrator will
have to make that call as to what is most appropriate.

[actions]: http://codex.wordpress.org/Plugin_API#Actions
[filters]: http://codex.wordpress.org/Plugin_API#Filters
[write a new plugin]: http://codex.wordpress.org/Writing_a_Plugin
[support forum]: http://wordpress.org/tags/shibboleth?forum_id=10#postform

== Screenshots ==

1. Configure login, logout, and password management URLs
2. Specify which Shibboleth headers map to user profile fields
3. Assign users into WordPress roles based on arbitrary data provided by Shibboleth

== Changelog ==

= github version (2011-04-21) =
 - more sane Multisite handling
 - fix for multisite logins

= version 1.4 (2010-08-30) =
 - tested for compatibility with WordPress 3.0
 - new hooks for developers to override the default user role mapping controls
 - now applies `sanitize_name()` to the Shibboleth user's `nicename` column

= version 1.3 (2009-10-02) = 
 - required WordPress version bumped to 2.8
 - much cleaner integration with WordPress authentication system
 - individual user profile fields can be designated as managed by Shibboleth
 - start of support for i18n.  If anyone is willing to provide translations, please contact the plugin author

= version 1.2 (2009-04-21) =
 - fix bug where shibboleth users couldn't update their profile. (props pchapman on bug report)
 - fix bug where local logins were being sent to shibboleth

= version 1.1 (2009-03-16) =
 - cleaner integration with WordPress login form (now uses a custom action instead of hijacking the standard login action)
 - add option for enterprise password change URL -- shown on user profile page.
 - add option for enterprise password reset URL -- Shibboleth users are auto-redirected here if attempt WP password reset.
 - add plugin deactivation hook to remove .htaccess rules
 - add option to specify Shibboleth header for user nickname
 - add filters for all user attributes and user role (allow other plugins to override these values)
 - much cleaner interface on user edit admin page
 - fix bug with options being overwritten in WordPress MU

= version 1.0 (2009-03-14) =
 - now works properly with WordPress MU
 - move Shibboleth menu to Site Admin for WordPress MU (props: Chris Bland)
 - lots of code cleanup and documentation

= version 0.1 =
 - initial public release

