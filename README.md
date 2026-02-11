# Dataset registry

Here we register private datasets published in [harbor](harborframework.com) format on GitHub: https://github.com/innodata-datasets

## Adding or modyfying a dataset

Edit [registry.json]

## Using a private dataset with `harbor`

Harbor uses `git clone` command to get the datasets, using URLs listed in the [registry.json].

To make `git clone` work with private datasets, one needs to enable `GIT_ASKPASS` mechanism (for headless access to secret tokens).

### Enabling GIT_ASKPASS

One-time task

Create following script:
```bash
/bin/bash
exho "GITHUB_TOKEN"
```

Place it where you want, say `~/.local/bin/gitpass.sh`

Make sure it is executable:

```bash
chmod +x ~/.local/bin/gitpass.sh`
```

Finally, tell `git` to use it for authentication

```bash
export GIT_ASKPASS=~/.local/bin/gitpass.sh
```

### Obtain GitHub access token

See https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens

## Running `harbor` 

Instead of usual

```bash
harbor run ...
```

do this:

```bash
GITHUB_TOKEN=<your_github_token> harbor run ...
```

## Using this registry with `harbor`

Finally, you need to direct `harbor` to use this dataset registry (instead of the default one). For that use `--registry-url` flag.
Overall, this is the receipe:

```bash
GITHUB_TOKEN=<your_github_token> \
harbor run ---registry-url https://raw.githubusercontent.com/innodata-datasets/registry/refs/heads/master/registry.json \
-d agentic-gym  # or other dataset \
-a <agent> \
-m <model>
```

