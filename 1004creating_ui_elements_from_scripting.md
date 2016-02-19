# Creating UI elements from scripting

If you are creating a dynamic UI where UI elements appear, disappear, or change based on user actions or other actions in the game, you may need to make a script that instantiates new UI elements based on custom logic.

如果您正在创建动态 UI,  在游戏中 UI 元素在哪里出现、 消失，或更改基于用户操作 或其他操作，你可能需要做一个脚本，实例化新 ui 元素基于自定义的逻辑。 

##Creating a prefab of the UI element

In order to be able to easily instantiate UI elements dynamically, the first step is to create a prefab for the type of UI element that you want to be able to instantiate. Set up the UI element the way you want it to look in the Scene, and then drag the element into the Project View to make it into a prefab.

为了能轻松地动态地实例化 UI 元素，第一步是创建一个 UI 元素的类型的预置体，是 你想要能够实例化的。设置用户界面元素，你想要它在场景中，看起来的方式，然后将该元 素拖到 Project View 项目视图，使它变成一个预置体。 

For example, a prefab for a button could be a Game Object with a Image component and a Button component, and a child Game Object with a Text component. Your setup might be different depending on your needs.

例如，一个按钮的预置体可能是一个游戏对象与 Image 图像组件和一个 Button 按钮组 件和一个子游戏对象具有 Text 组件。您可以设置不同的根据您的需求。

You might wonder why we don’t have a API methods to create the various types of controls, including visuals and everything. The reason is that there are an infinite number of way e.g. a button could be setup. Does it use an image, text, or both? Maybe even multiple images? What is the text font, color, font size, and alignment? What sprite or sprites should the image use? By letting you make a prefab and instantiate that, you can set it up exactly the way you want. And if you later want to change the look and feel of your UI you can just change the prefab and then it will be reflected in your UI, including the dynamically created UI.

你可能想知道为什么我们没有 API 方法来创建各种类型的控件，包括视觉效果和一切。 原因是这个方式有无限多的。如一个按钮可以 setup。它 可能是一个图像、 文本或两者都有？ 也许甚至是多个图像？文本的字体、 颜色、 字体大小和对齐方式是什么？图像应使用什么 精灵？通过让你创建一个预置和实例化的您可以设置它正是你想要的方式。如果您以后想要 更改您的用户界面的外观和感觉您只可以更改预置，然后，它将会反映在您的 UI，包括动 态创建用户界面。 

##Instantiating the UI element

Prefabs of UI elements are instantiated as normal using the Instantiate method. When setting the parent of the instantiated UI element, it’s recommended to do it using the Transform.SetParent method with the worldPositionStays parameter set to false.

UI 元素的预置体都作为正常使用 Instantiate 方法来进行实例化。在实例化时设置 UI 元 素的父对象是什么，它建议使用 Transform.SetParent 方法设置和 worldPositionStays 参数设 置为 false。 

##Positioning the UI element

A UI Element is normally positioned using its Rect Transform. If the UI Element is a child of a Layout Group it will be automatically positioned and the positioning step can be skipped.

When positioning a Rect Transform it’s useful to first determine it has or should have any stretching behavior or not. Stretching behavior happens when the anchorMin and anchorMax properties are not identical.

For a non-stretching Rect Transform, the position is set most easily by setting the anchoredPosition and the sizeDelta properties. The anchoredPosition specifies the position of the pivot relative to the anchors. The sizeDelta is just the same as the size when there’s no stretching.

For a stretching Rect Transform, it can be simpler to set the position using the offsetMin and offsetMax properties. The offsetMin property specifies the corner of the lower left corner of the rect relative to the lower left anchor. The offsetMax property specifies the corner of the upper right corner of the rect relative to the upper right anchor.

##Customizing the UI Element

If you are instantiating multiple UI elements dynamically, it’s unlikely that you’ll want them all to look the same and do the same. Whether it’s buttons in a menu, items in an inventory, or something else, you’ll likely want the individual items to have different text or images and to do different things when interacted with.

This is done by getting the various components and changing their properties. See the scripting reference for the Image and Text components, and for how to work with UnityEvents from scripting.