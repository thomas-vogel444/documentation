# ENV VS ARG

From https://vsupalov.com/docker-arg-vs-env/

Note that the `docker build` output leaves the referenced `ENV` and `ARG` unresolved despite actually resolving them in the actualbuild.

Differences:
- ENV
    - for future running containers
    - Used for providing default values for your future environment variables
    - Great way to pass configuration values
    - Cannot be changed at build time
- ARG 
    - for building your Docker image
    - Can be changed by providing a `build-arg VAR_NAME=6` argument at build time.

