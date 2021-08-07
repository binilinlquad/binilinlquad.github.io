---
layout: default
title: DRY Declare Artifacts Repository in Gradle
---
*What is Gradle*
Quoted [Gradle website](https://docs.gradle.org/current/userguide/what_is_gradle.html):
```
Gradle is an open-source build automation tool that is designed to be flexible enough to build almost any type of software
```
Gradle is de facto main tool to build Android Project where I spent lot of my time.

*What is Artifacts Repository*
The repository in this writing specifically means artifact repository, source where build tool get artifacts needed to build. It can be local or remote. MavenCentral is one of popular artifact repository.

*Declare Artifacts Repository*
Declaring artifacts Repository fairly easy. Look for `repository` block. It is usually resides in `build.gradle`. If it not found, then we can add it by ourselves directly.
Gradle has provides several default artifacts repository, such as Maven Central and Google Maven.
```
repositories {
    mavenCentral()
    google()
}
```

Now, Gradle will aware those two artifacts repository. For more detail, nothing can beat [reference](https://docs.gradle.org/current/userguide/declaring_repositories.html) in Gradle website.

*Declare Custom Repository*
There are several reasons why we want to use custom repository:
- It is not release artifact or not public consumption
- Gradle not provides the artifacts repository by default
- Security, need to be authenticated
- Host your own artifact repository
- etc

Declaring custom repository is as easy as declare Maven Central or Google Maven. Add `maven` inside `repository`.
For example adding maven repository which point to (fake) `https://mymaven.artifact/release` will look like this:
```
repositories {
    mavenCentral()
    google()
    maven {
       url 'https://mymaven.artifact/release'
    }
}
```

*Why DRY*
The title of this blog add DRY. If it is very easy to declare artifact repository, why do we need to DRY?
Image this scenario, you have multiple modules and you want to add each module artifact repository A. We can copy paste artifact repository A to each module's `build.gradle`. It is easy, but doing it for each module is not fun.

On top of the article, Gradle states itself as build automation tool. Even though Gradle has provides lot of default extension that just works, it cannot cover all of it. For this, Gradle give its users capability to [create their own plugin](https://docs.gradle.org/current/userguide/custom_plugins.html). This blog shows how to create plugin using Build script.

*Create custom plugin*
First implement Plugin interface and save it as `custom-repo-declarator.gradle` in root project.
```
class CustomRepoDeclarator implements Plugin<Project> {

    @Override
    void apply(Project target) {
      // we will implement add custom repository A to each module repository here
    }
}
```

`target` is project where we apply this plugin. If we apply this plugin inside `buildScript` in root project `build.gradle` then it will point to root project.

Because we want to declare repository to all modules, or root and child projects, we need to iterate all project. We can do it by invoke allProject pass closure as parameter.
```
target.allProjects {
    // we can access project and repository inside this closure
}
```

To declare custom maven, we need declare it inside `target.allProjects` above. 
```
target.allProjects {
    repositories.maven {
        url "A-repository-url-here"
    }
}
```

And if repository is needed by build script, we can add it too
```
target.allProjects {
    repositories.maven {
        url "A-repository-url-here"
    }
    
    project.buildScript {
        repositories.maven {
            url "A-repository-url-here"
        }
    }
}
```

To use custom plugin that we created, apply it in root `build.gradle`. It will look like below.
```
buildScript {
    apply from: './custom-repo-declarator.gradle'
}
```

*Conclusion*
Declare repository is very easy to be done. Any capability that not provided by default, can be easily add using custom plugin.

