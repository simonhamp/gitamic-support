---
description: >-
  Once you've installed Gitamic, you'll need to update your application's
  configuration. This is usually a one-time thing for each Statamic site where
  you use Gitamic.
---

# 🎛 Setup

### 1. Register the add-on within Statamic

Update your `config/statamic/editions.php` config file to indicate that you're using the `pro` edition of Gitamic:

```php
'addons' => [
    'simonhamp/gitamic' => 'pro',
],
```

### 2. \[Optional] Set the commit author details

By default, Gitamic uses the following details for the git committer name and email address:

* name: `Gitamic`
* email: `gitamic@[domain from APP_URL]`

You can easily override these values in your `.env` by adding the following keys, e.g.:

```dotenv
GITAMIC_GIT_USER_NAME="Simon Hamp"
GITAMIC_GIT_USER_EMAIL="simon.hamp@me.com"
```

Alternatively, publish the Gitamic config file to your application. This should already happen as part of the add-on's installation, but for some reason it doesn't exist, run the following command in your terminal:

```bash
php artisan vendor:publish --provider=SimonHamp\\Gitamic\\ServiceProvider
```

Then, if you prefer your whole team to use the same committer details, you can hard-code these settings into the `config/gitamic.php` config file.

{% hint style="info" %}
If you're using Statamic Pro's Git Integration and would prefer Gitamic to use the same set of user details, simply set these values to `null` in your `config/gitamic.php` config file.\
\
Gitamic will then use `STATAMIC_GIT_USER_NAME` and `STATAMIC_GIT_USER_EMAIL` instead, if those have been defined.
{% endhint %}

If you'd like to use the details of the logged-in Statamic user as the committer, you will need to enable the `gitamic.use_authenticated` option in `config/gitamic.php`:

```php
return [
    'use_authenticated' => true,

    'user' => ...
];
```

### 3. \[Optional] Statamic Pro

If you have [Statamic Pro](https://statamic.com/pricing) (you should, it's great!) and you have [Statamic's Git Automation](https://statamic.dev/git-automation) enabled, you may find it better to _disable_ Statamic's '[automatic commits](https://statamic.dev/git-automation#committing-changes)' feature so that Statamic doesn't automatically commit every change.

This will leave you to manage your commits via Gitamic, if that's what you prefer.

To disable Statamic's automatic commits, add the following to your `.env` file:

```dotenv
STATAMIC_GIT_AUTOMATIC=false
```

***

{% hint style="info" %}
You should commit these changes to your application to save the rest of your team from having to follow the same steps
{% endhint %}
