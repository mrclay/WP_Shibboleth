This is a temporary fork of the official WordPress [Shibboleth plugin](http://wordpress.org/extend/plugins/shibboleth/).

It has several fixes for Multisite users stemming from the fact that it stores its plugin settings globally rather that at the site level.

See [shibboleth/readme.txt](blob/master/shibboleth/readme.txt) for more details.

### How different is it?

You can compare the current branch with the official plugin's SVN trunk with a few bash commands:

    cd path/to/WP_Shibboleth
    svn export http://svn.wp-plugins.org/shibboleth/trunk wp-shib-trunk
    diff -r shibboleth/ wp-shib-trunk/ > wp.diff
    rm -rf wp-shib-trunk

Now wp.diff will contain all the differences.

(Our `.gitignore` file excludes the files and directories created with this operation.)