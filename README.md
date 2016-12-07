# Creating Elixir Phoenix Releases in Docker Container

There are several approaches to run a Phoenix Application within a Docker container:
 1. Default mix development server `mix phoenix.server`
 2. Elixir Release Manager `exrm`
 3. The successor of `exrm` named `distillery`

The Docker images are using [Alpine](https://alpinelinux.org/) lightweight Linux
distribution and are based on the [images from msaraiva](https://github.com/msaraiva/docker-alpine).


##  Using the default mix development server
This is the simplest approach for housing a Phoenix application in a Docker
container. It just uses the [Cowboy HTTP server](https://github.com/ninenines/cowboy)
that is started when running the command `mix phoenix.server`. This is an easy
solution which is applicable for development but it should not be used in a
production environment. It is described in the [Phoenix Docs](http://www.phoenixframework.org/docs/deployment).

Create the HelloPhoenix demo application from the [Up And Running Guide](http://www.phoenixframework.org/docs/up-and-running):
 1. `mix phoenix.new hello_phoenix --no-brunch --no-ecto`
 2. `docker build -t simple_cowboy_server .`
 3. `docker run --rm -p 4000:4000 simple_cowboy_server`
