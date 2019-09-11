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

