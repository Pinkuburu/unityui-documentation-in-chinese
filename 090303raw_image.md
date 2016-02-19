# Raw Image

The Raw Image control displays a non-interactive image to the user. This can be used for decoration, icons, etc, and the image can also be changed from a script to reflect changes in other controls. The control is similar to the Image control but does not have the same set of options for animating the image and accurately filing the control rectangle. However, the Raw Image can display any texture whilst the Image can only show a Sprite texture.

![](file:///C:/Program%20Files/Unity/Editor/Data/Documentation/en/uploads/Main/RawImageCtrlExample.png)
######A Raw Image control
##Properties


| Property:	 | Function: |
| -- | -- |
| Texture	 | The texture that represents the image to display. |
| Color	 | The color to apply to the image. |
| Material	 | The Material to use for rendering the image. |
| UV Rectangle	 | The image’s offset and size within the control rectangle, given in normalized coordinates (range 0.0 to 1.0). The edges of the image are stretched to fill the space around the UV rectangle. |
##Details

Since the Raw Image does not require a sprite texture, you can use it to display any texture available to the Unity player. For example, you might show an image downloaded from a URL using the WWW class or a texture from an object in a game.

The UV Rectangle properties allow you to display a small section of a larger image. The X and Y coordinates specify which part of the image is aligned with the bottom left corner of the control. For example, an X coordinate of 0.25 will cut off the leftmost quarter of the image. The W and H (ie, width and height) properties indicate the width and height of the section of image that will be scaled to fit the control rectangle. For example, a width and height of 0.5 will scale a quarter of the image area up to the control rectangle. By changing these properties, you can zoom and scale the image as desired (see also the Scrollbar control).