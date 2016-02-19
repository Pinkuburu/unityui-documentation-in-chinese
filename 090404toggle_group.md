# Toggle Group

A Toggle Group is not a visible UI control but rather a way to modify the behavior of a set of Toggles. Toggles that belong to the same group are constrained so that only one of them can switched on at a time - pressing one of them to switch it on automatically switches the others off.

开关切换组是不可见的 UI 控件而是在要修改的行为切换的一组（就是单选按钮）。属 于同一组的切换约束这样，只有一个人可以选择在时间-选择其中之一时将自动取消所有其 他选择。  

![](Main/UI_ToggleGroupExample.png)
######A Toggle Group
![](Main/UI_ToggleGroupInspector.png)

##Properties

| Property:	 | Function: |
| -- | -- |
| Allow Switch Off	 | Is it allowed that no toggle is switched on? If this setting is enabled, pressing the toggle that is currently switched on will switch it off, so that no toggle is switched on. If this setting is disabled, pressing the toggle that is currently switched on will not change its state. |
##Description

The Toggle Group is setup by dragging the Toggle Group object to the Group property of each of the Toggles in the group.

Toggle Groups are useful anywhere the user must make a choice from a mutually exclusive set of options. Common examples include selecting player character types, speed settings (slow, medium, fast, etc), preset colors and days of the week. You can have more than one Toggle Group object in the scene at a time, so you can create several separate groups if necessary.

Toggle Groups 切换组应用在任何地方， 用户必须作出一个选择从一组互斥的选项中。 常见的例子包括选择玩家性别类型、 速度设置 （慢，中等，速度快，等）、 预设的颜色和 星期几。

Unlike other UI elements, an object with a Toggle Group component does not need to be a child of a Canvas object, although the Toggles themselves still do.

Note that the Toggle Group will not enforce its constraint right away if multiple toggles in the group are switched on when the scene is loaded or when the group is instantiated. Only when a new toggle is swicthed on are the others switched off. This means it’s up to you to ensure that only one toggle is switched on from the beginning.