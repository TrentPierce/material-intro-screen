# Android Material Intro Screen
[![](https://jitpack.io/v/TrentPierce/material-intro-screen.svg)](https://jitpack.io/#TrentPierce/material-intro-screen)

This is a fork of the Material Intro Screen from TangoAgency. This fork allows you to use larger images in the onboarding screens. This is perfect for projects that already have text in the images, and prefer to not use the textviews under the images.

## Features
  - [Easily add new slides][Intro Activity]
  - [Custom slides][Custom Slide]
  - [Parallax slides][Parallax Slide]
  - Easy extensible api
  - Android TV support!
  - Material design at it's best!!!

| [Simple slide][SimpleSlide] | [Custom slide][Custom Slide] | [Permission slide][PermissionSlide] | [Finish slide][FinishSlide]
|:-:|:-:|:-:|:-:|
| ![Simple slide] | ![Customslide] | ![Permission slide] | ![Finish slide] |

## Usage
### Step 1:
#### Add the repository 
```
repositories {
			maven { url 'https://jitpack.io' }
		}
  ```
#### Add gradle dependecy
```
dependencies {
	        compile 'com.github.TrentPierce:material-intro-screen:0.0.6'
	}
```
### Step 2:
#### First, your [intro activity][Intro Activity] class needs to extend MaterialIntroActivity:
```java
public class IntroActivity extends MaterialIntroActivity
```
### Step 3:
#### Add activity to [manifest][Manifest] with defined theme:
```xml
        <activity
            android:name=".IntroActivity"
            android:theme="@style/Theme.Intro" />
```
### Step 4: 
#### [Add slides:][Intro Activity]
```java
 @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        addSlide(new SlideFragmentBuilder()
                .backgroundColor(R.color.colorPrimary)
                .buttonsColor(R.color.colorAccent)
                .possiblePermissions(new String[]{Manifest.permission.CALL_PHONE, Manifest.permission.READ_SMS})
                .neededPermissions(new String[]{Manifest.permission.CAMERA, Manifest.permission.ACCESS_FINE_LOCATION, Manifest.permission.ACCESS_COARSE_LOCATION})
                .image(agency.tango.materialintroscreen.R.drawable.ic_next)
                .title("title 3")
                .description("Description 3")
                .build(),
                new MessageButtonBehaviour(new View.OnClickListener() {
                    @Override
                    public void onClick(View v) {
                        showMessage("We provide solutions to make you love your work");
                    }
                }, "Work with love"));
}
```
#### Explanation of SlideFragment usage:
  - ```possiblePermissions``` &#8702; permissions which are not necessary to be granted
  - ```neededPersmissions``` &#8702; permission which are needed to be granted to move further from that slide
  - ```MessageButtonBehaviour``` &#8702; create a new instance only if you want to have a custom action or text on a message button

### Step 5: 
#### Customize Intro Activity:
  - ```setSkipButtonVisible()``` &#8702; show skip button instead of back button on the left bottom of screen
  - ```hideBackButton()``` &#8702; hides any button on the left bottom of screen
  - ```enableLastSlideAlphaExitTransition()``` &#8702; set if the last slide should disapear with alpha hiding effect

#### Customizing view animations: 

You can set enter, default and exit translation for every view in intro activity. To achive this you need to get translation wrapper for chosen view (for example: ```getNextButtonTranslationWrapper()```) and set there new class which will implement ```IViewTranslation```
```java
getBackButtonTranslationWrapper()
                .setEnterTranslation(new IViewTranslation() {
                    @Override
                    public void translate(View view, @FloatRange(from = 0, to = 1.0) float percentage) {
                        view.setAlpha(percentage);
                    }
                });
```
#### Available [translation wrappers][TranslationWrapper]:
- ```getNextButtonTranslationWrapper()```
- ```getBackButtonTranslationWrapper()```
- ```getPageIndicatorTranslationWrapper()```
- ```getViewPagerTranslationWrapper()``` 
- ```getSkipButtonTranslationWrapper()``` 

## Custom slides
#### Of course you are able to implement completely custom slides. You only need to extend SlideFragment and override following functions:
 - ```backgroundColor()```
 - ```buttonsColor()```
 - ```canMoveFurther()``` (only if you want to stop user from being able to move further before he will do some action)
 - ```cantMoveFurtherErrorMessage()``` (as above)
 
#### If you want to use parallax in a fragment please use one of the below views:
  - [```ParallaxFrameLayout```][ParallaxFrame]
  - [```ParallaxLinearLayout```][ParallaxLinear]
  - [```ParallaxRelativeLayout```][ParallaxRelative]

#### And set there the [app:layout_parallaxFactor][ParallaxFactor] attribute:
```xml
<agency.tango.materialintroscreen.parallax.ParallaxLinearLayout
xmlns:android="http://schemas.android.com/apk/res/android">

    <ImageView
        android:id="@+id/image_slide"
        app:layout_parallaxFactor="0.6"/>
```

All features which are not available in simple Slide Fragment are shown here: [Custom Slide]

## Things I have used to create this
 - For parallax I have used files from [Material Intro] by [@HeinrichReimer]
 - [InkPageIndicator.java] by [@NickButcher]
 - Images used to create sample app are from [freepik]
 - For over scroll effect on last slide I have partially used [Android-Overscroll-ViewPager]
 
## Getting Help

To report a specific problem or feature request, [open a new issue on Github](https://github.com/TrentPierce/material-intro-screen/issues/new).


[Here](https://github.com/TrentPierce/) you can see open source work developed by Tango Agency.
 
Whether you're searching for a new partner or trusted team for creating your new great product we are always ready to start work with you. 

You can contact us via Trent@SkeeBomb.com.
Thanks in advance.
 
