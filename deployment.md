# 🛳 Deployment

### Authentication

When building your application in its production environment or running it through a CI[^1] pipeline, you will likely need to install its dependencies, and this may include Gitamic.

When that happens, Composer will need to authenticate

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
