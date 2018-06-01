---
layout: default
title: Android Architecture Components
---
*Background*
As March 2018, Google release Android Architecture Lifecyle 1.1.0. After long time, I decide this is good time to try this especially after Jetpack announched. I will create simple Github client with this and will use Kotlin Coroutine for some parts (especially async).
My goal is to get basic understanding from there libraries and find way to incorporate it into my daily development.

*Architecture Lifecyle*
From here, I saw that Google start embracing reactive concept by providing simplifed state of activity, or, more accurately FragmentActivity (which is part of Android Support Library or Android X in future). What are these states?
DESTROYED, INITIALIZED,CREATED,STARTED, RESUMED
