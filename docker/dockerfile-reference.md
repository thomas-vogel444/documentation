# Dockerfile reference

From https://docs.docker.com/engine/reference/builder/

## Building Dockerfiles

- `docker build PATH | URL` creates an automated build from a Dockerfile using the `PATH` or `URL` as context.
    - The `PATH` is a directory on your local filesystem.
    - The `URL` is a Git repository location.

- The CLI transfers the entire content in `PATH` to the Docker daemon for building the image.
    - Best to
        - start with an empty directory
        - keep your Dockerfile there
        - Add only the files needed for building the Dockerfile
    - Add files and directories to exclude by adding a `.dockerignore` file
- options
    - `-f` for specifying a different Dockerfile
    - `-t` for tagging the image

## Environment replacement

Environment Variables can (set by `ENV`) be used as variables for certain instructions.
- use the notation `$variable_name` or `${variable_name}`
- Some `bash` modifiers can be used:
    - `{variable:-word}`: if `variable` is set then the result will be that value, otherwise it will be `word`.
    - `{variable:+word}`: if `variable` is set then the `word` will be the result, otherwise it will be the empty string.
- Environment variables are supported by the following list of instructions:
    - ADD
    - COPY
    - ENV
    - EXPOSE
    - FROM
    - LABEL
    - STOPSIGNAL
    - USER
    - VOLUME
    - WORKDIR
    - ONBUILD (when combined with one of the supported instructions above)

## COPY vs ADD

Always use `COPY` except when you want to use `ADD`'s auto-extraction of tar files.

For copying files from a URI, use `wget` or `curl` instead of `ADD` for efficiency purposes.

## .dockerignore

Excludes files and directories in the context matching patterns in the `.dockerignore` file.

This prevents unnecessary files being added to the image.

## FROM

You can have multiple `FROM`.

Interaction between `ARG` and `FROM`
- `ARG` set before `FROM` can have a value and only works until the first `FROM` is reached.
- To use the `ARG` value declared before a `FROM`, use an `ARG` instruction without a value inside of a build stage.

e.g.
```dockerfile
ARG VERSION=latest
FROM busybox:$VERSION
ARG VERSION
RUN echo $VERSION > image_version
```

## RUN

The `RUN` instruction executes any command in a new layer on top of the current layer and commit the results.

2 forms
- shell form (executed by the shell, by default `/bin/sh -c`)
    - `RUN <command>`
- exec form
    - `RUN ["executable", "param1", "param2", ...]`

## Exec form VS Shell form

- shell form (executed by the shell, by default `/bin/sh -c`)
    - `RUN|CMD|ENTRYPOINT <command>`
    - Enables substitution of environment variables
    - The shell is sent Unix signals, not the executable. 
        - The process is terminated forcefully if a SIGTERM to the shell is sent.
- exec form
    - `RUN|CMD|ENTRYPOINT ["executable", "param1", "param2", ...]`
    - Executable is called directly
    - When container is killed, the executable is sent the SIGTERM command. 
        - The process is terminated gracefully.
    - Parsed as a JSON array
        - use double quotes, not single quotes

## CMD

Main purpose: provide defaults for an executing container.

There can only be one CMD instruction in a docker file

3 forms:
- exec form (preferred)
    - `CMD ["executable", "param1", "param2", ...]`
- default parameters to `ENTRYPOINT`
    - `CMD ["param1", "param2", ...]`
    - Must specify `ENTRYPOINT`
- shell form
    - `CMD command param1 param2 ...`

## ENTRYPOINT

Main purpose: configuring a container as an executable.

Command line arguments to `docker run <image>` will be appended after all elements in an exec form.

You can override the entrypoint instruction using the `docker run --entrypoint` flag.
    - E.g. `docker run --entrypoint "ls" <image_name> <args>`

