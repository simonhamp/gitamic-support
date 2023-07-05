---
description: Gitamic is installed via Composer.
---

# 💾 Installation

Before you install Gitamic, make sure your system and application meets the [#requirements](./#requirements "mention").

### Composer

To install Gitamic, you must use [Composer.](https://getcomposer.org/)

Gitamic is not available on the public Composer package repository Packagist, so to install Gitamic, we must first tell Composer how to find it.

To do that, you must add the private repository URL to the `repositories` array in your `composer.json`:

```json
"repositories": [
  {
    "type": "composer",
    "url": "https://gitamic.composer.sh"
  }
],
```

Then, you can install the package via Composer as you'd expect:

```bash
composer require simonhamp/gitamic
```

The first time you run this, you'll be prompted to authenticate against the private package repository:

```bash
Loading composer repositories with package information
Authentication required (gitamic.composer.sh):
  Username: 
  Password: 
```

The authentication details will depend on where you purchased your license:

{% tabs %}
{% tab title="Anystack" %}
* **`Username`**: Your Anystack account email address.
* **`Password`**: Your [license key](https://account.anystack.sh/licenses) followed by a colon `:` and the domain name you entered when activating your license.\
  \
  For example: `9227fd74-ed29-4d1a-ad75-0bc41bea16a9:abc-widgets.com`

{% hint style="danger" %}
**Don't forget to activate your license first!**
{% endhint %}
{% endtab %}

{% tab title="Statamic Marketplace" %}
Your Statamic Marketplace license for Gitamic has been migrated to [Anystack](https://anystack.sh/).

You should have received an email encouraging you to [sign up for an Anystack Customer account](https://auth.anystack.sh/register?accountType=customer).

Your license key is associated with the email address you originally used to purchase Gitamic from the Statamic Marketplace. To retrieve it, please register with Anystack using the same email address

* **`Username`**: Your Anystack account email address
* **`Password`**: Your license key is available in your [Anystack dashboard](https://account.anystack.sh/licenses)

{% hint style="info" %}
There is no need to activate your license code
{% endhint %}

{% hint style="success" %}
**All Statamic Marketplace licenses have been upgraded to Gitamic Pro!**\
\
[Make sure you change your `config/statamic/editions.php`](setup.md#1.-register-the-add-on-within-statamic)
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Your Anystack email address cannot be changed.** If you cannot remember your license key and no longer have access to that email account, you will need to purchase another license
{% endhint %}

{% hint style="success" %}
Consider saving these details to your `auth.json` file so that you don't need to enter them every time you run a `composer install` or `composer update`
{% endhint %}
