---
title: 'Creating a Managed 3D Physics Engine in C# – Part I – Introduction'
author: ETdoFresh
type: post
date: 2017-05-06T18:03:51+00:00
url: /creating-a-managed-3d-physics-engine-in-c-part-i-introduction/
categories:
  - Programming
tags:
  - Physics

---
Before I knew the existence of [Jitter Physics][1] (which is what I&#8217;ll end up using), I decided to try to make my own Physics Engine following [Game Physics Engine Developmnet by Ian Millington][2], and basically got stuck somewhere when making Contact Resolvers for Rigidbodies. However, I wanted to share my experience making Physics Engine, hopefully as briefly as I can while still making sense.

## Base Data Types

Before we get started in creating the very best physics engine (right?), we first need to decide what kind of data types we&#8217;ll be using.

### Single Precision (float) or Double Precision (double) Numbers

<table>
  <tr>
    <td>
      <strong>Single</strong>
    </td>
    
    <td>
      <strong>Double</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      <ul>
        <li>
          Size: 4 bytes
        </li>
        <li>
          Precision: ~ 7 digits
        </li>
        <li>
          Range: -3.4 × 10<sup>38 </sup>to +3.4 × 10<sup>38</sup>
        </li>
        <li>
          Pro: Faster
        </li>
      </ul>
    </td>
    
    <td>
      <ul>
        <li>
          Size: 8 bytes
        </li>
        <li>
          Precision: ~ 15 digits
        </li>
        <li>
          Range: ±5.0 × 10<sup>−324</sup> to ±1.7 × 10<sup>308</sup>
        </li>
        <li>
          Pro: Accuracy
        </li>
      </ul>
    </td>
  </tr>
</table>

I am going to choose Single because it&#8217;s faster, smaller, and basically it is almost exclusively used by Unity. That&#8217;s where I&#8217;ll be doing all my testing. Another goal of mine is to structure our code so that we can change between single and double pretty painlessly.

### Vector3

For convenience sake, it will be important to have access to a (or implement your own) Vector class that has 3 parameters X, Y, Z (of type float or double). Under Matrix, there is a cheat sheet of useful operations for Vectors and Matrices

### Quaternion

Because of issues with [Gimbal Lock][3] we want to steer away from using Vector3 (Euler Angles) to store rotation of an object. So we use Quaternions which have 4 parameters X, Y, Z, W.

### Matrix

Matrices are used because they are quite powerful. You can do various things with a matrix. You can store Position, Rotation, Scale. And the great thing is any combination of translates (moving position), rotations, and scale modifications can be combined into one matrix. For example, converting from local coordinates to world coordinates can be used by multiplying one matrix. However, the Math gets a little more complex. I found these cheatsheets online on the implementation of Vector3 and Matrix operations.

<table>
  <tr>
    <td>
      <a href="https://www.etdofresh.com/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-1-1024.jpg"><img class="wp-image-876 size-thumbnail" src="https://www.etdofresh.com/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-1-1024-150x150.jpg" alt="" width="150" height="150" /></a>
    </td>
    
    <td>
      <a href="https://www.etdofresh.com/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-2-1024.jpg"><img class="wp-image-877 size-thumbnail" src="https://www.etdofresh.com/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-2-1024-150x150.jpg" alt="" width="150" height="150" /></a>
    </td>
    
    <td>
      <a href="https://www.etdofresh.com/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-3-1024.jpg"><img class="wp-image-878 size-thumbnail" src="https://www.etdofresh.com/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-3-1024-150x150.jpg" alt="" width="150" height="150" /></a>
    </td>
    
    <td>
      <a href="https://www.etdofresh.com/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-4-1024.jpg"><img class="wp-image-879 size-thumbnail" src="https://www.etdofresh.com/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-4-1024-150x150.jpg" alt="" width="150" height="150" /></a>
    </td>
  </tr>
</table>

### Timing

We want our Physics Engine to run the same given the same input. Hence we will use a constant/fixed time step. This can be whatever you want, but I think for the purposes of this tutorial, we&#8217;ll make it 1/60 seconds. Some psuedo code on how we can handle timing is

<pre class="lang:default decode:true " title="Time PsuedoCode">float time = 0f;
float fixedDeltaTime = 1 / 60f;
float deltaTimeLimit = 0.25f;
float timeAccumulator = 0f;
float previousTime = GetTime();
State currentState = GetCurrentState();
State previousState = GetCurrentState();
while(programIsRunning())
{
	float currentTime = GetTime();
	float deltaTime = currentTime - previousTime;
	deltaTime = Math.Min(deltaTime, deltaTimeLimit);
	previousTime = currentTime;
	timeAccumulator += deltaTime;

	while(timeAccumulator &gt;= fixedDeltaTime)
	{
		previousState = currentState;
		Update(out currentState, time, fixedDeltaTime);
		time += fixedDeltaTime;
		accumulator -= fixedDeltaTime;
	}
	float deltaState = timeAccumulator / fixedDeltaTime;
	State intermediate = LinearInterpolate(prevviousState, currentState, deltaState);
	Render(intermediate);
}</pre>

But if we are handling this via Unity, it&#8217;ll probably more in line with the following:

<pre class="lang:default decode:true" title="Unity Time Psuedocode">private PhysicsManager physics;
private State previousState;

void Update()
{
	physics.Interpolate(previousState);
}

void FixedUpdate()
{
	previousState = physics.CurrentState;
	physics.Update(Time.fixedDeltaTime);
}</pre>

### Next Time&#8230;

We&#8217;ll start with an overview of the entire Physics Engine. A list of objects, and what they&#8217;ll be responsible for. Also start getting into basic physics concepts. See you there!

 [1]: https://github.com/mattleibow/jitterphysics
 [2]: https://www.amazon.com/Game-Physics-Engine-Development-Commercial-Grade/dp/0123819768
 [3]: https://en.wikipedia.org/wiki/Gimbal_lock