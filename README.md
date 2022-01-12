# InstantiateErrorAGP
Sample repository which demonstrates linting issues with AGP >= 7.0.0

# Description
In the following scenario :

- An activity in a module A extends an activity in a module B
- The activity in the module B is an abstract class 
- The activity in the module B extends AppCompatActivity
- AGP version is >= 0
- Minify is enabled
- Java 11

The app:lintVitalRelease task will fail, saying that the activity in the module A should extend android.app.Activity.

The issue is not happening with 4.2.0 <= AGP <= 4.2.2 (checkout the git branch 4.2.2 to compare)

# Steps to reproduce
- Clone the repository
- Open a prompt and execute

```bash
./gradlew assembleRelease
```

The following error message should be displayed following *app:lintVitalRelease* :

```bash
> Task :app:lintVitalRelease FAILED
/Users/tboutin/AndroidStudioProjects/InstantiateErrorAGP/app/src/main/AndroidManifest.xml:13: Error: MainActivity must extend android.app.Activity [Instantiatable]
            android:name=".MainActivity"
                          ~~~~~~~~~~~~~

   Explanation for issues of type "Instantiatable":
   Activities, services, broadcast receivers etc. registered in the manifest
   file (or for custom views, in a layout file) must be "instantiatable" by
   the system, which means that the class must be public, it must have an
   empty public constructor, and if it's an inner class, it must be a static
   inner class.

1 errors, 0 warnings
Lint found fatal errors while assembling a release target.

To proceed, either fix the issues identified by lint, or modify your build script as follows:
...
android {
    lintOptions {
        checkReleaseBuilds false
        // Or, if you prefer, you can continue to check for errors in release builds,
        // but continue the build even when errors are found:
        abortOnError false
    }
}
...
```