# Creating a World Space UI

The UI system makes it easy to create UI that is positioned in the world among other 2D or 3D objects in the Scene.

UI 系统很容易地创建 UI 用户界面，被定位在其他 2D 或 3D 场景中对象之间的世界 中。 

Start by creating a UI element (such as an Image) if you don’t already have one in your scene by using GameObject > UI > Image. This will also create a Canvas for you.

开始通过创建一个 UI 元素 （如 Image 图像），如果在你的场景中还没有，可以通过使 用：GameObject > UI > Image。这也将为您创建一个画布。 

##Set the Canvas to World Space

Select your Canvas and change the Render Mode to World Space.

选择你的画布，改变 Render Mode 渲染模式为 World Space 世界空间。 

Now your Canvas is already positioned in the World and can be seen by all cameras if they are pointed at it, but it is probably huge compared to other objects in your Scene. We’ll get back to that.

现在你的画布已经位于世界空间中，所有相机都可以被看到，如果他们都指着它，但它 可能是巨大的和你的场景中的其他对象相比。 

##Decide on a resolution

First you need to decide what the resolution of the Canvas should be. If it was an image, what should the pixel resolution of the image be? Something like 800x600 might be a good starting point. You enter the resolution in the Width and Height values of the Rect Transform of the Canvas. It’s probably a good idea to set the position to 0,0 at the same time.

首先你需要决定的画布分辨率应该是什么。如果它是一个图像，该图像的像素分辨率应 该是什么？像 800 x 600 可能是一个很好的起点。您在画布的 Rect Transform 上输入该分辨 率的宽度和高度值。它可能是一个好主意，在同一时间将位置设置为 0，0。 

##Specify the size of the Canvas in the world

Now you should consider how big the Canvas should be in the world. You can use the Scale tool to simply scale it down until it has a size that looks good, or you can decide how big it should be in meters.

If you want it to have a specific width in meters, you can can calculate the needed scale by using meter_size / canvas_width. For example, if you want it to be 2 meters wide and the Canvas width is 800, you would have 2 / 800 = 0.0025. You then set the Scale property of the Rect Transform on the Canvas to 0.0025 for both X, Y, and Z in order to ensure that it’s uniformly scaled.

Another way to think of it is that you are controlling the size of one pixel in the Canvas. If the Canvas is scaled by 0.0025, then that is also the size in the world of each pixel in the Canvas.

##Position the Canvas

Unlike a Canvas set to Screen Space, a World Space Canvas can be freely positioned and rotated in the Scene. You can put a Canvas on any wall, floor, ceiling, or slanted surface (or hanging freely in the air of course). Just use the normal Translate and Rotate tools in the toolbar.

##Create the UI

Now you can begin setting up your UI elements and layouts the same way you would with a Screen Space Canvas.