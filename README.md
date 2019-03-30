Roundcube Dev Identify Avatar
=============================

Non official plug-in showing [Gravatar](https://www.gravatar.com/), Google and Google Plus profile images inside the [Roundcube webmail](https://roundcube.net/) client using [Dev Identify](https://github.com/SociallyDev/dev-identify).

This is partially based on Pau Rodriguez's [gravatar plugin](https://github.com/prodrigestivill/roundcube-gravatar).

It has been implemented as a Roundcube readonly hidden addressbook. You have to ensure this plugin is added into the latest entry in the main config (`$config['plugins']`). 

- If any address book (LDAP, Google, etc...) already has an image for a contact, it will use that image first. 
- If none is found, then it will use Dev Identify.

Tested in Roundcube 1.4.0.


Installation
============

Intallation steps:
  - Via composer:
    - Run `php composer.phar require "empowercreative/devidentify_avatar":"dev-master"`
  - Via git:
    - Clone the repository:
      `cd roundcube/plugins && git clone https://github.com/empower-creative-studios/devidentify_avatar.git devidentify_avatar`
  - Via tarball:
    - Download and extract the tarball into `roundcube/plugins` directory and rename the extracted directory to `devidentify_avatar`


For the expected behaviour **ensure** it is always the latest plugin (or at least addressbook plugin) in the `$config['plugins']` list at `config/config.inc.php`.


To enable per user: Login to Roundcube and enable/disable plugin by navigating to the Settings page, clicking on Preferences, click on Contacts, and Enable Dev Identify Avatar, and Save.


To configure/change default values:
  - Copy `config.inc.php.dist` to `config.inc.php` in the `plugins/gravatar/` directory.
  - Modify the values you are interested in changing and comment the rest with '//'


Custom API
==========

You can define your custom API for photos at 'devidentify_custom_avatar_api' in `config.inc.php` in `plugins/gravatar/` directory. With the following substitutions.
  - %%: literal '%'
  - %s: schema ('http', 'https') depending of 'gravatar_https' config
  - %e: contact email (escaped with urlencode)
  - %m: hashed md5(email)
  - %a: hashed sha1(email)
  - %z: configured avatar size (in px)
  - %r: configured rating ('g', 'pg', 'r', 'x')

Usage for default Gravatar API is: `%s://www.gravatar.com/avatar/%m?s=%z&r=%r&d=404`


You can use local files, it does not need to be a URL. But if you plan to use it for direct filesystem access, for security reasons it is best to only use hashed email substitutions, even though all parameters are escaped with urlencode.


Examples:
```php
$config['gravatar_custom_photo_api'] = 'http://www.example.com/directory/%e.jpg?s=%z';
//OR//
$config['gravatar_custom_photo_api'] = '/path/%m.jpg';
```

## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fempower-creative-studios%2Fdevidentify_avatar.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fempower-creative-studios%2Fdevidentify_avatar?ref=badge_large)
