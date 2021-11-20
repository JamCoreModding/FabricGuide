---
description: Using GitHub Actions to automate repetitive tasks and check for errors
---

# GitHub Actions

[GitHub Actions](https://github.com/features/actions) can be used to perform tasks when a chosen trigger happens (e.g. pushes, pull requests, issue comments).

### Creating an Error Checker

The simplest action you can create to get started is an error checker that builds your mod when it is pushed.

To get started, create a file in `.github/workflows` called `error_checker.yml`. Actions are created using YAML - if you are unfamiliar with it's syntax you can use [this ](https://learnxinyminutes.com/docs/yaml/)webpage to get started.

Within the action file, we write the following:

{% code title="error_checker.yml" %}
```yaml
name: Build
on: [push, pull_request]

jobs:
  build:
      matrix:
        java: [
            17
        ]
        os: [ ubuntu-20.04 ]
    runs-on: ${{ matrix.os }}
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2

      - name: Validate Gradle Wrapper
        uses: gradle/wrapper-validation-action@v1

      - name: Setup JDK ${{ matrix.java }}
        uses: actions/setup-java@v1
        with:
          java-version: ${{ matrix.java }}

      - name: Make Gradle Wrapper Executable
        if: ${{ runner.os != 'Windows' }}
        run: chmod +x ./gradlew
        
      - name: Build
        run: ./gradlew build

      - name: Capture Build Artifacts
        uses: actions/upload-artifact@v2
        with:
          name: Artifacts
          path: build/libs/
```
{% endcode %}

This is the simplest form of action we can create to build our mod. Next, we will go through the file step-by-step to explain it:

`name: Build` sets the name of the task that appears on GitHub.

`on: [push, pull_request]` sets the triggers to run this workflow. You can find all the available triggers [here](https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows).

Next, we define a job for our workflow named `build`, it contains a matrix of Java versions and runner operating systems. If we wanted to also build on Windows and Java 17, we could add these to our matrix and the following jobs would be run:

* Build (Java 16, Ubuntu)
* Build (Java 16, Windows)
* Build (Java 17, Ubuntu)
* Build (Java 17, Windows)

You can define up to 255 combinations of parameters that can be run.

Next, we checkout the repository, validate our Gradle wrapper, setup Java and make `gradlew` exectuable using official actions provided by GitHub or Gradle. The ability to call other workflows from your workflow is one reason why actions are so powerful, there are thousands of premade workflows available on the GitHub marketplace.

After that, we run `.\gradlew build` just like we would on our local machine in the terminal, after all a workflow runner is simply a machine hosted by GitHub and we have access to it's terminal and file system.

Finally, we upload the produced artefacts from `build/libs` to the action so they can be accessed afterwards. If the mod fails to build, the workflow will fail and a red cross will appear next to the commit on GitHub.
