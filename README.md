# simple-flank
simple-flank is a Gradle plugin to use Flank in Android projects with no configuration needed

Applied to any application or library module it creates a task called `runFlank` that will run all the android tests (all flavors, debug buildType by default)

Tests will be executed using NexusLowRes emulators, and the lower sdk possible (between minSdk and available SDKs at Firebase)

# Setup

Apply the plugin on the application/library modules you want to run tests:
```
plugins {
  ...
  id("simple-flank")
}
```

add your firebase credentials to the rootroject as `ftl-credentials.json`

That's it, run `./gradlew runFlank` and get the results.

# Optional configuration

## Changing the buildType to run

Android already provides a way for you to do it:
```
android {
  ...
  testBuildType = "beta"
  ...
}
```

## Changing the credentials file

```
simpleFlank {
  credentialsFile.set(project.rootProject.file("some-credentials.json"))
}
```

## Making the tests cacheable

If you are using the Gradle BuildCache, you just need to declare your tests as hermetic ( isolated and reproducible )

```
simpleFlank {
  hermetic.set(true)
}
```

