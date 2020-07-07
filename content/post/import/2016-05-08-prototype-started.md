---
title: Prototype Started
author: ETdoFresh
type: post
date: 2016-05-09T04:21:10+00:00
url: /prototype-started/
categories:
  - Cargo Bay 5
  - Games

---
Covered today: 2D Sprites and Sprite Sheets, Animations, Movement

<div id="attachment_227" style="width: 1355px" class="wp-caption aligncenter">
  <img aria-describedby="caption-attachment-227" class="wp-image-227 size-full" src="http://www.etdofresh.com/wp-content/uploads/2016/05/S05E00.png" alt="S05E00" width="1345" height="756" />
  
  <p id="caption-attachment-227" class="wp-caption-text">
    Twitch Stream: S05E00 &#8211; Cargo Bay 5 &#8211; In the beginning&#8230;
  </p>
</div>

So today I decided to work on the prototype for Cargo Bay 5 just so our team can start to get the &#8220;feel&#8221; for what we are talking about. I got a 2D character animated and moving across the screen for my first official episode of my Season/Shelf 05 streams.<!--more-->

## 2D Sprites and Sprite Sheets

<img class="alignnone size-full wp-image-229" src="http://www.etdofresh.com/wp-content/uploads/2016/05/S05E00-2.png" alt="S05E00" width="1321" height="726" /> 

Here is what I did to get this Bomberman spritesheet in my prototype:

  * Start off with a nice transparent spritesheet like shown above.
  * In Inspector: 
      * Texture Type: Sprite (2D and UI)
      * Sprite Mode: Multiple
      * Slice (Top Left of Sprite Editor) and Smart Slice

If done correctly, you&#8217;ll have a nicely cut out Sprites (light grey box around each sprite). Click inside a grey box if dimensions are a bit off to edit it. Done!

I recommend whatever the size of your sprites are, you use the max width or height value as your Pixels Per Unit in the inspector so that your sprites fit in 1-by-1 Unity Units.

Another recommendation is to name each of your sprites&#8230; yup, it will be a pain in the butt, but will be worth it down the line.

## Animations

Now that you have a bunch of Sprites, it&#8217;s time to animate them in a flipbook fashion.

<img class="alignnone size-full wp-image-232" src="http://www.etdofresh.com/wp-content/uploads/2016/05/S05E00-3.png" alt="S05E00" width="805" height="388" /> 

There are multiple ways to create the animation, but the way I think I like the best (as of right now) is to select the sprites you would like in your animation, right click on a selected item, Click Create, Click Animation.

<img class="alignnone size-full wp-image-233" src="http://www.etdofresh.com/wp-content/uploads/2016/05/S05E00-4.png" alt="S05E00" width="902" height="412" /> 

You should then have an Animation File (probably called New Animation). Assign this animation in an animator of a GameObject that already has a SpriteRenderer. Open up an Animation window, and you should be able to play around with the animation file some more. I believe you could also just drag New Animation onto a Sprite GameObject. Either way, now you can make multiple Animator States for the different states of your character.

<img class="alignnone size-full wp-image-234" src="http://www.etdofresh.com/wp-content/uploads/2016/05/S05E00-5.png" alt="S05E00" width="907" height="340" /> 

## Movement

Since this is a top down game, we will not be using any gravity. In this prototype I used RigidBody 2D and Box Collider 2D with Gravity Scale set to 0.<img class="alignnone size-full wp-image-235" src="http://www.etdofresh.com/wp-content/uploads/2016/05/S05E00-6.png" alt="S05E00" width="1233" height="301" />

Then I created a script called Movement.cs to Animate the character and move the character using the RigidBody 2D.

<pre lang="csharp">// Movement.cs
using UnityEngine;
public class Movement : MonoBehaviour
{
    public float speedY = 2;
    public float speedX = 4;

    private Animator animator;
    private new Rigidbody2D rigidbody;

    private void Start()
    {
        animator = GetComponentInChildren&lt;Animator&gt;();
        rigidbody = GetComponentInChildren&lt;Rigidbody2D&gt;();
    }

    private void Update()
    {
        if (Input.GetAxisRaw("Horizontal") != 0)
        {
            if (Input.GetAxisRaw("Horizontal") &gt; 0)
            {
                animator.Play("Walk Right");
                rigidbody.velocity = new Vector2(speedX, 0);
            }
            else
            {
                animator.Play("Walk Left");
                rigidbody.velocity = new Vector2(-speedX, 0);
            }
        }
        else if (Input.GetAxisRaw("Vertical") != 0)
        {
            if (Input.GetAxisRaw("Vertical") &gt; 0)
            {
                animator.Play("Walk Up");
                rigidbody.velocity = new Vector2(0, speedY);
            }
            else
            {
                animator.Play("Walk Down");
                rigidbody.velocity = new Vector2(0, -speedY);
            }
        }
        else
        {
            animator.Play("Idle");
            rigidbody.velocity = Vector2.zero;
        }
    }
}
</pre>

In the final product, I do not recommend calling animator.Play() or rigidbody.velocty in the Update() function. But for now, attach the script to your GameObject with the Animator with the Animations and that&#8217;s it! We got a 2D Sprite moving and animating around in a 2D World.