# IMGUI Layout Modes

##Fixed Layout vs Automatic Layout

There are two different modes you can use to arrange and organize your UI when using the IMGUI system: Fixed and Automatic. Up until now, every IMGUI example provided in this guide has used Fixed Layout. To use Automatic Layout, write GUILayout instead of GUI when calling control functions. You do not have to use one Layout mode over the other, and you can use both modes at once in the same OnGUI() function.

可以采用两种不同的模式来安排组织您的 GUI：固定模式和自动模式。目前为止，本指南中所提供 的所有 UnityGUI 示例都采用固定布局 (Fixed Layout)。要使用自动布局 (Automatic Layout) 模式，在调用控制函数时,写入 GUILayout 来代替 GUI。您不必逐个设置布局模式，并且还可以在同一 OnGUI() 函数中同时使用两种模式。

Fixed Layout makes sense to use when you have a pre-designed interface to work from. Automatic Layout makes sense to use when you don’t know how many elements you need up front, or don’t want to worry about hand-positioning each Control. For example, if you are creating a number of different buttons based on Save Game files, you don’t know exactly how many buttons will be drawn. In this case Automatic Layout might make more sense. It is really dependent on the design of your game and how you want to present your interface.

当您已经有了一个预先设计好界面可以用来工作时,就可以使用固定布局 (Fixed Layout)。当您之前不知道需要多少元素，或者不想手动安置每个控件时，则可以使用自动布局 (Automatic Layout)。比如，当您要根据保存游戏文件来创建若干不同按钮时，您可能不知道要绘制按钮的确切数目。在这种情况下使用自动布局 (Automatic Layout) 会更方便。这实际上取决于游戏的设计以及您想要如何呈现界面。

There are two key differences when using Automatic Layout:

使用自动布局 (Automatic Layout) 时，存在两个关键的不同之处：

* GUILayout is used instead of GUI
* 使用 GUILayout，而非 GUI
* No Rect() function is required for Automatic Layout Controls
* 自动布局 (Automatic Layout Controls) 控件无需 Rect() 函数

```
/* Two key differences when using Automatic Layout */


// JavaScript
function OnGUI () {
    // Fixed Layout
    GUI.Button (Rect (25,25,100,30), "I am a Fixed Layout Button");

    // Automatic Layout
    GUILayout.Button ("I am an Automatic Layout Button");
}


// C#
using UnityEngine;
using System.Collections;

public class GUITest : MonoBehaviour {
    
    void OnGUI () {
        // Fixed Layout
        GUI.Button (new Rect (25,25,100,30), "I am a Fixed Layout Button");
    
        // Automatic Layout
        GUILayout.Button ("I am an Automatic Layout Button");
    }

}
```


##Arranging Controls

Depending on which Layout Mode you’re using, there are different hooks for controlling where your Controls are positioned and how they are grouped together. In Fixed Layout, you can put different Controls into Groups. In Automatic Layout, you can put different Controls into Areas, Horizontal Groups, and Vertical Groups

随您所使用的布局模式而定，可采用不同的挂钩来控制控件 (Controls) 的位置以及这些控件的集合方式。在固定布局 (Fixed Layout) 中，您可以将不同的控件 (Controls) 放入 群组 (Groups) 。在自动布局 (Fixed Layout) 中，您可以将不同的控件 (Controls) 放入 区域 (Areas)、水平群组 (Horizontal Groups) 和垂直群组 (Vertical Groups)。

###Fixed Layout - Groups

Groups are a convention available in Fixed Layout Mode. They allow you to define areas of the screen that contain multiple Controls. You define which Controls are inside a Group by using the GUI.BeginGroup() and GUI.EndGroup() functions. All Controls inside a Group will be positioned based on the Group’s top-left corner instead of the screen’s top-left corner. This way, if you reposition the group at runtime, the relative positions of all Controls in the group will be maintained.

群组 (Groups) 是固定布局模式 (Fixed Layout Mode) 下可用的惯例，使您能够定义包含多个控件 (Controls) 的屏幕区域。您通过使用GUI.BeginGroup() 函数和GUI.EndGroup() 函数来定义哪些控件 (Controls) 在一个群组 (Group) 内。一个群组 (Group) 内的所有控件 (Controls) 都将基于群组 (Group) 的左上角来放置而不是按屏幕的左上角。以此方式，当您在运行时重新调整该群组的位置时，群组内所有控件 (Controls) 的相对位置保持不变。

As an example, it’s very easy to center multiple Controls on-screen.

例如，可以很容易地把多个控件 (Controls) 放置在屏幕中心。
```

/* Center multiple Controls on the screen using Groups */


// JavaScript
function OnGUI () {
    // Make a group on the center of the screen
    GUI.BeginGroup (Rect (Screen.width / 2 - 50, Screen.height / 2 - 50, 100, 100));
    // All rectangles are now adjusted to the group. (0,0) is the topleft corner of the group.
    
    // We'll make a box so you can see where the group is on-screen.
    GUI.Box (Rect (0,0,100,100), "Group is here");
    GUI.Button (Rect (10,40,80,30), "Click me");
    
    // End the group we started above. This is very important to remember!
    GUI.EndGroup ();
}


// C#
using UnityEngine;
using System.Collections;

public class GUITest : MonoBehaviour {
    
    void OnGUI () {
        // Make a group on the center of the screen
        GUI.BeginGroup (new Rect (Screen.width / 2 - 50, Screen.height / 2 - 50, 100, 100));
        // All rectangles are now adjusted to the group. (0,0) is the topleft corner of the group.
    
        // We'll make a box so you can see where the group is on-screen.
        GUI.Box (new Rect (0,0,100,100), "Group is here");
        GUI.Button (new Rect (10,40,80,30), "Click me");
    
        // End the group we started above. This is very important to remember!
        GUI.EndGroup ();
    }

}
```


![The above example centers controls regardless of the screen resolution](file:///C:/Program%20Files/Unity/Editor/Data/Documentation/en/uploads/Main/gsg-GroupCenteredControls.png)
######The above example centers controls regardless of the screen resolution
You can also nest multiple Groups inside each other. When you do this, each group has its contents clipped to its parent’s space.

您也可以将多个群组 (Group) 嵌套进彼此内部。进行嵌套后，每个群组的内容都被剪切到其父级空间。
```

/* Using multiple Groups to clip the displayed Contents */


// JavaScript
var bgImage : Texture2D; // background image that is 256 x 32
var fgImage : Texture2D; // foreground image that is 256 x 32
var playerEnergy = 1.0; // a float between 0.0 and 1.0

function OnGUI () {
    // Create one Group to contain both images
    // Adjust the first 2 coordinates to place it somewhere else on-screen
    GUI.BeginGroup (Rect (0,0,256,32));

    // Draw the background image
    GUI.Box (Rect (0,0,256,32), bgImage);
    
    // Create a second Group which will be clipped
    // We want to clip the image and not scale it, which is why we need the second Group
    GUI.BeginGroup (Rect (0,0,playerEnergy * 256, 32));

    // Draw the foreground image
    GUI.Box (Rect (0,0,256,32), fgImage);

    // End both Groups
    GUI.EndGroup ();
    GUI.EndGroup ();
}


// C#
using UnityEngine;
using System.Collections;

public class GUITest : MonoBehaviour {
    
    // background image that is 256 x 32
    public Texture2D bgImage; 
    
    // foreground image that is 256 x 32
    public Texture2D fgImage; 
    
    // a float between 0.0 and 1.0
    public float playerEnergy = 1.0f; 
    
    void OnGUI () {
        // Create one Group to contain both images
        // Adjust the first 2 coordinates to place it somewhere else on-screen
        GUI.BeginGroup (new Rect (0,0,256,32));
    
        // Draw the background image
        GUI.Box (new Rect (0,0,256,32), bgImage);
    
            // Create a second Group which will be clipped
            // We want to clip the image and not scale it, which is why we need the second Group
            GUI.BeginGroup (new Rect (0,0,playerEnergy * 256, 32));
        
            // Draw the foreground image
            GUI.Box (new Rect (0,0,256,32), fgImage);
        
            // End both Groups
            GUI.EndGroup ();
        
        GUI.EndGroup ();
    }

}

```

![You can nest Groups together to create clipping behaviors](file:///C:/Program%20Files/Unity/Editor/Data/Documentation/en/uploads/Main/gsg-NestedGroupsClipping.png)
######You can nest Groups together to create clipping behaviors
###Automatic Layout - Areas

Areas are used in Automatic Layout mode only. They are similar to Fixed Layout Groups in functionality, as they define a finite portion of the screen to contain GUILayout Controls. Because of the nature of Automatic Layout, you will nearly always use Areas.

区域 (Areas) 只在自动布局 (Automatic Layout) 模式中使用。区域在功能上与固定布局群组类似，因为它们定义了屏幕中有限的一部分来容纳 GUILayout 控件。由于自动布局 (Automatic Layout) 特性的原因，您几乎会总是用到区域 (Area)。

In Automatic Layout mode, you do not define the area of the screen where the Control will be drawn at the Control level. The Control will automatically be placed at the upper-leftmost point of its containing area. This might be the screen. You can also create manually-positioned Areas. GUILayout Controls inside an area will be placed at the upper-leftmost point of that area.

在自动布局 (Automatic Layout) 模式中，不必在控件层 (Control level) 定义要绘制控件的屏幕区域。控件 (Control) 将被自动放置到容纳区域的最左上角。这有可能是屏幕。您也可以创建手动放置区域 (Areas)。区域内的 GUILayout 控件 (GUILayout Control) 将被放置到该区域的最左上角。

```
/* A button placed in no area, and a button placed in an area halfway across the screen. */


// JavaScript
function OnGUI () {
    GUILayout.Button ("I am not inside an Area");
    GUILayout.BeginArea (Rect (Screen.width/2, Screen.height/2, 300, 300));
    GUILayout.Button ("I am completely inside an Area");
    GUILayout.EndArea ();
}


// C#
using UnityEngine;
using System.Collections;

public class GUITest : MonoBehaviour {
    
    void OnGUI () {
        GUILayout.Button ("I am not inside an Area");
        GUILayout.BeginArea (new Rect (Screen.width/2, Screen.height/2, 300, 300));
        GUILayout.Button ("I am completely inside an Area");
        GUILayout.EndArea ();
    }

}
```


Notice that inside an Area, Controls with visible elements like Buttons and Boxes will stretch their width to the full length of the Area.

注意，在一个区域 (Area) 内，带按钮 (Buttons)、框 (Boxes) 等可见元素的控件都会将其宽度拉伸至区域 (Area) 的全长。
###Automatic Layout - Horizontal and Vertical Groups

When using Automatic Layout, Controls will by default appear one after another from top to bottom. There are plenty of occasions you will want finer level of control over where your Controls are placed and how they are arranged. If you are using the Automatic Layout mode, you have the option of Horizontal and Vertical Groups.

Like the other layout Controls, you call separate functions to start or end these groups. The specific functions are GUILayout.BeginHoriztontal(), GUILayout.EndHorizontal(), GUILayout.BeginVertical(), and GUILayout.EndVertical().

Any Controls inside a Horizontal Group will always be laid out horizontally. Any Controls inside a Vertical Group will always be laid out vertically. This sounds plain until you start nesting groups inside each other. This allows you to arrange any number of controls in any imaginable configuration.

```
/* Using nested Horizontal and Vertical Groups */


// JavaScript
var sliderValue = 1.0;
var maxSliderValue = 10.0;

function OnGUI()
{
    // Wrap everything in the designated GUI Area
    GUILayout.BeginArea (Rect (0,0,200,60));

    // Begin the singular Horizontal Group
    GUILayout.BeginHorizontal();

    // Place a Button normally
    if (GUILayout.RepeatButton ("Increase max\nSlider Value"))
    {
        maxSliderValue += 3.0 * Time.deltaTime;
    }

    // Arrange two more Controls vertically beside the Button
    GUILayout.BeginVertical();
    GUILayout.Box("Slider Value: " + Mathf.Round(sliderValue));
    sliderValue = GUILayout.HorizontalSlider (sliderValue, 0.0, maxSliderValue);

    // End the Groups and Area
    GUILayout.EndVertical();
    GUILayout.EndHorizontal();
    GUILayout.EndArea();
}


// C#
using UnityEngine;
using System.Collections;

public class GUITest : MonoBehaviour {
    
    private float sliderValue = 1.0f;
    private float maxSliderValue = 10.0f;
    
    void OnGUI()
    {
        // Wrap everything in the designated GUI Area
        GUILayout.BeginArea (new Rect (0,0,200,60));
    
        // Begin the singular Horizontal Group
        GUILayout.BeginHorizontal();
    
        // Place a Button normally
        if (GUILayout.RepeatButton ("Increase max\nSlider Value"))
        {
            maxSliderValue += 3.0f * Time.deltaTime;
        }
    
        // Arrange two more Controls vertically beside the Button
        GUILayout.BeginVertical();
        GUILayout.Box("Slider Value: " + Mathf.Round(sliderValue));
        sliderValue = GUILayout.HorizontalSlider (sliderValue, 0.0f, maxSliderValue);
    
        // End the Groups and Area
        GUILayout.EndVertical();
        GUILayout.EndHorizontal();
        GUILayout.EndArea();
    }

}
```


![Three Controls arranged with Horizontal & Vertical Groups](file:///C:/Program%20Files/Unity/Editor/Data/Documentation/en/uploads/Main/gsg-NestedGroupsLayout.png)
######Three Controls arranged with Horizontal & Vertical Groups
##Using GUILayoutOptions to define some controls

You can use GUILayoutOptions to override some of the Automatic Layout parameters. You do this by providing the options as the final parameters of the GUILayout Control.

Remember in the Areas example above, where the button stretches its width to 100% of the Area width? We can override that if we want to.

```
/* Using GUILayoutOptions to override Automatic Layout Control properties */


//JavaScript
function OnGUI () {
    GUILayout.BeginArea (Rect (100, 50, Screen.width-200, Screen.height-100));
    GUILayout.Button ("I am a regular Automatic Layout Button");
    GUILayout.Button ("My width has been overridden", GUILayout.Width (95));
    GUILayout.EndArea ();
}


// C#
using UnityEngine;
using System.Collections;

public class GUITest : MonoBehaviour {
        
    void OnGUI () {
        GUILayout.BeginArea (new Rect (100, 50, Screen.width-200, Screen.height-100));
        GUILayout.Button ("I am a regular Automatic Layout Button");
        GUILayout.Button ("My width has been overridden", GUILayout.Width (95));
        GUILayout.EndArea ();
    }

}

```

For a full list of possible GUILayoutOptions, please read the GUILayoutOption Scripting Reference page.