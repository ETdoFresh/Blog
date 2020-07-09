---
title: 'Creating a Managed 3D Physics Engine in C# – Part I – Introduction'
author: ETdoFresh
type: post
date: 2017-05-06T18:03:51+00:00
url: /creating-a-managed-3d-physics-engine-in-c-part-i-introduction/
featured_image: /wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-1-1024.jpg
hide_featured_image: true
tags:
  - Physics
  - Programming
  - CSharp

---
Before I knew the existence of [Jitter Physics][1] (which is what I'll end up using), I decided to try to make my own Physics Engine following [Game Physics Engine Developmnet by Ian Millington][2], and basically got stuck somewhere when making Contact Resolvers for Rigidbodies. However, I wanted to share my experience making Physics Engine, hopefully as briefly as I can while still making sense.

## Base Data Types

Before we get started in creating the very best physics engine (right?), we first need to decide what kind of data types we'll be using.

### Single Precision (float) or Double Precision (double) Numbers

| Single | Double |
|--------|--------|
| • Size: 4 bytes | • Size: 8 bytes |
| • Precision: ~ 7 digits | • Precision: ~ 15 digits |
| • Range: -3.4 × 1{{< sup 38 >}} to +3.4 × 10{{< sup 38 >}} | • Range: ±5.0 × 10{{< sup -324 >}} to ±1.7 × 10{{< sup 308 >}} |
| • Pro: Faster | • Pro: Accuracy |

I am going to choose Single because it's faster, smaller, and basically it is almost exclusively used by Unity. That's where I'll be doing all my testing. Another goal of mine is to structure our code so that we can change between single and double pretty painlessly.

### Vector3

For convenience sake, it will be important to have access to a (or implement your own) Vector class that has 3 parameters X, Y, Z (of type float or double). Under Matrix, there is a cheat sheet of useful operations for Vectors and Matrices

### Quaternion

Because of issues with [Gimbal Lock][3] we want to steer away from using Vector3 (Euler Angles) to store rotation of an object. So we use Quaternions which have 4 parameters X, Y, Z, W.

### Matrix

Matrices are used because they are quite powerful. You can do various things with a matrix. You can store Position, Rotation, Scale. And the great thing is any combination of translates (moving position), rotations, and scale modifications can be combined into one matrix. For example, converting from local coordinates to world coordinates can be used by multiplying one matrix. However, the Math gets a little more complex. I found these cheatsheets online on the implementation of Vector3 and Matrix operations.

{{< image src="/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-1-1024.jpg" width="24%" >}}
{{< image src="/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-2-1024.jpg" width="24%" >}}
{{< image src="/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-3-1024.jpg" width="24%" >}}
{{< image src="/wp-content/uploads/2017/05/eng1091-past-paper-summary-monash-university-4-1024.jpg" width="24%" >}}

### Timing

We want our Physics Engine to run the same given the same input. Hence we will use a constant/fixed time step. This can be whatever you want, but I think for the purposes of this tutorial, we'll make it 1/60 seconds. Some psuedo code on how we can handle timing is

```c#
float time = 0f;
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
}
```

But if we are handling this via Unity, it'll probably more in line with the following:

```c#
private PhysicsManager physics;
private State previousState;

void Update()
{
	physics.Interpolate(previousState);
}

void FixedUpdate()
{
	previousState = physics.CurrentState;
	physics.Update(Time.fixedDeltaTime);
}
```

### Next Time...

We'll start with an overview of the entire Physics Engine. A list of objects, and what they'll be responsible for. Also start getting into basic physics concepts. See you there!

 [1]: https://github.com/mattleibow/jitterphysics
 [2]: https://www.amazon.com/Game-Physics-Engine-Development-Commercial-Grade/dp/0123819768
 [3]: https://en.wikipedia.org/wiki/Gimbal_lock