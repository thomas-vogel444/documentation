# Docker Run vs CMD vs ENTRYPOINT
from https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/

- RUN
    - executes commands in a new layer and creates a new image
    - e.g. installing software
- CMD
    - sets default command and/or parameters which can be overwritten from the command line when docker container runs
    - choose it to 
        - provide extra parameters to ENTRYPOINT
        - provide a default command and/or arguments that can be overwritten from command line 
    - has 3 forms
        - CMD ["executable", "param1", "param2, ...]
        - CMD ["param1", "param2, ...]
            - sets additional default parameters for ENTRYPOINT in exec form
            - this is used in conjunction with ENTRYPOINT
        - CMD command param1 param2 ...
- ENTRYPOINT
    - configures a container that will run as an executable
    - the command is always executed

2 forms
- Shell form
    - <instruction> <command>
    - e.g. 
        RUN apt-get install python3
        CMD echo "Hello world"
        ENTRYPOINT echo "Hello world"
    - calls /bin/sh <command> => will substitue variables
- Exec form
    - <instruction> ["executable", "param1", "param2, ...]
    - e.g. 
        RUN ["apt-get", "install" "python3"]
        CMD ["echo", "Hello world"]
        ENTRYPOINT ["echo", "Hello world"]
    - calls the executables directly => will NOT substitue variables