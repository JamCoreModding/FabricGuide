---
description: Using JitPack to make your mod or library available for other developers
---

# JitPack

JitPack.io allows you to serve your mod to other developers who can add it as a Gradle dependency without having to setup your own Maven repository.

### Publishing Your Mod Via JitPack

First, we must create a config file for JitPack in the root of our GitHub repository.&#x20;

Create a file called `jitpack.yml` with the following contents:

{% code title="jitpack.yml" %}
```yaml
before_install:
  - export SDKMAN_DIR="/home/jitpack/sdkman" && curl -s "https://get.sdkman.io" | bash
  - source "/home/jitpack/sdkman/bin/sdkman-init.sh"
  - sdk install java 16.0.1.hs-adpt
  - sdk use java 16.0.1.hs-adpt
```
{% endcode %}

This file is read by JitPack when a build is requested and used to configure the build. JitPack does not yet officially support Java 16/17, so we must manually install it using this script.

Now, to add your mod as a dependency via Gradle, add it in your build script:

{% code title="build.gradle" %}
```groovy
[...]

repositories {
    [...]
    maven { url 'https://jitpack.io' }
}

[...]

dependencies {
    modImplementation 'com.github.<username>:<repo name>:<tag>'
    
    // For Example:
    modImplementation 'com.github.JamCoreModding:LIbJam:main-SNAPSHOT'
    // You could also use modApi depending on your usecase
}
```
{% endcode %}

The `<tag>` component of the dependency can be:

* A commit hash
* A branch + `-SNAPSHOT` (e.g. `main-SNAPSHOT`) to build the latest version of a branch
* A GitHub release
* A Git tag

You can find your repository using the search bar at[ jitpack.io](https://jitpack.io), you can then see the tags you have available
