# Glow - Git-Flow (for Gitlab)

You can use this tool in any git project of course. But there are some commands which are bound to the gitlab api. So therefore i promote this as a tool tailored for gitlab.

## Installation

Here you can find all [available Binaries](https://github.com/meinto/glow/releases).

## Workflow

> Important!  
> Some commands need additional information like git author or gitlab namespace and project name.  
> These Informations can be stored in a config file or can be passed through flags.

![glow workflow](./glow.jpg?raw=true)

### Feature Development

The following command will create a new feature branch in the following form: `features/dvader/death-star`. The name of the author (`dvader`) is grabbed from the config file.

```bash
# author grabbed from config
glow feature death-star
```

After you created the feature branch it is automatically checked out.  
When you finish your feature you can create a merge request in gitlab:

```bash
# gitlab information grabbed from config
glow close
```

### Create a release

I recommend to use [Semver](https://semver.org/) for versioning. The following command will create a release branch with the following format: `release/v1.2.3`.

```bash
glow release 1.2.3
```

### Publish a release

When you decide that the release is stable and you want to publish it, the following command will create a merge request on the `master` branch in gitlab.

```bash
glow publish
```

### Close a release

After publishing the release, you have to merge all changes made on the release branch back into `develop`. The following command creates a merge request of the release branch into `develop`.

```bash
glow close
```

## Commands

```bash
# feature
glow feature <name-of-the-feature> \ 
  --author <name-of-the-author> # optional when using config file

# release
glow release <version> \ 
  --postRelease <name-of-script> # optional

# merge request
glow mergeRequest <source-branch> <target-branch> \
  -e <gitlabEndpoint> \     # optional when using config file
  -n <projectNamespace> \   # optional when using config file
  -p <projectName> \        # optional when using config file
  -t <gitlabCIToken>        # optional when using config file

# publish
glow publish \
  -e <gitlabEndpoint> \     # optional when using config file
  -n <projectNamespace> \   # optional when using config file
  -p <projectName> \        # optional when using config file
  -t <gitlabCIToken>        # optional when using config file

# finish release
glow close \
  -e <gitlabEndpoint> \     # optional when using config file
  -n <projectNamespace> \   # optional when using config file
  -p <projectName> \        # optional when using config file
  -t <gitlabCIToken>        # optional when using config file
```

## Config

For some commands you must provide information like the url of your gitlab instance or your gitlab ci token. These informations can be put in a `glow.json` file. Glow will lookup this json in the directory where its executed.

**List of all config params**

```json
{
  "author": "dvadar",
  "gitlabEndpoint": "https://gitlab.com",
  "projectNamespace": "my-namespace",
  "projectName": "my-project",
  "gitlabCIToken": "abc",
}
```