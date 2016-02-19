<h1>Rich Text</h1>
<!--BeginSwitchLink--><!--EndSwitchLink-->
<div class="clear"></div>

<p>The text for UI elements and text meshes can incorporate multiple font styles and sizes. Rich text is supported both for the UI System and the legacy GUI system. The Text, GUIStyle, GUIText and TextMesh classes have a <span class="doc-keyword">Rich Text</span> setting which instructs Unity to look for markup tags within the text. The <a href="../ScriptReference/Debug.Log.html">Debug.Log</a> function can also use these markup tags to enhance error reports from code. The tags are not displayed but indicate style changes to be applied to the text.</p>

<h2>Markup format</h2>

<p>The markup system is inspired by HTML but isn’t intended to be strictly compatible with standard HTML. The basic idea is that a section of text can be enclosed inside a pair of matching tags:-</p>

<p>   We are &lt;b&gt;not&lt;/b&gt; amused</p>

<p>As the example shows, the tags are just pieces of text inside the “angle bracket” characters, &lt; and &gt;. The text inside the tag denotes its name (which in this case is just <strong>b</strong>). Note that the tag at the end of the section has the same name as the one at the start but with the slash / character added. The tags are not displayed to the user directly but are interpreted as instructions for styling the text they enclose. The b tag used in the example above applies boldface to the word “not”, so the text will appear onscreen as:-</p>

<p>   We are <strong>not</strong> amused</p>

<p>A marked up section of text (including the tags that enclose it) is referred to as an <strong>element</strong>.</p>

<h3>Nested elements</h3>

<p>It is possible to apply more than one style to a section of text by “nesting” one element inside another</p>

<p>   We are &lt;b&gt;&lt;i&gt;definitely not&lt;/i&gt;&lt;/b&gt; amused</p>

<p>The i tag applies italic style, so this would be presented onscreen as</p>

<p>   We are <strong><em>definitely not</em></strong> amused</p>

<p>Note the ordering of the ending tags, which is in reverse to that of the starting tags. The reason for this is perhaps clearer when you consider that the inner tags need not span the whole text of the outermost element</p>

<p>   We are &lt;b&gt;absolutely &lt;i&gt;definitely&lt;/i&gt; not&lt;/b&gt; amused</p>

<p>which gives</p>

<p>   We are <strong>absolutely <em>definitely</em> not</strong> amused</p>

<h3>Tag parameters</h3>

<p>Some tags have a simple all-or-nothing effect on the text but others might allow for variations. For example, the <strong>color</strong> tag needs to know which color to apply. Information like this is added to tags by the use of <strong>parameters</strong>:-</p>

<p>   We are &lt;color=green&gt;green&lt;/color&gt; with envy</p>

<p>Note that the ending tag doesn’t include the parameter value. Optionally, the value can be surrounded by quotation marks but this isn’t required.</p>

<h2>Supported tags</h2>

<p>The following list describes all the styling tags supported by Unity.</p>

<table>
<colgroup>
<col style="text-align:left;">
<col style="text-align:left;">
<col style="text-align:left;">
</colgroup>

<thead>
<tr>
	<th style="text-align:left;"><strong><em>Tag</em></strong></th>
	<th style="text-align:left;"><strong><em>Description</em></strong></th>
	<th style="text-align:left;"><strong><em>Example</em></strong></th>
	<th style="text-align:left;"><strong><em>Notes</em></strong></th>
</tr>
</thead>

<tbody>
<tr>
	<td style="text-align:left;"><strong>b</strong></td>
	<td style="text-align:left;">Renders the text in boldface.</td>
	<td style="text-align:left;">   We are &lt;b&gt;not&lt;/b&gt; amused.</td>
	<td style="text-align:left;"></td>
</tr>
<tr>
	<td style="text-align:left;"><strong>i</strong></td>
	<td style="text-align:left;">Renders the text in italics.</td>
	<td style="text-align:left;">   We are &lt;i&gt;usually&lt;/i&gt; not amused.</td>
	<td style="text-align:left;"></td>
</tr>
<tr>
	<td style="text-align:left;"><strong>size</strong></td>
	<td style="text-align:left;">Sets the size of the text according to the parameter value, given in pixels.</td>
	<td style="text-align:left;">   We are &lt;size=50&gt;largely&lt;/size&gt; unaffected.</td>
	<td style="text-align:left;">Although this tag is available for Debug.Log, you will find that the line spacing in the window bar and Console looks strange if the size is set too large.</td>
</tr>
<tr>
	<td style="text-align:left;"><strong>color</strong></td>
	<td style="text-align:left;">Sets the color of the text according to the parameter value. The color can be specified in the traditional HTML format. <em>   #rrggbbaa</em> …where the letters correspond to pairs of hexadecimal digits denoting the red, green, blue and alpha (transparency) values for the color. For example, cyan at full opacity would be specified by</td>
	<td style="text-align:left;"><em>   &lt;color=#00ffffff&gt;…</em></td>
	<td style="text-align:left;">Another option is to use the name of the color. This is easier to understand but naturally, the range of colors is limited and full opacity is always assumed. <em>   &lt;color=cyan&gt;…</em> The available color names are given in the table below.</td>
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
	<th style="text-align:left;"><strong><em>Color name</em></strong></th>
	<th style="text-align:left;"><strong><em>Hex value</em></strong></th>
	<th style="text-align:left;"><strong><em>Swatch</em></strong></th>
</tr>
</thead>

<tbody>
<tr>
	<td style="text-align:left;">aqua (same as cyan)</td>
	<td style="text-align:left;"><code>#00ffffff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/CyanSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">black</td>
	<td style="text-align:left;"><code>#000000ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/BlackSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">blue</td>
	<td style="text-align:left;"><code>#0000ffff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/BlueSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">brown</td>
	<td style="text-align:left;"><code>#a52a2aff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/BrownSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">cyan (same as aqua)</td>
	<td style="text-align:left;"><code>#00ffffff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/CyanSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">darkblue</td>
	<td style="text-align:left;"><code>#0000a0ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/DarkblueSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">fuchsia (same as magenta)</td>
	<td style="text-align:left;"><code>#ff00ffff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/MagentaSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">green</td>
	<td style="text-align:left;"><code>#008000ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/GreenSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">grey</td>
	<td style="text-align:left;"><code>#808080ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/GreySwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">lightblue</td>
	<td style="text-align:left;"><code>#add8e6ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/LightblueSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">lime</td>
	<td style="text-align:left;"><code>#00ff00ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/LimeSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">magenta (same as fuchsia)</td>
	<td style="text-align:left;"><code>#ff00ffff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/MagentaSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">maroon</td>
	<td style="text-align:left;"><code>#800000ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/MaroonSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">navy</td>
	<td style="text-align:left;"><code>#000080ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/NavySwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">olive</td>
	<td style="text-align:left;"><code>#808000ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/OliveSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">orange</td>
	<td style="text-align:left;"><code>#ffa500ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/OrangeSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">purple</td>
	<td style="text-align:left;"><code>#800080ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/PurpleSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">red</td>
	<td style="text-align:left;"><code>#ff0000ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/RedSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">silver</td>
	<td style="text-align:left;"><code>#c0c0c0ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/SilverSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">teal</td>
	<td style="text-align:left;"><code>#008080ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/TealSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">white</td>
	<td style="text-align:left;"><code>#ffffffff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/WhiteSwatch.png" alt=""></td>
</tr>
<tr>
	<td style="text-align:left;">yellow</td>
	<td style="text-align:left;"><code>#ffff00ff</code></td>
	<td style="text-align:left;"><img src="../uploads/Main/YellowSwatch.png" alt=""></td>
</tr>
</tbody>
</table>

<p><strong>material</strong></p>

<p>This is only useful for text meshes and renders a section of text with a material specified by the parameter. The value is an index into the text mesh’s array of materials as shown by the inspector.</p>

<p>   We are &lt;material=2&gt;texturally&lt;/material&gt; amused</p>

<p><strong>quad</strong></p>

<p>This is only useful for text meshes and renders an image inline with the text. It takes parameters that specify the material to use for the image, the image height in pixels, and a further four that denote a rectangular area of the image to display. Unlike the other tags, quad does not surround a piece of text and so there is no ending tag - the slash character is placed at the end of the initial tag to indicate that it is “self-closing”.</p>

<p>   &lt;quad material=1 size=20 x=0.1 y=0.1 width=0.5 height=0.5 /&gt;</p>

<p>This selects the material at position in the renderer’s material array and sets the height of the image to 20 pixels. The rectangular area of image starts at given by the x, y, width and height values, which are all given as a fraction of the unscaled width and height of the texture.</p>

<h2>Editor GUI</h2>

<p>Rich text is disabled by default in the editor GUI system but it can be enabled explicitly using a custom GUIStyle. The richText property should be set to true and the style passed to the GUI function in question:-</p>

<pre><code>GUIStyle style = new GUIStyle ();
style.richText = true;
GUILayout.Label(&quot;&lt;size=30&gt;Some &lt;color=yellow&gt;RICH&lt;/color&gt; text&lt;/size&gt;&quot;,style);
</code></pre>
