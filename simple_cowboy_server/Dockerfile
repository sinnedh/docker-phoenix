FROM msaraiva/elixir-dev:latest

EXPOSE 4000

ADD hello_phoenix .

RUN mix deps.get
RUN mix compile
RUN mix phoenix.digest

CMD mix phoenix.server
