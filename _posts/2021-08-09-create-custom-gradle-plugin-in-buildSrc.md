---
layout: post
title: Create Custom Gradle Plugin in buildSrc
---
In [previous post]({% post_url 2021-08-08-dry-declare-repository-in-gradle %}), we have created custom gradle plugin in build script. This post shows how to do it by using buildSrc.

# How to
1. Create buildSrc folder in root project. Then create `src/main/groovy` (yes, this post will use groovy language) folder inside it.
1. Create new file `CustomRepoDeclarator.groovy` under `src/main/groovy`
1. We can duplicate the [class CustomRepoDeclarator]({% post_url 2021-08-08-dry-declare-repository-in-gradle %}). But, we need to import `Project` and `Plugin`.
   ```
	import org.gradle.api.Project
	import org.gradle.api.Plugin

	class CustomRepoDeclarator implements Plugin<Project> {

	    @Override
	    void apply(Project target) {
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
	    }
	}

   ```
1. Now instead of using `apply from: './CustomRepoDeclarator.gradle'`, use `apply plugin: CustomRepoDeclarator` in root buildScript.

# Final Thought
BuildSrc provides mechanism to centralize all custom plugin that can be accessed in project. BuildSrc is automatically compiled and test, and put in the build script classpath. And it provides direct access to Gradle API too. Please read [Gradle Reference](https://docs.gradle.org/current/userguide/organizing_gradle_projects.html#sec:build_sources) for more about `buildSrc`.

