# Velitask SDK

[Русский](README_ru.md)

Public SDK for developing plugins for [Velitask](https://velitask.com) — the video & telemetry synchronization tool. Build custom indicators, figures, and data sources for Velitask using Java 21 and JavaFX.

## Add to your plugin project

Add JitPack repository and the SDK dependency to your `build.gradle`:

```gradle
repositories {
    mavenCentral()
    maven { url 'https://jitpack.io' }
}

dependencies {
    compileOnly 'com.github.velitask:velitask-sdk:1.0.+'
}
```

For a specific version, replace `1.0.+` with a tag (e.g. `v1.0.43-beta`). All available versions are listed on the [Releases page](https://github.com/velitask/velitask-sdk/releases).

## Quick start

A working plugin template is available at [github.com/velitask/plugin-example](https://github.com/velitask/plugin-example):

```bash
git clone https://github.com/velitask/plugin-example
cd plugin-example
./gradlew jar
```

The resulting `build/libs/*.jar` can be placed in your Velitask plugins directory (`~/.velitask/plugins/`) and loaded by the application.

## Build a plugin from scratch

1. Create a Java 21 Gradle project.
2. Add the SDK dependency (see above).
3. Implement `com.velitask.sdk.IPlagin` and your indicators / figures / sources.
4. Define the entry point in your jar manifest:

   ```gradle
   jar {
       manifest {
           attributes(
               'Velitask-Plugin-Class': 'com.example.MyPlugin'
           )
       }
   }
   ```

5. `./gradlew jar` and copy the result to `~/.velitask/plugins/`.

## License

Distributed under the [Apache License 2.0](LICENSE).

The Apache License 2.0 covers the **public API** of this SDK (the `com.velitask.sdk.**` packages). Internal implementation classes that are bundled and obfuscated within the JAR (under non-public package names) remain proprietary and are not licensed for separate use, modification, or extraction.

## Issues and contributions

- Bug reports and feature requests: [GitHub Issues](https://github.com/velitask/velitask-sdk/issues).
- Pull requests are welcome for documentation, examples, and SDK improvements.
- The SDK source itself is maintained in a private repository; the binary releases are mirrored here.
