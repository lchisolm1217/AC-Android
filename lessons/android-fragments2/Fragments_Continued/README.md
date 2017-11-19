# Fragments: Views with their own Lifecyles

## Objectives

* Fellows will learn what fragments are
* Fellows will explore the Fragment Lifecycle
* Fellows will instantiate Fragments
* Fellows will utilize Fagment managers
* Fellows will use Fragment Transactions to add bundles and commit Fragments
* Fellows will add Fragments to a BackStack
* Fellows will add and replace Fragments within Frame Layouts

# Lecture

As we've seen with Activities, the only way to include different layouts for an activity, is to use the <include> tag in your layout xml, or to use an intent to switch between activities. However, there are ways to have multiple Activity-like views, with their own view logic, both attached to, and indepented of, an activity within your app.

## What is a Fragment?

According to the [Android Docs](https://developer.android.com/guide/components/fragments.html):

*"A Fragment represents a behavior or a portion of user interface in an Activity. You can combine multiple fragments in a single activity to build a multi-pane UI and reuse a fragment in multiple activities. You can think of a fragment as a modular section of an activity, which has its own lifecycle, receives its own input events, and which you can add or remove while the activity is running (sort of like a "sub activity" that you can reuse in different activities)."*

## The Fragment Lifecycle

The Fragment Lifecycle is similar to that of the Activity Lifecycle, in that it goes through various stages throughout its lifecycle, and can shift between these states depending on the actions of either the user, or the device itself. However, fragments have additional lifecycle callback methods that Activities do not, primarily because they can only exist within an activity, and must respect its parent's lifecycle as well.

|Fragment Lifecycle Callback Method|Description|
|:-----------:|:-----------------|
|onAttach()|This method will be called first, even before onCreate(), letting us know that your fragment has been attached to an activity. You are passed the Activity that will host your fragment|
|onCreateView()| The system calls this callback when it’s time for the fragment to draw its UI for the first time. To draw a UI for the fragment, a View component must be returned from this method which is the root of the fragment’s layout. We can return null if the fragment does not provide a UI|
|onViewCreated()| This will be called after onCreateView(). This is particularly useful when inheriting the onCreateView() implementation but we need to configure the resulting views, such as with a ListFragment and when to set up an adapter|
|onActivityCreated()| This will be called after onCreate() and onCreateView(), to indicate that the activity’s onCreate() has completed. If there is something that’s needed to be initialised in the fragment that depends upon the activity’s onCreate() having completed its work then onActivityCreated() can be used for that initialisation work|
|onStart()|The onStart() method is called once the fragment gets visible|
|onPause()|The system calls this method as the first indication that the user is leaving the fragment. This is usually where you should commit any changes that should be persisted beyond the current user session|
|onStop()|Fragment going to be stopped by calling onStop()|
|onDestroyView()|It’s called before onDestroy(). This is the counterpart to onCreateView() where we set up the UI. If there are things that are needed to be cleaned up specific to the UI, then that logic can be put up in onDestroyView()|
|onDestroy()|onDestroy() called to do final clean up of the fragment’s state but Not guaranteed to be called by the Android platform|
|onDetach()|It’s called after onDestroy(), to notify that the fragment has been disassociated from its hosting activity|

## Why use Fragments?

Although it is tempting to think of designing an entire app with many different activities, your manifest fill up with their declarations pretty fast. Fragments are like activities that can be swapped out many times, without having to leave the current activity. You can have only one activity running at any given time, but you can have a seemingly infinite number of fragments running at any given time.

Fragments give us the opportunity to create dynamic UI elements within our application. 

Fragments are available as widgets we can use within our XLM Layout files. However, they are rarely if ever used that way. Often, fragments are instantiated at runtime, and replace the contents of a view container.

Typically, when creating an app where Fragments are the UI elements most often used to host the views visible to the user, a main fragment is added, or replaces the contents of a view container, which typically takes up the entire screen. In the layout XML for our Main Activity, we can add a FrameLayout, within the root view, which will be used to "swap out" fragments as necessary:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context="nyc.c4q.fragmentstesting.MainActivity">

    <FrameLayout
        android:id="@+id/main_container"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    </FrameLayout>

</LinearLayout>
```

Because the FrameLayout is set to "match_parent" for both width and height, it will take up the whole screen. We can then fill the screen with our fragment at runtime.

```java
package nyc.c4q.fragmentstesting;

import android.support.v4.app.FragmentManager;
import android.support.v4.app.FragmentTransaction;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

import nyc.c4q.fragmentstesting.Fragments.ButtonFragment;
import nyc.c4q.fragmentstesting.Fragments.MainFragment;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        MainFragment mainFragment = new MainFragment();
        FragmentManager fragmentManager = getSupportFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
        fragmentTransaction.replace(R.id.main_container, mainFragment);
        fragmentTransaction.commit();
    }
}
```
