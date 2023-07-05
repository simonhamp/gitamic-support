---
description: Some notes on various deployment scenarios whilst using Gitamic.
---

# 🛳 Deployment

### Authentication

When building your application in its production environment or running it through a CI[^1] pipeline, you will likely need to install its dependencies, and this may include Gitamic.

When that happens, Composer will need to authenticate against the private repository in order to install Gitamic.

You probably don't want to be doing this manually in a terminal every time – and [thanks to Composer, you don't have to](https://getcomposer.org/doc/articles/authentication-for-private-packages.md)!

How you authenticate will depend on how you deploy:

{% tabs %}
{% tab title="Laravel Forge" %}
Laravel Forge has [built-in support](https://forge.laravel.com/docs/1.0/sites/packages.html) for private package repository authentication.

* Repository URL: **`gitamic.composer.sh`**
* Username: Your Anystack email address
* Password: [Your license key](installation.md#anystack) (which depends on how you purchased it)
{% endtab %}

{% tab title="Netlify" %}
Create a `COMPOSER_AUTH` Environment Variable with the JSON structure that Composer expects, e.g.

```json
{"http-basic":{"HOSTNAME":{"username":"USERNAME","password":"PASSWORD"}}}
```

Replace the placeholders with the following values:

* `HOSTNAME`: **`gitamic.composer.sh`**
* `USERNAME`: Your Anystack email address
* `PASSWORD`: [Your license key](installation.md#anystack) (which depends on how you purchased it)

For compatibility, remove all spaces and line breaks.
{% endtab %}

{% tab title="Custom / Other" %}
Any of the following methods should work. **You only need to pick one.**

#### `auth.json`

You can create an `auth.json` file [in your project](https://getcomposer.org/doc/articles/authentication-for-private-packages.md#authentication-in-auth-json-per-project) or in [a global `auth.json`](https://getcomposer.org/doc/articles/authentication-for-private-packages.md#global-authentication-credentials) that stores these credentials.

{% hint style="danger" %}
**Do not commit your `auth.json` file to git**
{% endhint %}

#### `COMPOSER_AUTH`

Create a `COMPOSER_AUTH` environment variable similarly to the approach used for [#netlify](deployment.md#netlify "mention").

You can set this environment variable in your shell config file or you can create it on-the-fly as part of your `composer` CLI commands:

```bash
COMPOSER_AUTH={JSON} composer install ...
```

See the [#netlify](deployment.md#netlify "mention") example for what to replace the `{JSON}` placeholder with
{% endtab %}
{% endtabs %}

### Auto-deployment

If you're using Gitamic to `push` commits from a server that is also the target for automated deployments, when you `push` from Gitamic it might trigger a redundant deployment back to the environment that is the _source_ of those changes.

To prevent this, in your deployment script, you will need to write a statement that exits the deployment when it detects that Gitamic initiated the commit.

For example, if you use [Laravel Forge](https://forge.laravel.com/) (and you haven't customised the git commiter name - see [#2.-optional-set-the-git-committer](setup.md#2.-optional-set-the-git-committer "mention")), you could add the following to the beginning of your deploy script, which inspects the author of the commit and stops the process before it begins:

```bash
[[ "$FORGE_DEPLOY_AUTHOR" == "Gitamic" ]] && echo "Commit by $FORGE_DEPLOY_AUTHOR" && exit 0

# The rest of your deployment script...
```

However, the specific approach you should use will depend on your unique setup.

[^1]: Continuous Integration
