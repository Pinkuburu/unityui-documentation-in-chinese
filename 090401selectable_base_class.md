# Selectable Base Class
The Selectable Class is the base class for all the interaction components and it handles the items that are in common.

可选择的类是交互的所有组件的基类，它处理的项是共同的。 

| Property:	 | Function: |
| -- | -- |
| Interactible	 | This determines if this component will accept input. When it is set to false interaction is disabled and the transition state will be set to the disabled state. |
| Transition	 | Within a selectable component there are several Transition Options depending on what state the selectable is currently in. The different states are: normal, highlighted, pressed and disabled. |
| Navigation	 | There are also a number of Navigation Options to control how keyboard navigation of the controls is implemented. |