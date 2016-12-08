FROM msaraiva/elixir-dev:latest

ENV MIX_ENV prod
ENV PORT 80

EXPOSE $PORT

RUN mkdir /app
WORKDIR /app

ADD hello_phoenix .
RUN mix deps.get --only prod
RUN mix compile
RUN mix phoenix.digest
RUN mix release

ENTRYPOINT ["rel/hello_phoenix/bin/hello_phoenix"]
CMD ["foreground"]
