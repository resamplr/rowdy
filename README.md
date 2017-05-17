# rowdy

[Documentation](https://lawliet89.github.io/rowdy/)

A [Rocket](https://rocket.rs/) based JSON Web Token authentication server.

## Requirements

Rocket requires nightly Rust. You should probably install Rust with [rustup](https://www.rustup.rs/), then override the code directory to use nightly instead of stable. See
[installation instructions](https://rocket.rs/guide/getting-started/#installing-rust).

In particular, `rowdy` is currently targetted for `nightly-2017-05-03`.

## Testing

To separate the dependencies of the `library` part of the crate from the `binary` part, the crate is set up
to make use of [workspaces](http://doc.crates.io/manifest.html#the-workspace--field-optional).

To run tests on both the `libary` and `binary`, do `cargo test --all`.

## Docker Image

An musl-linked image can be built from the `Dockerfile` in the repository root. You will need at least Docker 17.05
(API version 1.29) to build.

By default, the Docker image will not start Rowdy for you. You will need to provide your own configuration file
and command line arguments. The provided `docker-compose.yml` should get you started.

You can simply define your own `docker-compose.override.yml` file. For example:

```yaml
version: "2.1"
services:
  rowdy:
    environment:
      ROCKET_ENV: production
    expose:
      - "80"
    volumes:
      - ./config:/app/config
    command: [rowdy-cli, csv, config/Config.json]
networks:
  nginx:
    external: true

```

Then, you can simply start the containers with `docker-compose up --build -d`.
