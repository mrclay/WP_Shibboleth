This is a temporary fork of the official WordPress [Shibboleth plugin](http://wordpress.org/extend/plugins/shibboleth/).

It has several fixes for Multisite users stemming from the fact that it stores its plugin settings globally rather that at the site level.

See [shibboleth/readme.txt](WP_Shibboleth/blob/master/shibboleth/readme.txt) for more details.

### What's been done?

All we've done is formalize the limitations caused by shibboleth settings being stored at the network level. In multisite mode we've prevented "regular" admins from changing shib settings, and also required that a user be already added to a site before the plugin will add roles from Shib. The problem still exists that users will get the same roles from shibboleth across all sites they were added to, but at least they can't "surf in" to other site's admin panels to gain the roles there.

### How different is it?

You can compare the current branch with the official plugin's SVN trunk with a few bash commands:

    cd path/to/WP_Shibboleth
    svn export http://svn.wp-plugins.org/shibboleth/trunk wp-shib-trunk
    diff -r shibboleth/ wp-shib-trunk/ > wp.diff
    rm -rf wp-shib-trunk

Now wp.diff will contain all the differences.

(Our `.gitignore` file excludes the files and directories created with this operation.)