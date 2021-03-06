Fork of [Swipeable-Cards][6] for adding like or dislike image changing transparency depending on card rotation.
--------------------

### Like

![Example Image][7]
![Example Image][8]

### Dislike

![Example Image][9]
![Example Image][10]


Swipeable cards: Tinder-like cards library for Android
=================

Swipeable-cards is a native library for Android that provide a Tinder card like effect. A card can be constructed using an image and displayed with animation effects, dismiss-to-like and dismiss-to-unlike, and use different sorting mechanisms.

The library is compatible for Android versions 3.0 (API Level 11) and upwards.

A [library][1] and a [sample application][2] are provided with the code.

![Example Image][3]
![Example Image][4]


Usage
--------------------
Download the library with git and import it into your project (right now there is only Gradle support, so you need to import it writing in your build.gradle the following:

```groovy
compile project(':AndTinder')
```

and in your settings.gradle

```groovy
include 'AndTinder'
```

When you have included the library in your project, you need to proceeed as follows. First, create a container to store the cards.

```xml
<com.andtinder.view.CardContainer 
     xmlns:android="http://schemas.android.com/apk/res/android"
     android:id="@+id/layoutview"
     android:layout_width="fill_parent"
     android:layout_height="fill_parent" />
```
    
From your Activity, inflate into a CardContainer the container you declared in your XML
    
```java
mCardContainer = (CardContainer) findViewById(R.id.layoutview);
```

The card container can sort the cards either ordered or disordered:

```java
mCardContainer.setOrientation(Orientation.Ordered);
mCardContainer.setOrientation(Orientation.Disordered);
```
     
Now you need to create your cards. The procedure is quite simple: you just need to create an object CardView and provide the image resource you want to add:

```java
CardModel card = new CardModel("Title1", "Description goes here", r.getDrawable(R.drawable.picture1);
```
    
Additionally, you can set up a Delegate to be notified when the image is being liked or disliked:
     
```java
card.setOnCardDimissedListener(new CardModel.OnCardDismissedListener() {
     @Override
     public void onLike() {
          Log.d("Swipeable Card", "I liked it");
     }

     @Override
     public void onDislike() {
          Log.d("Swipeable Card", "I did not liked it");
     }
});
```

Or when it is clicked:

```java
card.setOnClickListener(new CardModel.OnClickListener() {
     @Override
     public void OnClickListener() {
          Log.i("Swipeable Cards","I am pressing the card");
     }
});
```

Finally, use an adapter to link the cards and the container:

```java
SimpleCardStackAdapter adapter = new SimpleCardStackAdapter(this);
adapter.add(new CardModel("Title1", "Description goes here", r.getDrawable(R.drawable.picture1)));
mCardContainer.setAdapter(adapter);
mCardContainer.setOnSwipeListener(new CardContainer.onSwipeListener() {
    @Override
    public void onSwipe(float scrollProgressPercent) {
        View view = mCardContainer.getSelectedView();
        view.findViewById(R.id.item_swipe_right_indicator)
                .setAlpha(scrollProgressPercent < 0 ? -scrollProgressPercent : 0);
        view.findViewById(R.id.item_swipe_left_indicator)
                .setAlpha(scrollProgressPercent > 0 ? scrollProgressPercent : 0);

    }
});
```

Version history
--------------------
*  14.02.2015: Version 0.3: Fixed bugs with the cards locations and updated to the latest build tools
*  4.06.2014: Published the version 0.2 with several improvements thanks to [Dr-Emann][5]
* 13.05.2014: Published the first version 0.1

Next steps
--------------------
There are many things that can be done with this library. 

* Allow custom templates
* Extend image personalization options
* Recreate the container when it has been emptied

If you want to colaborate with the project or have any idea to be implemented feel free to submit a pull request or to write an issue! 

Also, if you have used AndTinder on your app and you let me know, I can link it from here :)

Contact
--------------------

kidach1 - <kidach1.tngc@gmail.com>

License
-------

    Copyright 2014 Enrique López Mañas

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

[1]: https://github.com/kikoso/AndTinder/tree/master/AndTinder
[2]: https://github.com/kikoso/AndTinder/tree/master/AndTinderDemo
[3]: https://raw.github.com/kikoso/AndTinder/master/art/captura1.png
[4]: https://raw.github.com/kikoso/AndTinder/master/art/captura2.png
[5]: https://github.com/Dr-Emann
[6]: https://github.com/kikoso/Swipeable-Cards
[7]: https://qiita-image-store.s3.amazonaws.com/0/48274/a98bda2e-1ec6-73bb-4ffb-e6523ce67512.png
[8]: https://qiita-image-store.s3.amazonaws.com/0/48274/5070f0de-3b6b-de1a-6338-9bbdca983f0c.png
[9]: https://qiita-image-store.s3.amazonaws.com/0/48274/f90fb10f-7edb-a080-4ee9-337520b7e531.png
[10]: https://qiita-image-store.s3.amazonaws.com/0/48274/1a650822-6f3c-3ed5-db09-ce403672e516.png
