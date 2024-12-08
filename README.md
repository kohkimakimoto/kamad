# Kamad

Kamad (short for Kamal in Docker) is a wrapper script for [Kamal](https://kamal-deploy.org/). It runs Kamal by in a Docker container.

## Why Use Kamad?

[Kamal](https://github.com/basecamp) is a tool for deploying web applications anywhere developed by [Basecamp](https://github.com/basecamp).
It can be installed as a Ruby gem. Basecamp also provides an official Docker image and [instructions](https://kamal-deploy.org/docs/installation/) for using the dockerized version via a shell alias like the following:

```sh
alias kamal='docker run -it --rm -v "${PWD}:/workdir" -v "/run/host-services/ssh-auth.sock:/run/host-services/ssh-auth.sock" -e SSH_AUTH_SOCK="/run/host-services/ssh-auth.sock" -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/basecamp/kamal:latest'
```

While this approach is simple to set up and works well, the Dockerized version of Kamal has minor issues due to running Kamal in an isolated Docker container.

- You cannot deploy an application from a subdirectory: https://github.com/basecamp/kamal/issues/799
- You cannot use secrets that are provided by environment variables: https://github.com/basecamp/kamal/issues/1258

Kamad solves these problems by providing customization options for running Kamal in a Docker container.

## Installation

Kamad is a simple, single-file Bash script.
You can download the [`kamad`](https://github.com/kohkimakimoto/kamad/raw/main/kamad) file from the repository and make the file executable.

## Usage

Kamad can be used in the same way as Kamal, making it a drop-in replacement. For example, if you use the `kamal` command like this:

```sh
kamal deploy
```

You can simply use the `kamad` command like this:

```sh
kamad deploy
```

### Deploy an application from a subdirectory

Kamad provides the `-W|--kamal-workdir` option. So you can deploy an application from a subdirectory with this option.

```sh
kamad -W path/to/app deploy
```

### Use secrets that are provided by environment variables

Kamad provides the `-e|--env` option. So you can use the environment variables as secret values.

```sh
kamad -e KAMAL_REGISTRY_PASSWORD deploy
```

## Author

Kohki Makimoto <kohki.makimoto@gmail.com>

## License

The MIT License (MIT)
