What?
=====

A very basic two factor authentication service for mcollective.

A webservice runs centrally and has a private key.  Users log
into the webservice and authenticates using duo security:

    % mco login
    User Name: rip
    Password: ******
    Performing two factor authentication against webservice and duo security....
    Token saved to /home/rip/.mcollective.token valid till Thu Aug 23 22:24:02 +0100 2012

Once logged in every mcollective client request is submitted to the
webservice which would validate the token and and return a signature
and encrypted user name.

The client will then submit the request including the secure
hashes and encrypted username to the network.  Each receiving
node will decrypt the data using the public key for the webservice
if succesfull the request gets dispatched and replies get sent
direct to the client.

This way there is a central authority thats authorative for
any and all mcollective requests on the entire network.  There
is only 1 set of SSL keys on the network which makes securing
the whole easier.

The end result is that the identity of users are not tied to
a certificate file name or unix user but to whatever the webservice
declares the user name is.  This username is used throughout in
all Auditing and Authorization done by mcollective

*This is a proof of concept to demonstrate the basic design of
such a system and not for wider use just yet.*
