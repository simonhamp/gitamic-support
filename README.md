---
description: >-
  Gitamic is a premium Statamic add-on that allows you to take full control of
  your git workflow from within your CMS.
---

# 👋 Introduction

**Gitamic** adds a simple, beautiful and intuitive git UI to your Statamic CP so that you can have more control over your commits.

It's great for solo sites where you want more granular control of your git history, but really shines on more complex sites that rely on live-publishing whilst pushing changes from your Statamic CP back to your git repository.

### Features

Gitamic supports many of the features you'd expect from a git GUI:

* View the 'working tree'
* Stage and unstage changes (in bulk)
* Discard unstaged changes
* Commit staged changes
* Push to & pull from the remote branch
* See the commit history
* File diffs

**Gitamic is under active development.** More features are on the way. If you've got any specific requests, please see how to raise [#bugs-features](./#bugs-features "mention")

Please support this project by purchasing a license, as it allows me to continue working on it. 🙏

### Requirements

| Gitamic  | v1    | v2    |
| -------- | ----- | ----- |
| PHP      | 7.4+  | 8.0+  |
| Statamic | 3+    | 4+    |
| Git      | 2.30+ | 2.30+ |

### Installation

1. To install and use Gitamic, you first need a license key. Purchase one on [Anystack](https://marketplace.anystack.sh/item/gitamic)
2. Activate your license key in your Anystack dashboard
3. Install Gitamic (see below)

#### Composer

To install Gitamic, you must use [Composer.](https://getcomposer.org/)

Firstly, add the private repository URL to the `repositories` array in your `composer.json`:

```json
"repositories": [
  {
    "type": "composer",
    "url": "https://gitamic.composer.sh"
  }
],
```

Then, install the package:

```bash
composer require simonhamp/gitamic
```

You'll then be prompted to authenticate against the private package repository.

```bash
Loading composer repositories with package information
Authentication required (gitamic.composer.sh):
  Username: [licensee-email]
  Password: [license-key]
```

Use the email address you used to purchase Gitamic as the `Username`.

**If you purchased a Gitamic license via the Statamic Marketplace, your `Password` here is simply your license key**

Otherwise, the `Password` is your license key followed by a colon `:` and the domain name you entered when activating your license.

For example, if your license key was `9227fd74-ed29-4d1a-ad75-0bc41bea16a9` and you set the domain setting in your Anystack portal when activating your license to `abc-widgets.com`, the your `Password` would be:

```
9227fd74-ed29-4d1a-ad75-0bc41bea16a9:abc-widgets.com
```

### Setup

Once Composer has finished downloading the necessary dependencies, you'll need to update your application's configuration.

#### 1. Register the add-on with Statamic

Update your `config/statamic/editions.php` config file to indicate that you're using the `pro` edition of Gitamic:

```php
'addons' => [
    'simonhamp/gitamic' => 'pro',
],
```

#### 2. \[Optional] Set the git committer

By default, Gitamic uses the following details for the git committer name and email address:

* name: `Gitamic`
* email: `gitamic@[domain from APP_URL]`

You can easily override these values in your `.env` by adding the following keys, e.g.:

```dotenv
GITAMIC_GIT_USER_NAME="Simon Hamp"
GITAMIC_GIT_USER_EMAIL="simon.hamp@me.com"
```

> If you're using Statamic Pro's Git Integration and would prefer Gitamic to use the same set of user details, simply set these values to `null` in you `config/gitamic.php` or empty in your Gitamic Settings, and it will use `STATAMIC_GIT_USER_NAME` and `STATAMIC_GIT_USER_EMAIL` instead, if those are defined.

If you'd like to use the details of the logged-in Statamic user as the committer, you will need to enable the `gitamic.use_authenticated` option in `config/gitamic.php`:

```php
return [
    'use_authenticated' => true,

    'user' => ...
];
```

You will need to publish this config file to your site in order to make that change (this should already be done as part of the add-on's installation):

```bash
php artisan vendor:publish --provider=SimonHamp\\Gitamic\\ServiceProvider
```

### Statamic Pro

**Gitamic does not require Statamic Pro**, nor [Statamic's Git Integration](https://statamic.dev/git-integration) to be enabled.

If however you do have Statamic Pro and you have Statamic's Git Integration enabled, you may find it better to _disable_ Statamic's 'automatic commits' feature so that Statamic doesn't automatically commit every change.

This will leave you to manage your commits via Gitamic, if that's what you prefer.

To disable Statamic's automatic commits, add the following to your `.env` file:

```dotenv
STATAMIC_GIT_AUTOMATIC=false
```

### Auto-deployment

If you're using Gitamic to `push` commits on a server that is also the target for automated deployments, when you `push` from Gitamic it might trigger a redundant deployment back to the environment that is the _source_ of those changes.

To prevent this, in your deployment script, you will need to write a statement that exits the deployment when it detects that Gitamic initiated the commit.

For example, if you use [Laravel Forge](https://forge.laravel.com/) (haven't customised the git commiter name - see [#2.-optional-set-the-git-committer](./#2.-optional-set-the-git-committer "mention")), you could add the following to the beginning of your deploy script, which inspects the author of the commit and stops the process before it begins:

```bash
[[ "$FORGE_DEPLOY_AUTHOR" == "Gitamic" ]] && echo "Commit by $FORGE_DEPLOY_AUTHOR" && exit 0

# The rest of your deployment script...
```

However, the specific approach you should use will depend on your unique setup.

### Bugs and Feature Requests <a href="#bugs-features" id="bugs-features"></a>

If you experience any problems with Gitamic or would like to make a feature request, please [raise an issue](https://github.com/simonhamp/gitamic-support/issues) using the appropriate template.

You can also find me ([@simonhamp](https://twitter.com/simonhamp)) in the `#3rd-party` channel on the [Statamic Discord](https://statamic.com/discord). (Note that I will likely still ask you to fill out a GitHub issue).

### Security

If you discover any security related issues, please **do not** raise an issue on GitHub. Email gitamic@simonhamp.me instead.

**Please note that I will not respond to feature requests or bug reports at this email address.**

See [SECURITY](https://github.com/simonhamp/Gitamic/blob/main/SECURITY.md) for more details.

### License

Gitamic is a premium add-on and you must purchase a license key in order to use it.

See [LICENSE](https://github.com/simonhamp/Gitamic/blob/main/LICENSE.md).
