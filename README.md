# circleci-template
This is a sample project to show how to grab a value from a file in your repository, and then set it as an environment variable. 

## Setup

You will need to do the following:

1. Create a config.yml file containing a setup workflow
2. Create a continuation config file (continuation-config.yml)
3. Enable the `Enable dynamic config using setup workflows` setting under Advanced Settings on your project's settings page

The sample config.yml in this repository can most likely be used as-is, but please update the filename referenced in the example if needed.

Secondly, if you are adapting a previous project, you can use your current config.yml file, but you will need to rename it `continuation-config.yml` or whatever name you specify for the `configuration_path` parameter in config.yml.
Then you would need to add the following to the top of your new continuation-config.yml file:

```
parameters:
  build-version:
    type: string
    default: ""
```

After that, you will be able to access the value of `build-version` anywhere in your config with the following syntax:

```
<< pipeline.parameters.build-version >>
```
Here is an example:

```
  job-1:
    executor:
      name: win/default
      size: "medium"
    environment:
      BUILD_VERSION: << pipeline.parameters.build-version >>
    steps:
      - checkout
      - run:
          name: Check value of sample variable
          shell: bash.exe
          command: echo $BUILD_VERSION
```
