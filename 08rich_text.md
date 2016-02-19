# Rich Text

<!--BeginSwitchLink--><!--EndSwitchLink-->
<div class="clear"></div>

The text for UI elements and text meshes can incorporate multiple font styles and sizes. Rich text is supported both for the UI System and the legacy GUI system. The Text, GUIStyle, GUIText and TextMesh classes have a <span class="doc-keyword">Rich Text</span> setting which instructs Unity to look for markup tags within the text. The [Debug.Log](../ScriptReference/Debug.Log.html) function can also use these markup tags to enhance error reports from code. The tags are not displayed but indicate style changes to be applied to the text.

## Markup format

The markup system is inspired by HTML but isn’t intended to be strictly compatible with standard HTML. The basic idea is that a section of text can be enclosed inside a pair of matching tags:-

   We are &lt;b&gt;not&lt;/b&gt; amused

As the example shows, the tags are just pieces of text inside the “angle bracket” characters, &lt; and &gt;. The text inside the tag denotes its name (which in this case is just **b**). Note that the tag at the end of the section has the same name as the one at the start but with the slash / character added. The tags are not displayed to the user directly but are interpreted as instructions for styling the text they enclose. The b tag used in the example above applies boldface to the word “not”, so the text will appear onscreen as:-

   We are **not** amused

A marked up section of text (including the tags that enclose it) is referred to as an **element**.

### Nested elements

It is possible to apply more than one style to a section of text by “nesting” one element inside another

   We are &lt;b&gt;&lt;i&gt;definitely not&lt;/i&gt;&lt;/b&gt; amused

The i tag applies italic style, so this would be presented onscreen as

   We are **_definitely not_** amused

Note the ordering of the ending tags, which is in reverse to that of the starting tags. The reason for this is perhaps clearer when you consider that the inner tags need not span the whole text of the outermost element

   We are &lt;b&gt;absolutely &lt;i&gt;definitely&lt;/i&gt; not&lt;/b&gt; amused

which gives

   We are **absolutely _definitely_ not** amused

### Tag parameters

Some tags have a simple all-or-nothing effect on the text but others might allow for variations. For example, the **color** tag needs to know which color to apply. Information like this is added to tags by the use of **parameters**:-

   We are &lt;color=green&gt;green&lt;/color&gt; with envy

Note that the ending tag doesn’t include the parameter value. Optionally, the value can be surrounded by quotation marks but this isn’t required.

## Supported tags

The following list describes all the styling tags supported by Unity.

<table>
<colgroup>
<col style="text-align:left;">
<col style="text-align:left;">
<col style="text-align:left;">
</colgroup>

<thead>
<tr>
	<th style="text-align:left;">**_Tag_**</th>
	<th style="text-align:left;">**_Description_**</th>
	<th style="text-align:left;">**_Example_**</th>
	<th style="text-align:left;">**_Notes_**</th>
</tr>
</thead>

<tbody>
<tr>
	<td style="text-align:left;">**b**</td>
	<td style="text-align:left;">Renders the text in boldface.</td>
	<td style="text-align:left;">   We are &lt;b&gt;not&lt;/b&gt; amused.</td>
	<td style="text-align:left;"></td>
</tr>
<tr>
	<td style="text-align:left;">**i**</td>
	<td style="text-align:left;">Renders the text in italics.</td>
	<td style="text-align:left;">   We are &lt;i&gt;usually&lt;/i&gt; not amused.</td>
	<td style="text-align:left;"></td>
</tr>
<tr>
	<td style="text-align:left;">**size**</td>
	<td style="text-align:left;">Sets the size of the text according to the parameter value, given in pixels.</td>
	<td style="text-align:left;">   We are &lt;size=50&gt;largely&lt;/size&gt; unaffected.</td>
	<td style="text-align:left;">Although this tag is available for Debug.Log, you will find that the line spacing in the window bar and Console looks strange if the size is set too large.</td>
</tr>
<tr>
	<td style="text-align:left;">**color**</td>
	<td style="text-align:left;">Sets the color of the text according to the parameter value. The color can be specified in the traditional HTML format. _   #rrggbbaa_ …where the letters correspond to pairs of hexadecimal digits denoting the red, green, blue and alpha (transparency) values for the color. For example, cyan at full opacity would be specified by</td>
	<td style="text-align:left;">_   &lt;color=#00ffffff&gt;…_</td>
	<td style="text-align:left;">Another option is to use the name of the color. This is easier to understand but naturally, the range of colors is limited and full opacity is always assumed. _   &lt;color=cyan&gt;…_ The available color names are given in the table below.</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="text-align:left;">
<col style="text-align:left;">
</colgroup>

<thead>
<tr>
	<th style="text-align:left;">**_Color name_**</th>
	<th style="text-align:left;">**_Hex value_**</th>
	<th style="text-align:left;">**_Swatch_**</th>
</tr>
</thead>

<tbody>
<tr>
	<td style="text-align:left;">aqua (same as cyan)</td>
	<td style="text-align:left;">`#00ffffff`</td>
	<td>![](../uploads/Main/CyanSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">black</td>
	<td style="text-align:left;">`#000000ff`</td>
	<td style="text-align:left;">![](../uploads/Main/BlackSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">blue</td>
	<td style="text-align:left;">`#0000ffff`</td>
	<td style="text-align:left;">![](../uploads/Main/BlueSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">brown</td>
	<td style="text-align:left;">`#a52a2aff`</td>
	<td style="text-align:left;">![](../uploads/Main/BrownSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">cyan (same as aqua)</td>
	<td style="text-align:left;">`#00ffffff`</td>
	<td style="text-align:left;">![](../uploads/Main/CyanSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">darkblue</td>
	<td style="text-align:left;">`#0000a0ff`</td>
	<td style="text-align:left;">![](../uploads/Main/DarkblueSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">fuchsia (same as magenta)</td>
	<td style="text-align:left;">`#ff00ffff`</td>
	<td style="text-align:left;">![](../uploads/Main/MagentaSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">green</td>
	<td style="text-align:left;">`#008000ff`</td>
	<td style="text-align:left;">![](../uploads/Main/GreenSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">grey</td>
	<td style="text-align:left;">`#808080ff`</td>
	<td style="text-align:left;">![](../uploads/Main/GreySwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">lightblue</td>
	<td style="text-align:left;">`#add8e6ff`</td>
	<td style="text-align:left;">![](../uploads/Main/LightblueSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">lime</td>
	<td style="text-align:left;">`#00ff00ff`</td>
	<td style="text-align:left;">![](../uploads/Main/LimeSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">magenta (same as fuchsia)</td>
	<td style="text-align:left;">`#ff00ffff`</td>
	<td style="text-align:left;">![](../uploads/Main/MagentaSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">maroon</td>
	<td style="text-align:left;">`#800000ff`</td>
	<td style="text-align:left;">![](../uploads/Main/MaroonSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">navy</td>
	<td style="text-align:left;">`#000080ff`</td>
	<td style="text-align:left;">![](../uploads/Main/NavySwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">olive</td>
	<td style="text-align:left;">`#808000ff`</td>
	<td style="text-align:left;">![](../uploads/Main/OliveSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">orange</td>
	<td style="text-align:left;">`#ffa500ff`</td>
	<td style="text-align:left;">![](../uploads/Main/OrangeSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">purple</td>
	<td style="text-align:left;">`#800080ff`</td>
	<td style="text-align:left;">![](../uploads/Main/PurpleSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">red</td>
	<td style="text-align:left;">`#ff0000ff`</td>
	<td style="text-align:left;">![](../uploads/Main/RedSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">silver</td>
	<td style="text-align:left;">`#c0c0c0ff`</td>
	<td style="text-align:left;">![](../uploads/Main/SilverSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">teal</td>
	<td style="text-align:left;">`#008080ff`</td>
	<td style="text-align:left;">![](../uploads/Main/TealSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">white</td>
	<td style="text-align:left;">`#ffffffff`</td>
	<td style="text-align:left;">![](../uploads/Main/WhiteSwatch.png)</td>
</tr>
<tr>
	<td style="text-align:left;">yellow</td>
	<td style="text-align:left;">`#ffff00ff`</td>
	<td style="text-align:left;">![](../uploads/Main/YellowSwatch.png)</td>
</tr>
</tbody>
</table>

**material**

This is only useful for text meshes and renders a section of text with a material specified by the parameter. The value is an index into the text mesh’s array of materials as shown by the inspector.

   We are &lt;material=2&gt;texturally&lt;/material&gt; amused

**quad**

This is only useful for text meshes and renders an image inline with the text. It takes parameters that specify the material to use for the image, the image height in pixels, and a further four that denote a rectangular area of the image to display. Unlike the other tags, quad does not surround a piece of text and so there is no ending tag - the slash character is placed at the end of the initial tag to indicate that it is “self-closing”.

   &lt;quad material=1 size=20 x=0.1 y=0.1 width=0.5 height=0.5 /&gt;

This selects the material at position in the renderer’s material array and sets the height of the image to 20 pixels. The rectangular area of image starts at given by the x, y, width and height values, which are all given as a fraction of the unscaled width and height of the texture.

## Editor GUI

Rich text is disabled by default in the editor GUI system but it can be enabled explicitly using a custom GUIStyle. The richText property should be set to true and the style passed to the GUI function in question:-

    GUIStyle style = new GUIStyle ();
    style.richText = true;
    GUILayout.Label(&quot;&lt;size=30&gt;Some &lt;color=yellow&gt;RICH&lt;/color&gt; text&lt;/size&gt;&quot;,style);
    