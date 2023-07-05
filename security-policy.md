---
description: What to do if you become aware of a vulnerability exposed by Gitamic.
---

# 🔐 Security Policy

### Reporting a Vulnerability

**❗️ PLEASE SEND REPORTS TO** [**gitamic@simonhamp.me**](mailto:gitamic@simonhamp.me) **WITH THE SUBJECT LINE `Gitamic Security`**

**🛑 DO NOT REPORT SECURITY VULNERABILITIES AS ISSUES ON GITHUB**

Please **do not** share your discovery on Twitter, Discord or in any other public forum, as this may result in it being exploited.

Each report **MUST** include:

* PHP version (e.g. `8.2.7`)\
  `php -v`
* Statamic version (e.g. `4.9.2`)\
  `php please -V`
* Laravel version (e.g. `10.14.1`)\
  `php artisan -V`
* Git version (e.g. `2.34.1`)\
  `git --version`

Besides this, please provide as much detail as possible to allow me to assess and reproduce the vulnerability.

All reports will be acknowledged within 48 hours of receipt.

Your report will either be `ACCEPTED` or `DECLINED`, and you will be notified of this decision by reply to your original email.

If your report is accepted, I will work on a fix and you will be notified via email once the fix has been released.

**Note that I will not respond to feature requests or bug reports at the above email address.** Please [report an issue](https://github.com/simonhamp/gitamic-support/issues) instead.

### Rewards

The first reporter of an accepted vulnerability report will receive a free Gitamic lifetime license **once the vulnerability has been mitigated**.

There is no cash alternative.

### Supported Versions

| Version | Supported            |
| ------- | -------------------- |
| > 1.0   | :white\_check\_mark: |
