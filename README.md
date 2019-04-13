[![Build Status](https://travis-ci.com/philips-software/code-maat.svg?branch=master)](https://travis-ci.com/philips-software/code-maat)
[![Slack](https://philips-software-slackin.now.sh/badge.svg)](https://philips-software-slackin.now.sh)

# Code-maat Docker images

This repo will contain code-maat docker images

Current versions available:
```
.
├── 1.0
│   └── alpine
│       └── Dockerfile
```
## Usage

Images can be found on [https://hub.docker.com/r/philipssoftware/code-maat/](https://hub.docker.com/r/philipssoftware/code-maat/).
```
docker run --rm philipssoftware/code-maat -h
```

### Example getting Churn for project

```
git log --all --numstat --date=short --pretty=format:'--%h--%ad--%aN' --no-renames --after=2019-04-01 > codemaat.txt
docker run -v $(pwd):/data --rm philipssoftware/code-maat -l /data/codemaat.txt -c git2 -a abs-churn
```

## Content

The images obviously contain code-maat, but also two other files:
- `REPO`
- `TAGS`

### REPO

This file has a url to the REPO with specific commit-sha of the build.
Example:

```
$ docker run philipssoftware/code-maat cat REPO
https://github.com/philips-software/code-maat/tree/facb2271e5a563e5d6f65ca3f475cefac37b8b6c
```

### TAGS

This contains all the similar tags at the point of creation.

```
$ docker run philipssoftware/code-maat cat TAGS
code-maat code-maat:1 code-maat:1.0 code-maat:1.0.1 code-maat:1.0.1-alpine
```

You can use this to pin down a version of the container from an existing development build for production. When using `code-maat:1` for development. This ensures that you've got all security updates in your build. If you want to pin the version of your image down for production, you can use this file inside of the container to look for the most specific tag, the last one.


## Simple Tags

### code-maat
- `code-maat`, `code-maat:1`, `code-maat:1.0`, `code-maat:1.0.2`, `code-maat:1.0.2-alpine` [1.0/alpine/Dockerfile](1.0/alpine/Dockerfile)

- `code-maat:1.0.1`, `code-maat:1.0.1-alpine` refering to code-maat:v1.0.1 

## Why?

> Why do we have our own docker image definitions?

We often need some tools in a container for checking some things. F.e. [jq](https://stedolan.github.io/jq/) and [curl](https://curl.haxx.se/).
We can install this every time we need a container, but having this baked into a container seems a better approach.

For Code-maat there is no official docker image. We can build it ourselves, but having it versioned in a pipeline is always better. We strive for immutable builds.

That's why we want our own docker file definitions.

## Issues

- If you have an issue: report it on the [issue tracker](https://github.com/philips-software/code-maat/issues)

## Author

- Jeroen Knoops <jeroen.knoops@philips.com>
- Heijden, Remco van der <remco.van.der.heijden@philips.com>

## License

License is MIT. See [LICENSE file](LICENSE.md)

## Philips Forest

This module is part of the Philips Forest.

```
                                                     ___                   _
                                                    / __\__  _ __ ___  ___| |_
                                                   / _\/ _ \| '__/ _ \/ __| __|
                                                  / / | (_) | | |  __/\__ \ |_
                                                  \/   \___/|_|  \___||___/\__|  

                                                                 Infrastructure
```

Talk to the forestkeepers in the `docker-images`-channel on Slack.

[![Slack](https://philips-software-slackin.now.sh/badge.svg)](https://philips-software-slackin.now.sh)
