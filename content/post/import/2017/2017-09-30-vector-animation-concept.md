---
title: Vector Animation Concept
author: ETdoFresh
type: post
date: 2017-09-30T18:00:18+00:00
url: /vector-animation-concept/
linkedFacebookPostID:
  - 10102442561105218_10102443183013908
categories:
  - Programming

---
[<img class="aligncenter size-large wp-image-924" src="https://www.etdofresh.com/wp-content/uploads/2017/09/VectorAnimationPrototype-1024x596.png" alt="" width="840" height="489" srcset="http://localhost/wp-content/uploads/2017/09/VectorAnimationPrototype-1024x596.png 1024w, http://localhost/wp-content/uploads/2017/09/VectorAnimationPrototype-300x175.png 300w, http://localhost/wp-content/uploads/2017/09/VectorAnimationPrototype-768x447.png 768w, http://localhost/wp-content/uploads/2017/09/VectorAnimationPrototype-1200x698.png 1200w, http://localhost/wp-content/uploads/2017/09/VectorAnimationPrototype.png 1602w" sizes="(max-width: 840px) 100vw, 840px" />][1]I am currently working on software called **Vector Animation** (subject to change). The software will allow you to draw (or import), bone, animate, and test animations all in one place. The scope is big, but I am trying to avoid any bells or whistles.

## Draw Mode  
[<img class="aligncenter wp-image-918" src="https://www.etdofresh.com/wp-content/uploads/2017/09/RasterVsVector-300x200.png" alt="" width="200" height="133" srcset="http://localhost/wp-content/uploads/2017/09/RasterVsVector-300x200.png 300w, http://localhost/wp-content/uploads/2017/09/RasterVsVector.png 431w" sizes="(max-width: 200px) 100vw, 200px" />][2]

Vector art has definitely taken hold of many media outlets, like games, websites, comics, etc. Instead of pixels, everything is drawn with lines, curves, polygons, and basic shapes. Vector Animation will definitely not be the next Adobe Illustrator or Inkscape when it comes to drawing, but there will be a basic draw mode for anyone to at least dabble in Vector Art. This will also be good for any small modifications that need to be made.

## Bone Mode

[<img class="aligncenter size-full wp-image-922" src="https://www.etdofresh.com/wp-content/uploads/2017/09/BoneExample.png" alt="" width="439" height="429" srcset="http://localhost/wp-content/uploads/2017/09/BoneExample.png 439w, http://localhost/wp-content/uploads/2017/09/BoneExample-300x293.png 300w" sizes="(max-width: 439px) 100vw, 439px" />][3]

Bones map many different parts of an object into a bone structure. This simplifies animation via a hierarchy. For example if lift my leg, my foot comes along. In addition, re-targeting is helpful to applying one set of animation to many different types of characters of different sizes and shapes (if they contain the same bones).

## Animation Mode

Making your drawing come to life is the main purpose of this software. Using keyframes, interpolation (tweening), and layer switching, drawings will become alive. And because we are into game development, we want to create software where you can export all your animations into software like Unity 3d easily.

## Play Mode

Want to test your animation in game? Exporting from one software and importing to another can start to get tedious. Because we are building this in Unity, we can also allow you test in the Unity Game Engine. We will provide very simple templates like platformer, overhead joystick, and click-and-point adventure where you just plug in animations, and you can test to see how your character feels in a game.

 [1]: https://www.etdofresh.com/wp-content/uploads/2017/09/VectorAnimationPrototype.png
 [2]: https://www.etdofresh.com/wp-content/uploads/2017/09/RasterVsVector.png
 [3]: https://www.etdofresh.com/wp-content/uploads/2017/09/BoneExample.png