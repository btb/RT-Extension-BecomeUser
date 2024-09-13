# RT-Extension-BecomeUser - Become another user

## DESCRIPTION

Extra functionality to become another user. This is reserved for 
people with "SuperUser" or the newly introduced "BecomeUser" right.

Users cannot become SuperUsers.

This module adds a column to the user table in Admin->Users called "become user".
Clicking on the "become" link leads to an ugly page from where you can go to the homepage of the target user.

The title bar in a "sudo session" is overwritten with "back to original account". This serves as a reminder of being a different user and clicking on it leads back to the original account.

Do not become yet another user after having impersonated a different user..

Use this module with care, you really are the other user. Also, be careful with granting the "BecomeUser" right. E.g. granted to an otherwise unprivileged user, it enables this user to become any arbitrarily privileged user (unless SuperUsers).

## IMPROVEMENTS

This module is ugly on purpose in the hope to avoid inadvertent manipulations.
The code is rather straighforward and simple.

It should be easy to make it beautiful if that is what you need.
If you do so, please get back with me before submitting a pull request. It might be better to start a new module like "BecomeUserBeautiful" or "BecomeUserUnobtrusive", in which case you are invited to use this module as a starting point.

## INSTALLATION

### Manual Installation

    cd (root dir of your rt install)
    cd local/
    mkdir -p RT-Extension-BecomeUser
    cd RT-Extension-BecomeUser

unzip the tar, here

Make sure the module gets loaded by including 

    Plugin('RT::Extension::BecomeUser');

into your etc/RT_SiteConfig.pm or a file in etc/RT_SiteConfig.d/

## Changes for RT 5

Updated the overridden Elements/Header to match the rt5 version.
Need to find another place to put that BackToOriginalAccount callback
where we don't have to do an override.

Removed the override to CollectionList, and its AddColumn callback, so the
"become user" links no longer show up on the Admin/Users list. To enable
them again, simply add it to the AdminSearchResultFormat option:

    Set(%AdminSearchResultFormat,
        Users =>
            q{'<a href="__WebPath__/Admin/Users/Modify.html?id=__id__">__id__</a>/TITLE:#'}
            .q{,'<a href="__WebPath__/Admin/Users/Modify.html?id=__id__">__Name__</a>/TITLE:Name'}
            .q{,__RealName__, __EmailAddress__,__SystemGroup__,__Disabled__}
            .q{,'<a href="__WebPath__/BecomeUser.html?id=__id__">become</a>/TITLE:become user'},
    );

### Problems

"back to original account" link doesn't work from SelfService (Unprivileged?).

### Automated Install

    perl Makefile.PL

    make

    make install

Pull requests welcome!

## COPYRIGHT

Copyright (c) 2018 by Matthias Bloch. All rights reserved.

## LICENSE

This library is free software; you can redistribute it and/or modify it under the same terms as Perl itself.

## AUTHOR

Matthias Bloch <matthias.bloch@puffin.ch>

=cut
