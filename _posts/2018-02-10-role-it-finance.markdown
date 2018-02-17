---
layout: single
title:  "Snomed-CT"
date:   2018-02-10 19:20:30 +1100
categories: general
comments: true
---
<div dir="ltr" style="text-align: left;" trbidi="on">
<div class="separator" style="clear: both; text-align: center;">
</div>
<div class="separator" style="clear: both; text-align: center;">
<a href="https://4.bp.blogspot.com/-ouj7TjCVtBE/WRGP9YmPalI/AAAAAAAARAk/4BiTRrGmsUU1QQ8wMFvIBeKexVHC5dQ0ACLcB/s1600/DSC_0687.JPG" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="https://4.bp.blogspot.com/-ouj7TjCVtBE/WRGP9YmPalI/AAAAAAAARAk/4BiTRrGmsUU1QQ8wMFvIBeKexVHC5dQ0ACLcB/s1600/DSC_0687.JPG" /></a></div>
<br />
<br />
Ever wonder why specifications from a standard body are complex? Have a look at Java Specifications or try understanding a new declarative language, they are mired in complex functionality and assumptions.<br />
<br />
A couple of years ago, I came across SNOMED-CT and found that not all specifications are made equal. Being an IT professional, I expected such kind of work from an IT major, but surprisingly it came from the medical community.<br />
<br />
SNOMED-CT is a&nbsp;specification for identifying, defining and describing medical terms. This should have been one of the complex specification in the know IT world but is one of the simplest.<br />
<br />
The authors of this specification understood the underlying structure of the data should closely represent the domain model, which is the medical terminology context. The following is the basis for the specification(I will use terminology and specification interchangeably in this blog):<br />
<br />
<ul style="text-align: left;">
<li>All components in the terminology are represented by Concepts.</li>
<li>Any relations between these concepts are defined by relationships.</li>
<li>All the components have a human/system readable description.</li>
</ul>
<div>
That's it! This is the entire gist of the specification. The underlying data structure is simple and concise and does not blur the distinction between data representation vs interpretation.</div>
<div>
<br /></div>
<div>
The goal of this article is to go through the data representation of the SNOMED-CT terminology.</div>
<div>
<br /></div>
<div>
The main Content components in SNOMED</div>
<div>
<ul style="text-align: left;">
<li>&nbsp;Concepts</li>
<li>&nbsp;Descriptions</li>
<li>&nbsp;Relationships</li>
</ul>
<div>
There are other supporting components such as</div>
</div>
<div>
<ul style="text-align: left;">
<li>Reference sets</li>
<li>Extensions</li>
</ul>
<div>
Let's go through the main concepts one by one</div>
</div>
<div>
<br /></div>
<h3 style="text-align: left;">
<b>Concept:</b>&nbsp;</h3>
<div style="text-align: left;">
<span style="font-weight: normal;">A clinical idea that is associated with a unique identifier. &nbsp;Each concept is associated with an FSN.</span></div>
<h4 style="text-align: left;">
<b>FSN(Fully Specified Name):</b><b>&nbsp;&nbsp;</b><span style="font-weight: normal;">An FSN is used to describe a clinical concept and is associated strongly&nbsp;with a concept. Each concept will have one and only one FSN in one locale. Authoritative description of the concept type.</span></h4>
<h4 style="text-align: left;">
<b>Identifier:</b><b>&nbsp;</b><span style="font-weight: normal;">A concept identifier is a numeric identifier which is up to 18 digits.&nbsp;</span></h4>
<h4 style="text-align: left;">
<span style="font-weight: normal;">Each concept is associated with one or more "description".</span></h4>
<div>
<h3 style="text-align: left;">
Description:&nbsp;</h3>
</div>
<div>
&nbsp; &nbsp; &nbsp; A description describes the associated&nbsp;concept or relationship. The relationship between description and concept is managed by a reference to the concept identifier. Similar to a Foreign Key relationship on the Concept Identifier.<br />
&nbsp; &nbsp; &nbsp; Descriptions also have a unique identifier which follows a different pattern to the concept identifier.<br />
<br />
There are different types of descriptions that can be associated with a concept.<br />
<ul style="text-align: left;">
<li>Fully Specified Name(FSN)&nbsp;</li>
<li>Synonym</li>
<li>Optional Description of other types</li>
</ul>
<div>
The description is in Unicode, so can be used to describe concepts in different locales.<br />
<br />
<h3 style="text-align: left;">
Relationship:</h3>
</div>
</div>
<div>
&nbsp; &nbsp; &nbsp; A relationship identifies the associated relationships between concepts. A relationship is identified by a unique identifier which follows a different pattern than a concept or descriptions identifier.<br />
<br />
Each relationship has a relationship type which identifies the type of relationship between two concepts. <br />
<br />
The relationship is of the form (concept)---[relationship]---(concept). The concepts are identified by the concept identifiers.<br />
<br />
<br />
<br />
<div class="separator" style="clear: both; text-align: center;">
<a href="https://confluence.ihtsdotools.org/download/attachments/26837117/logicalModel.png?version=1&amp;modificationDate=1471425689000&amp;api=v2" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="282" src="https://confluence.ihtsdotools.org/download/attachments/26837117/logicalModel.png?version=1&amp;modificationDate=1471425689000&amp;api=v2" width="640" /></a></div>
<br /></div>
<div>
For a detailed understanding of the SNOMED-CT terminology&nbsp;please visit <a href="https://confluence.ihtsdotools.org/display/DOCSTART/5.+SNOMED+CT+Logical+Model" target="_blank">SNOMED-CT tutorial</a>&nbsp;</div>
<div>
<br /></div>
In the next article, will see how to persist the Snomed data into a Graph DB.<br />
<br /></div>
