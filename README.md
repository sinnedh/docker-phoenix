# Creating Elixir Phoenix Releases in Docker Container

There are several approaches to run a Phoenix Application within a Docker container:
 1. Default mix development server `mix phoenix.server`
 2. Elixir Release Manager `exrm`
 3. The successor of `exrm` named `distillery`

The Docker images are using [Alpine](https://alpinelinux.org/) lightweight Linux
distribution and are based on the [images from msaraiva](https://github.com/msaraiva/docker-alpine).

The repo contains the source code and the `Dockerfile` for these three
solutions apllied to the default HelloPhoenix demo application from the
[Up And Running Guide](http://www.phoenixframework.org/docs/up-and-running).


##  Using the default mix development server
This is the simplest approach for housing a Phoenix application in a Docker
container. It just uses the [Cowboy HTTP server](https://github.com/ninenines/cowboy)
that is started when running the command `mix phoenix.server`. This is an easy
solution which is applicable for development but it should not be used in a
production environment. It is described in the [Phoenix Docs](http://www.phoenixframework.org/docs/deployment).

The required steps are as follows:
 1. `mix phoenix.new hello_phoenix --no-brunch --no-ecto`
 2. `docker build -t simple_cowboy_server .`
 3. `docker run --rm -p 4000:4000 simple_cowboy_server`


## Advanced deployment using the Elixir Release Manager (exrm)
The [Elixir Release Manager](https://github.com/bitwalker/exrm) creates a compiled 
stand-alone bundle of the application so distributing the source code to the
production server can be avoided. The system parameters for build system should
be identical to the production system. This can be easily accomplished by
utilizing docker containers.

These are the required steps:
 1. `mix phoenix.new hello_phoenix --no-brunch --no-ecto`
 2. Add `{:exrm, "~> x.x.x"}` to the deps in `mix.exs`
 3. Define which servers are started for which endpoints in `config/$MIX_ENV.exs`, e.g. `config :hello_phoenix, HelloPhoenix.Endpoint, server: true`
 4. Create docker image: `docker build -t advanced_deployment_with_exrm .`
 5. Start docker image on production port 80: `docker run --rm -p 80:80 advanced_deployment_with_exrm`

In this example the building happens in the image where also the server is
running. As a consequence the source code is also shipped in the docker
container to the production envirnoment. To avoid this, either remove
everything except the `rel` directory or create a separate container for
building.


## Advanced deployment using Distillery
Exrm will be replaced by [Distillery](https://github.com/bitwalker/distillery) soon.

Description will follow soon.

