**This is created follow by the tutorial of "Hello World GitHub Actions"**

This contains a shell script named `entrypoint.sh` which will print out the message of "Hello world my name is *$INPUT_MY_NAME*", *$INPUT_MY_NAME* will replace with the values that assigned to it.

This also contain a Dockerfile. The `entrypoint.sh` script will be run in Docker, and it will define what the action is really going to be doing.:

```dockerfile
FROM debian:9.5-slim  #Describes which mirror implementation is based on

ADD entrypoint.sh /entrypoint.sh  #Copies everything from entrypoint.sh and adds to the filesystem of the image
RUN chmod +x /entrypoint.sh  #run the command 
ENTRYPOINT ["/entrypoint.sh"]
```



This also have a yaml file named `main.yml` in **.github/workflows**

```yaml
name: A workflow for my Hello World file
on: push #This indicates it is triggered when the code is pushed to any branch in the repository

jobs:
  build:
    name: Hello world action
    runs-on: ubuntu-latest  #Indicates the type of machine to run the job on.
    steps:  #sequence of tasks should be done 
      - uses: actions/checkout@v1 #clone the source code of the repository into the workflow.
      - uses: ./action-a
        with:
          MY_NAME: "Mona"  #Defines the input parameter(MY_NAME), it will be passed to the INPUT_MY_NAME variable of entrypoint.sh 
```

So in this case, the output will be "Hello world my name is Mona"