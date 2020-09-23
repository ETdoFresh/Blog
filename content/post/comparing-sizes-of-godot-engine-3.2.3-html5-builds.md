+++
author = "ETdoFresh"
date = 2020-09-23T22:37:08Z
excerpt = "I have been really getting into F# lately, and I realize, that I may have a problem. My builds of a nearly empty project is about 20MB bigger. So, I decided to compare all 3 of my language options and make a decision of what I will use going forward."
featured_image = "/uploads/2020/09/image20200923001.jpg"
tags = ["Godot", "CSharp", "FSharp", "GDScript"]
title = "Comparing Sizes of Godot Engine 3.2.3 HTML5 Builds"
url = ""

+++
## between GDScript, C#, F#

I have been really getting into F# lately, and I realize, that I may have a problem. My builds of a nearly empty project is about 20MB bigger. So, I decided to compare all 3 of my language options and make a decision of what I will use going forward.

### Example Project

![](/uploads/2020/09/image-20200923171532244.gif)

**World.tscn** \[Node Structure\]

* World
  * icon \[pre-built icon.png\]

### GDScript

_world.gd_

``` python
extends Node2D
var t = 0.0
func _process(delta):
    t += delta * 5
    get_node("icon").position = Vector2(0, cos(t) * 100)
```

#### HTML5 Build Size

16,852,924 bytes (16.0 MB)

### C#

_World.cs_

``` c#
using Godot;
public class World : Node
{
    float t = 0;
    public override void _Process(float delta)
    {
        t += delta * 5;
        GetNode<Sprite>("icon").Position = new Vector2(0, Mathf.Cos(t) * 100);
    }
}
```

#### HTML 5 Build Size

34,617,419 bytes (33.0 MB)

### F#

_World.fs_

``` F#
namespace FSharp
open Godot
type World() =
    inherit Node2D()
    let mutable t = 0.0f
    override this._Process delta =
        t <- t + delta * 5.0f
        let icon = this.GetNode<Node2D> (new NodePath "icon")
        icon.Position <- new Vector2(0.0f, cos t * 100.0f)
```

_World.cs_

``` c#
public class World : FSharp.World { }
```

#### HTML 5 Build Size

37,641,899 bytes (35.8 MB)

# Conclusion

On size alone, using **GDScript wins hands down**! However, there will be other factors like performance and support that will go into making my decision. I have read C# is much faster on big data structures/arrays. But as of right now, C# is still in alpha, and god only knows about F#. I used F# just to figure out how to best structure my project so that I can use C# or GDScript in a much more functional way.