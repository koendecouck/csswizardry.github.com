---
layout: post
title: "Portfolio Template"
meta: "portfolio-template"
permalink: /case-studies/portfolio-template/
next-case-study-title: "3D printed MRI data"
next-case-study-url: /case-studies/20140809-3dprintedbrain/
hide-hire-me-link: true
---

<p><strong>Screenshots</strong></p>
<p><strong>Artifacts</strong></p>
<p><strong>Tagline</strong></p>
<p><strong>(Build time)</strong></p>
<p><strong>Challenge</strong></p>
<p><strong>Criteria for success</strong></p>
<p><strong>Process</strong></p>
<p><strong>Results</strong></p>
<p><strong>Future work</strong></p>
<p><strong>Final thoughts</strong></p>

--------------------------------------------------------------------------
<p><strong>Skeleton structure</strong></p>
<p>The following is a suggested structure reverse-engineered from Pat. A full project description includes all sections, although older projects may have a reduced number. The sections are placed in order of importance. If sections need to be dropped one should start at the bottom with the least important part (Final thoughts) and work their way up. 'Project Summary' is an all-caps, higher level title.</p>
<p>My own adaptation takes some inspiration from APA style journal articles (abstract, intro, methods, results, future work). I chose to replace the academic term 'introduction' or the engineering term 'problem' by 'Challenge'.</p>

<table style="width:800px">
<tr>
  <td>Source</td>
  <td>My adaptation</td> 
</tr>
<tr>
  <td>PROJECT SUMMARY</td>
  <td>Project description (separate field)</td> 
</tr>
<tr>
  <td>The problem</td>
  <td>Challenge</td> 
</tr>
<tr>
  <td>Defining criteria for success</td>
  <td>Criteria for success</td> 
</tr>
<tr>
  <td>Moving forward</td>
  <td>Process</td> 
</tr>
<tr>
  <td>How it all turned out</td>
  <td>Results</td> 
</tr>
<tr>
  <td>Room for future improvement</td>
  <td>Future work</td> 
</tr>
<tr>
  <td>Final thoughts</td>
  <td>Final thoughts</td> 
</tr>
</table>

<p><strong>Screenshots & Artifacts</strong></p>
<strong>Screenshots</strong> seem to be included as right-aligned screenshot thumbnails (75x75 px), that expand when clicked. The images are part of an image slider specific to each project.

<strong>Artifacts</strong> include a number a download links to project deliverables. These documents are hosted on Google Drive and publicly viewable.

--------------------------------------------------------------------------


<p><strong>Visual versus Text editor</strong></p>
<p>Use the Text mode of the Wordpress editor as your default for writing posts and pages. The visual editor likes to mess you up with empty divs, spaces (both of which are ignored anyway) and random acts of Vandalism. Make sure the visual editor is disabled through Users -> User profile. Note how a section title is bold and considered a separate paragraph.</p>

<p><strong>Understanding paragraphs and linebreaks</strong></p>
<p>Type your texts in posts properly by removing div tags (how they did they even get there in the first place?) and wrap your text in paragraph tags (p). Linebreaks are achieved by typing a single br/ element. The br/ tag is useful for separating images (and their captions) from paragraphs. It can also be used to write addresses or poems. It should <em>not</em> be used to separate paragraphs.</p> 

<p>This paragraph is separated by an empty line. This is because of <strong>paragraph wrapper tags (p)</strong>. WordPress's visual editor is supposed to automatically converts line breaks into paragraphs and new lines into line breaks (br/). But that cr*p doesn't seem to work. Instead take a look at these paragraphs which all are separately wrapped in paragraph tags. Here is a hyperlink for show <a href="http://blogs.uw.edu/hcdelabs/labs/lute/">UW LUTE lab</a>. The visual editor can be disabled through Users -> User profile.</p> 

<p><strong>Inserting Images in posts</strong></p>
Make sure that the source image is 800px wide. Insert as original size, central alignment. Use caption wrappers. Align the caption central as well, while ordinary text is left aligned. Notice the two br/ elements which create a break both before and after the image.</p>

<br/>
<div style="text-align: center;"><a href="/_post_images/2014/04/forced_alinea.png"><img class="aligncenter" alt="Naamloos3x" src="/_post_images/2014/08/Naamloos3x.png" width="800" height="401" /></a>[caption]This image source is 800px and scales correctly on mobile. The picture and caption are centrally aligned.[/caption]</div>
<br/>

<div style="text-align: left;">There is an invisible <strong>br/ tag</strong> above this paragraph which separates the image tagline from this left aligned paragraph.</div>
<div style="text-align: left;">This is an example of a paragraph following another paragraph. It is again left aligned. Using 'enter' to separate paragraphs unfortunately doesn't work (Wordpress editor removes those extra spaces). Instead in the html view you <em>could</em> force them apart by typing a br/ tag for line breaks. The br/ tag is useful for writing addresses or poems, but is not intended to separate paragraphs.</div>

<div><a style="text-align: center; line-height: 1.5em;" href="/_post_images/2014/04/forced_alinea.png"><img class="alignnone size-full wp-image-4142" src="/_post_images/2014/04/forced_alinea.png" width="1" height="36" /></a></div>

<p>There is an invisible <strong>1px wide image</strong> above this paragraph which separates it from the previous paragraph. This is an old, crude hack and terrible practice but it does work.</p>

<p><strong>Captions</strong></p>
<p>Use caption tags for image captions. Even though there doesn't seem to be any advantage to using them (other than cleaner code).</p>

<br/>
<div style="text-align: center;"><a href="/_post_images/2014/04/forced_alinea.png"><img class="aligncenter" alt="Naamloos3x" src="/_post_images/2014/08/Naamloos3x.png" width="800" height="401" /></a>This image does not use captions.</div>
<br/>
<div style="text-align: center;"><a href="/_post_images/2014/04/forced_alinea.png"><img class="aligncenter" alt="Naamloos3x" src="/_post_images/2014/08/Naamloos3x.png" width="800" height="401" /></a>[caption]This image does use captions.[/caption]</div>
<br/>

<p><strong>Unordered list with bullet points</strong></p>
<p>This is the text that goes above the bullet point list. The following is the list itself, wrapped in <strong>u1 tags</strong>:</p>
<ul>
	<li>A white line is automatically inserted before the first list item.</li>
	<li>Each new list item is wrapped in li tags.</li>
	<li>A white line is automatically inserted after the last list item.</li>
</ul>
<p><strong>Unordered list with USCI characters</strong></p>
<p>The following also looks like an bullet point item list, even though it doesn't use u1 tags. It doesn't even use linebreaks (br/). Instead it looks like hyperlinks automatically act as linebreaks when arranged after eachother.</p>
* <a href="http://goo.gl/D4DPoV">Preliminary Cloud Storage study proposal</a>
* <a href="http://goo.gl/jHybLv">Cloud Storage Interaction Map</a>
* <a href="http://goo.gl/qgtw3k">Cloud Storage Initial Study Plan</a>
* <a href="http://goo.gl/7uCtcz">Cloud Storage Study Testing Kit</a>
* <a href="http://goo.gl/NXxm8m">Findings &amp; Recommendations Presentation</a></div>

---

{% include promo-next.html %}
