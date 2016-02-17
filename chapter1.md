# Canvas 画布

The Canvas is the area that all UI elements should be inside. The Canvas is a Game Object with a Canvas component on it, and all UI elements must be children of such a Canvas.

所有的UI元素都应该包含在画布里。canvas实际上是一个有canvas组件的Game Object（游戏对象），所有的UI组件必须是这个canvas的子对象。


Creating a new UI element, such as an Image using the menu GameObject > UI > Image, automatically creates a Canvas, if there isn’t already a Canvas in the scene. The UI element is created as a child to this Canvas.

创建一个新的UI元素，例如从菜单“ GameObject > UI > Image”创建一个image，如果当前场景中不存在一个canvas，则会自动的创建一个canvas。该UI元素会作为子对象创建在这个画布里。

The Canvas area is shown as a rectangle in the Scene View. This makes it easy to position UI elements without needing to have the Game View visible at all times.

在场景视图中canvas区域显示为一个矩形。这样就不需要一直看着Game视图，可以在Scene窗口里便捷的定位UI元素。

##Draw order of elements 元素的绘制顺序

UI elements in the Canvas are drawn in the same order they appear in the Hierarchy. The first child is drawn first, the second child next, and so on. If two UI elements overlap, the later one will appear on top of the earlier one.

Canvas中的UI 元素以它们在Hierarchy模块中出现的相同顺序进行绘制。第一个子对象会第一个绘制，接下来是第二个子对象，以此类推。如果两个UI元素重叠，则晚一些绘制的会出现在早先绘制的上面

To change which element appear on top of other elements, simply reorder the elements in the Hierarchy by dragging them. The order can also be controlled from scripting by using these methods on the Transform component: SetAsFirstSibling, SetAsLastSibling, and SetSiblingIndex.

哪个元素需要显示在其他的元素之上，只要简单地去拖动元素即可重新排列他们在Hierarchy中的顺序。顺序也可以使用代码控制，通过调用Transform组件中的这些方法：SetAsFirstSibling，SetAsLastSibling，和 SetSiblingIndex。

##Render Modes 渲染模式

The Canvas has a Render Mode setting which can be used to make it render in screen space or world space.

画布拥有一种渲染模式用来决定它是在屏幕空间还是世界空间上渲染。

###Screen Space - Overlay


This render mode places UI elements on the screen rendered on top of the scene. If the screen is resized or changes resolution, the Canvas will automatically change size to match this.
这种渲染模式将UI元素放置在屏幕上并在场景的最前方渲染。如果更换了屏幕或者改变了分辨率，Canvas将自动改变大小来适配它。
![](Main/GUI_Canvas_Screenspace_Overlay.png)

UI in screen space overlay canvas
#Screen Space - Camera

This is similar to Screen Space - Overlay, but in this render mode, the Canvas is placed a given distance in front of a specified Camera. The UI elements are rendered by this camera, which means that the Camera settings affect the appearance of the UI. If the Camera is set to Perspective, the UI elements will be rendered with perspective, and the amount of perspective distortion can be controlled by the Camera Field of View. If the screen is resized or changes resolution, or the camera frustrum changes, the Canvas will automatically change size to match as well.


UI in screen space camera canvas
#World Space

In this render mode, the Canvas will behave as any other object in the scene. The size of the Canvas can be set manually using its Rect Transform, and UI elements will render in front of or behind other objects in the scene based on 3D placement. This is useful for UIs that are meant to be a part of the world. This is also known as a “diegetic interface”.


UI in world space canvas