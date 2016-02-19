# Making UI elements fit the size of their content

Normally when positioning a UI element with its Rect Transform, its position and size is specified manually (optionally including behavior to stretch with the parent Rect Transform).

通常当 UI 元素定位到 Rect Transform 上时，其位置和大小是手动指定的 （选项包括 stretch 与父 Rect Transform）。

However, sometimes you may want the rectangle to be automatically sized to fit the content of the UI element. This can be done by adding a component called Content Size Fitter.

然而，有时你可能想要矩形可以自动调整大小来适应 UI 元素的内容。这可以通过添加 一个称为 Content Size Fitter 的组件。

##Fit to size of Text

In order to make a Rect Transform with a Text component on it fit the text content, add a Content Size Fitter component to the same Game Object which has the Text component. Then set both the Horizontal Fit and Vertical Fit dropdowns to the Preferred setting.

为了使 Rect Transform 与 Text 文本组件适合它的的文本内容，添加 Content Size Fitter 组件到具有 Text 文本组件的同一游戏对象上。然后设置 Horizontal Fit、Vertical Fit，或者两个 都预先设置

###How does it work?

What happens here is that the Text component functions as a Layout Element that can provide information about how big its minimum and preferred size is. In a manual layout this information is not used. A Content Size Fitter is a type of Layout Controller, which listens to layout information provided by Layout Elements and control the size of the Rect Transform according to this.

发生了什么在这里是 Text 组件功能作为一个 Layout Element 布局元素，可以提供有关其 最小值和首选的大小是多少的信息。在手动布局中不使用此信息。Content Size Fitter 是 Layout Controller 的一种类型，它听布局信息提供的布局元素和控件的 Rect Transform 大小。 

###Remember the pivot

When UI elements are automatically resized to fit their content, you should pay extra attention to the pivot of the Rect Transform. The pivot will stay in place when the element is resized, so by setting the pivot position you can control in which direaction the element will expand or shrink. For example, if the pivot is in the center, then the element will expand equally in all directions, and if the pivot is in the upper left corner, then the element will expand to the right and down.

当 UI 元素将自动调整大小以适合其内容时，你要额外留意到 pivot 的 Rect Transform。 pivot 留在的地方，当调整元素大小，所以通过设置 pivot 的位置你可以控制哪些内件中元素 将会扩展或收缩。例如，如果 pivot 是在中心，然后该元素将展开同样在所有方向上，如果 pivot 是在左上角，然后该元素将展开向右和向下。

##Fit to size of UI element with child Text

If you have a UI element, such as a Button, that has a background image and a child Game Object with a Text component on it, you probably want the whole UI element to fit the size of the text - maybe with some padding.

In order to do this, first add a Horizontal Layout Group to the UI element, then add a Content Size Fitter too. Set the Horizontal Fit, the Vertical Fit, ot both to the Preferred setting. You can add and tweak padding using the padding property in the Horizontal Layout Group.

Why use a Horizontal Layout Group? Well, it could have been a Vertical Layout Group as well - as long as there is only a single child, they produce the same result.

###How does it work?

The Horizontal (or Vertical) Layout Group functions both as a Layout Controller and as a Layout Element. First it listens to the layout information provided by the children in the group - in this case the child Text. Then it determines how large the group must be (at minimum, and preferrably) in order to be able to contain all the children, and it functions as a Layout Element that provides this information about its minimum and preferred size.

The Content Size Fitter listens to layout information provided by any Layout Element on the same Game Object - in this case provided by the Horizontal (or Vertical) Layout Group. Depending on its settings, it then controls the size of the Rect Transform based on this information.

Once the size of the Rect Transform has been set, the Horizontal (or Vertical) Layout Group makes sure to position and size its children according to the available space. See the page about the Horizontal Layout Group for more information about how it controls the positions and sizes of its children.

##Make children of a Layout Group fit their respective sizes

If you have a Layout Group (horizontal or vertical) and want each of the UI elements in the group to fit their respective content, what do you do?

You can’t put a Content Size Fitter on each child. The reason is that the Content Size Fitter wants control over its own Rect Transform, but the parent Layout Group also wants control over the child Rect Transform. This creates a conflict and the result is undefined behavior.

However, it isn’t necessary either. The parent Layout Group can already make each child fit the size of the content. What you need to do is to disable the Child Force Expand toggles on the Layout Group. If the children are themselves Layout Groups too, you may need to disable the Child Force Expand toggles on those too.

Once the children no longer expand with flexible width, their alignment can be specified in the Layout Group using the Child Alignment setting.

What if you want some of the children to expand to fill additional available space, but not the other children? You can easily control this by adding a Layout Element component to the children you want to expand and enabling the Flexible Width or Flexible Height properties on those Layout Elements. The parent Layout Group should still have the Child Force Expand toggles disabled, otherwise all the children will expand flexibly.

###How does it work?

A Game Object can have multiple components that each provide layout information about minimum, preferred and flexible sizes. A priority system determines which values take effect over others. The Layout Element component has a higher priority than the Text, Image, and Layout Group components, so it can be used to override any layout information values they provide.

When the Layout Group listens to the layout information provided by the children, it will take the overridden flexible sizes into account. Then, when controlling the sizes of the children, it will not make them any bigger than their preferred sizes. However, if the Layout Group has the Child Force Expand option enabled, it will always make the flexible sizes of all the children be at least 1.

##More information

This page has explained solutions to a few common use cases. For a more in depth explanation of the auto layout system, see the UI Auto Layout page.