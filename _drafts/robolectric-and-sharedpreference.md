---
layout: default
title: Robolectric and SharedPreference: Unfortunate Case
---
*Background*
Just upgrade Android SDK target version to 27 then running all test unit test together with Robelectric test. All is well until it is not. Test got stuck randomly. Neither error nor log is shown.

*Investigation*
1. Saw Robelectric has new release (3.8). Updated. Test still got stuck and got one  more error
~~~
java.lang.VerifyError: class org.robolectric.android.fakes.RoboMonitoringInstrumentation overrides final method specifyDexMakerCacheProperty
~~~
which easily fix by adding
~~~
testImplementation "com.android.support.test:runner:1.0.2"
testImplementation "com.android.support.test:rules:1.0.2"
~~~
1. Look more issue which Robolectric stuck and found this [issue](https://github.com/robolectric/robolectric/issues/3721). Open [visualvm](https://visualvm.github.io/) and dump thread while test stuck. Getting same log which SharedPreferenceEditor commit operation is blocking. Testing by remove it and test not stuck again.

*Conclusion*
Agree with comments in [issue](https://github.com/robolectric/robolectric/issues/3721) that SharedPreferenceEditor commit is waiting CountDownLatch condition to be fulfilled which in this case never happened. It is still open issue so no fix right now.

*My Fix*
Luckily, in my case this operation is not related with the tests itself. I can work around it by wrapping SharedPreference operation into class put it under `main` folder.
~~~
class Preference(sp: SharedPreference) {
  fun save(bool: Boolean) {
    sh.editor().put(bool).commit
  }
}
~~~
Then replace its implementation under `tests` folder.
~~~
class Preference(sp: SharedPreference) {
  fun save(bool: Boolean) {
    // do nothing
  }
}
~~~
