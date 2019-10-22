# NAME

Mojolicious::Command::bcrypt - bcrypt a password using the settings in your Mojolicious app.

# STATUS

<div>
    <a href="https://travis-ci.org/srchulo/Mojolicious-Command-bcrypt"><img src="https://travis-ci.org/srchulo/Mojolicious-Command-bcrypt.svg?branch=master"></a>
</div>

# SYNOPSIS

    Usage: myapp.pl bcrypt password [OPTIONS]

    NOTE: If no options are provided, the bcrypt helper installed on your app will
    be used to generate the crypted text. See Mojolicious::Plugin::BcryptSecure for more info.

    Options:
      -c, --cost           Uses this cost instead of the one used in your application. Must be an integer between 1 and 99. Default is 12.
      -nkn, --no-key-nul   Flag that specifies that NUL should not be appended to the password before using it as a key. Default is to append NUL.
                           If an empty password is provided, NUL must be appended and will be by Crypt::Eksblowfish::Bcrypt.
      -s, --salt           22 base 64 digits. Default is Crypt::Eksblowfish::Bcrypt::en_base64(Crypt::URandom::urandom(16))

    # output password with your app's bcrypt helper and settings
    ./myapp.pl bcrypt password

    # output password not using a bcrypt helper by providing custom settings
    ./myapp.pl bcrypt password --c 8
    ./myapp.pl bcrypt password --cost 8

    # do not append a NUL before the password (not recommended)
    ./myapp.pl bcrypt password --nkn
    ./myapp.pl bcrypt password --no-key-nul

    # provide your own salt
    ./myapp.pl bcrypt password --s YndOHub.EV9Y37VeobUeSu
    ./myapp.pl bcrypt password --salt YndOHub.EV9Y37VeobUeSu

    # combine options
    ./myapp.pl bcrypt password --c 8 --nkn --s YndOHub.EV9Y37VeobUeSu

# DESCRIPTION

[Mojolicious::Command::bcrypt](https://metacpan.org/pod/Mojolicious::Command::bcrypt) allows you to crypt a password using `bcrypt` via a [Mojolicious::Command](https://metacpan.org/pod/Mojolicious::Command).

If you are using a [Mojolicious::Plugin](https://metacpan.org/pod/Mojolicious::Plugin) like [Mojolicious::Plugin::BcryptSecure](https://metacpan.org/pod/Mojolicious::Plugin::BcryptSecure) or [Mojolicious::Plugin::Bcrypt](https://metacpan.org/pod/Mojolicious::Plugin::Bcrypt) that installs a
`bcrypt` helper, then this helper along with any settings you provided the plugin will be used to generate the crypted text:

    # crypt using bcrypt helper
    ./myapp.pl bcrypt password

If you provide any ["OPTIONS"](#options), the `bcrypt` helper (if present) will be ignored, and crypted text will be generated from the provided
["OPTIONS"](#options) and any defaults:

    ./myapp.pl bcrypt password --cost 8

# COMMAND OPTIONS

## --cost

A non-negative integer with at most two digits that controls the cost of the hash function.
The number of operations is proportional to 2^cost. The default value is 12.
This option is described more in [Crypt::Eksblowfish::Bcrypt](https://metacpan.org/pod/Crypt::Eksblowfish::Bcrypt).

    ./myapp.pl bcrypt password --cost 8

    # short option
    ./myapp.pl bcrypt password --c 8

## --no-key-nul

If present, a NUL is not appended to the password before it is used as a key. The default is to append a NUL and this flag is not recommended.
This option is described more in [Crypt::Eksblowfish::Bcrypt](https://metacpan.org/pod/Crypt::Eksblowfish::Bcrypt).

    ./myapp.pl bcrypt password --no-key-nul

    # short option
    ./myapp.pl bcrypt password --nkn

## --salt

22 base 64 digits that will be used as the salt. The default is `Crypt::Eksblowfish::Bcrypt::en_base64(Crypt::URandom::urandom(16))`.
This option is described more in [Crypt::Eksblowfish::Bcrypt](https://metacpan.org/pod/Crypt::Eksblowfish::Bcrypt).

    ./myapp.pl bcrypt password --salt YndOHub.EV9Y37VeobUeSu

    # short option
    ./myapp.pl bcrypt password --s YndOHub.EV9Y37VeobUeSu

# AUTHOR

Adam Hopkins <srchulo@cpan.org>

# COPYRIGHT

Copyright 2019- Adam Hopkins

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# SEE ALSO

- [Mojolicious::Plugin::BcryptSecure](https://metacpan.org/pod/Mojolicious::Plugin::BcryptSecure)
- [Crypt::Eksblowfish::Bcrypt](https://metacpan.org/pod/Crypt::Eksblowfish::Bcrypt)
- [Crypt::URandom](https://metacpan.org/pod/Crypt::URandom)
- [Mojolicious::Plugin::Bcrypt](https://metacpan.org/pod/Mojolicious::Plugin::Bcrypt)
