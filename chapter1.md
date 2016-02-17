# Canvas（画布）

The Canvas is the area that all UI elements should be inside. The Canvas is a Game Object with a Canvas component on it, and all UI elements must be children of such a Canvas.

所有的UI元素都应该包含在画布里。canvas实际上是一个有canvas组件的Game Object（游戏对象），所有的UI组件必须是这个canvas的子对象。


Creating a new UI element, such as an Image using the menu GameObject > UI > Image, automatically creates a Canvas, if there isn’t already a Canvas in the scene. The UI element is created as a child to this Canvas.

创建一个新的UI元素，例如从菜单“ GameObject > UI > Image”创建一个image，

The Canvas area is shown as a rectangle in the Scene View. This makes it easy to position UI elements without needing to have the Game View visible at all times.

#Draw order of elements

UI elements in the Canvas are drawn in the same order they appear in the Hierarchy. The first child is drawn first, the second child next, and so on. If two UI elements overlap, the later one will appear on top of the earlier one.

To change which element appear on top of other elements, simply reorder the elements in the Hierarchy by dragging them. The order can also be controlled from scripting by using these methods on the Transform component: SetAsFirstSibling, SetAsLastSibling, and SetSiblingIndex.

#Render Modes

The Canvas has a Render Mode setting which can be used to make it render in screen space or world space.


###Screen Space - Overlay


This render mode places UI elements on the screen rendered on top of the scene. If the screen is resized or changes resolution, the Canvas will automatically change size to match this.
![](Main/GUI_Canvas_Screenspace_Overlay.png)