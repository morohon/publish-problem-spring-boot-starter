# publish problem

The repository shows an error when generating a metadata file using the maven-publish plugin when the dependencies 
do not have the specified versions.
To reproduce the error, you must do the following:
1. Switch to the main branch: `git checkout main`
2. Run the command:
```shell
./gradlew publish-problem-spring-boot-autoconfigure:clean publish-problem-spring-boot-autoconfigure:generateMetadataFileForStarterPublication
```
3. See an error like this in the execution log:
<pre>
* What went wrong:
   Execution failed for task ':publish-problem-spring-boot-autoconfigure:generateMetadataFileForStarterPublication'.
   > Invalid publication 'starter':
   - Publication only contains dependencies and/or constraints without a version. You need to add minimal version information, publish resolved versions (For more on this, please refer to https://docs.gradle.org/8.6/userguide/publishing_maven.html#publishing_maven:resolved_dependencies in the Gradle documentation.) or reference a platform (For more platforms, please refer to https://docs.gradle.org/8.6/userguide/platforms.html in the Gradle documentation.)
</pre>
The error occurs because maven-publish cannot determine the version of the dependencies specified in 
the publish-problem-spring-boot-autoconfigure module. Dependency versions are set using the
spring dependency management gradle plugin declared according to the [spring documentation](https://docs.spring.io/spring-boot/docs/current/gradle-plugin/reference/htmlsingle/#managing-dependencies.dependency-management-plugin.using-in-isolation).

To fix the error, just specify the versions in the [build.gradle.kts](publish-problem-spring-boot-autoconfigure/build.gradle.kts).
The scenario in which the metadata file is successfully generated:
1. Switch to branch: `git checkout fix-publish`
2. Run the command: 
```shell
./gradlew publish-problem-spring-boot-autoconfigure:clean publish-problem-spring-boot-autoconfigure:generateMetadataFileForStarterPublication
```
3. See the successful execution of the command in the log