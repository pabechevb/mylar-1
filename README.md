Meteor-enc

Requires packages: principal, accounts-password, accounts-base


How to use new IDP
==================

Setup:
-------

- start idp on the default port (3000)
- start kChatIDP on port 3004

As a user:
---------

- go to localhost:3000 and login or create an account with idp
- go to localhost:3004 and just click sign in


As a developer of an app
------------------------

0. use packages accounts-idp, idp-user
 
1. specify which IDP you trust, e.g., our IDP:

var idp_pub = '{"encrypt":"021cbeb072a8a136a35efd7d59eac32d4415929bc1ca9d5a0e1e640789079a91dcc534c65119ed3fbddb12c918c5a582","verify":"b7bf9d94519d221ec2dd5cb033da55149852858c776d66bf8568a85a45b099c009c926575494bddf3fe2783c15de337b"}';
idp_init("http://localhost:3000", idp_pub, "http://localhost:3004");

(should be available both client and server-side)

2. use Meteor.loginWithIDP to login the user, no arguments needed

(you can still use server-side Accounts.onCreateUser if useful)


Meteor-enc developers:
----------------------

Here is how the IDP source code is organized:

meteor-enc/idp
: the idp application

packages/accounts-idp:
: provides Meteor.loginWithIDP

packages/idp-user:
: runs at the client-side app, talks to the the window for the idp client in the user's browser

packages/idp-provider:
: runs at the idp client, responds to idp-user



TODO (post-deadline):
======================
-- it would be nice to have the app open a login window to idp upon sign in, instead of asking the user to have a window open with the idp

-- better error messages; for example, now if you try to add a user that does not exist the error is not friendly; 