---
description: To distribute your mod to end users, you must first build it
---

# Building Your Mod

In order to distribute your mod, you need to build it.

First, make sure the version listed in `gradle.properties` is correct. For example:

{% code title="gradle.properties" %}
```properties
[...]
mod_version=1.2.4
[...]
```
{% endcode %}

Your mod versioning should follow [semantic versioning](https://semver.org)

Next, go to a terminal within your mods folder and run the command:

`.\gradlew build`

Once that command has completed, you can find the build `.jar` files in `build/libs`, the file that should be distributed to users is the file that does not have any extensions. For example:

* \<modid>-\<version>.jar
* \<modid>-\<version>-dev.jar
* \<modid>-\<version>-sources.jar
* \<modid>-\<version>-sources-dev.jar

The JAR file you use is the first one on that list.
