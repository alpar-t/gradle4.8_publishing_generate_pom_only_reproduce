# gradle4.8_publishing_generate_pom_only_reproduce

Reproduce [gradle/gradle#5696](https://github.com/gradle/gradle/issues/5696)

Generating the POM for publishing doesn't work as documented in neither Gradle 4.7 nor 4.8. 
The task is probably created late. 
With Gradle 4.8 using `tasks.withType` no longer works either. It seems there's no way to configure
this.

```
[:~/work/elastic/gradle4.8_publishing_generate_pom_only_reproduce] % sed  -i 's/4\.[0-9]/4.7/'  gradle/wrapper/gradle-wrapper.properties
[:~/work/elastic/gradle4.8_publishing_generate_pom_only_reproduce] % ./gradlew clean generatePomFileForMavenJavaPublication
> Task :clean
> Task :generatePomFileForMavenJavaPublication

BUILD SUCCESSFUL in 0s
2 actionable tasks: 2 executed
[:~/work/elastic/gradle4.8_publishing_generate_pom_only_reproduce] % find -name *.pom -o -name *.xml
./build/test.pom
[:~/work/elastic/gradle4.8_publishing_generate_pom_only_reproduce] % sed  -i 's/4\.[0-9]/4.8/'  gradle/wrapper/gradle-wrapper.properties
[:~/work/elastic/gradle4.8_publishing_generate_pom_only_reproduce] % ./gradlew clean generatePomFileForMavenJavaPublication
> Task :clean
> Task :generatePomFileForMavenJavaPublication

Deprecated Gradle features were used in this build, making it incompatible with Gradle 5.0.
See https://docs.gradle.org/4.8/userguide/command_line_interface.html#sec:command_line_warnings

BUILD SUCCESSFUL in 0s
2 actionable tasks: 2 executed
[:~/work/elastic/gradle4.8_publishing_generate_pom_only_reproduce] % find -name *.pom -o -name *.xml
./build/publications/mavenJava/pom-default.xml
```
