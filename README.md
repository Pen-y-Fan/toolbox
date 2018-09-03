# Toolbox

[![Build Status](https://travis-ci.com/jakzal/toolbox.svg?branch=master)](https://travis-ci.com/jakzal/toolbox)
[![Build Status](https://scrutinizer-ci.com/g/jakzal/toolbox/badges/build.png?b=master)](https://scrutinizer-ci.com/g/jakzal/toolbox/build-status/master)

Helps to discover and install tools.

## Use cases

Toolbox [started its life](https://github.com/jakzal/phpqa/blob/49482ae447d4b6341cf77aac9d51390fe1176e8c/tools.php)
as a simple script in the [phpqa docker image](https://github.com/jakzal/phpqa).
Its purpose was to install set of tools while building the image.
It has been extracted as a separate project to make maintenance easier and open itself for new use cases.

## Installation

Get the `toolbox.phar` from the [latest release](https://github.com/jakzal/toolbox/releases/latest).
The command below should do the job:

```bash
curl -s https://api.github.com/repos/jakzal/toolbox/releases/latest \
  | grep "browser_download_url.*toolbox.phar" \
  | cut -d '"' -f 4 \
  | xargs curl -Ls -o toolbox \
  && chmod +x toolbox
```

## Usage

### List available tools

```
./toolbox list-tools
```

### Install tools

```
./toolbox install
```

#### Dry run

To only see what commands would be executed, use the dry run mode:

```
./toolbox install --dry-run
```

### Test if installed tools are usable

```
./toolbox test
```

#### Dry run

To only see what commands would be executed, use the dry run mode:

```
./toolbox test --dry-run
```

### Tools definitions

By default `resources/pre-installation.json` and `resources/tools.json` are used to load tool definitions.
Definitions can be loaded from customised files by passing the `--tools` option(s):

```
./toolbox list-tools --tools path/to/file1.json --tools path/to/file2.json
```

Tool definition location(s) can be also specified with the `TOOLBOX_JSON` environment variable:

```
TOOLBOX_JSON='path/to/file1.json,path/to/file2.json' ./toolbox list-tools
```