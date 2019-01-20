---
layout: single
title:  "Master Data Management in Financial sector"
date:   2018-02-10 19:20:30 +1100
categories: design
comments: true
classes: wide
---
<div dir="ltr" style="text-align: left;" trbidi="on">
<div class="separator" style="clear: both; text-align: center;">
<a><img border="0" src="/assets/images/mdm.jpg"/></a></div>
<br />
One of the problems with large banks is that they are monsters created by mergers and acquisitions.<br />
<br />
The initial plan would be to merge the software stacks in a phased manner.
<br />
<ul>
<li>Identify systems that provide common functionality.</li>
<li>Identify costs associated with maintaining and upgrading the systems and software.</li>
<li>Select a strategic platform.</li>
<li>Start your project to migrate all applications onto the strategic platform.</li>
<li>Start Phase 1</li>
<li>Get lost in business process translation.</li>
</ul>
Most of the time it is too hard to merge two software stacks and come up with a single unified strategic platform.

Higher Management would see this as a futile exercise and will take a decision to maintain the two systems and merge them in the future to save costs in the short term.<br />
<br />
Now, from a customer perspective you are a single bank, but the from the bank perspective you are a different customer in each of their systems.<br />
<br />
To simplify things, let us assume a bank which is standalone and does not have the baggage of mergers and acquisitions.

Until unless the bank is established in the 21st century the core software landscape will be a mix of modern and legacy applications.<br />
<br />
Most of the time, they will be customised 3rd party products. To make matters worse, the original product will be out of support and with zero documentation.

In this kind of setting, it would be a humongous task&nbsp;to integrate all the existing systems to provide a unified view of the customer data.<br />
<br />
A typical software landscape would be

Core Systems:<br />
<table>
<tbody>
<tr>
<td width="170"><strong>Infrastructure</strong></td>
<td width="143"><strong>&nbsp;Software</strong></td>
<td width="161">Persistence</td>
</tr>
<tr>
<td width="170"><strong>&nbsp;Mainframes, AS400</strong></td>
<td width="143">&nbsp;Cobol, CICS, IMS</td>
<td width="161">&nbsp;DB2, IMS</td>
</tr>
<tr>
<td width="170"><strong>&nbsp;Linux</strong></td>
<td width="143">&nbsp;Java, J2EE, EJB</td>
<td width="161">&nbsp;Db2, Oracle, SQL Server</td>
</tr>
<tr>
<td width="170"><strong>&nbsp;Windows</strong></td>
<td width="143">&nbsp;Seibel</td>
<td width="161">&nbsp;Oracle</td>
</tr>
<tr>
<td width="170"><strong>&nbsp;Linux</strong></td>
<td width="143">&nbsp;SAP</td>
<td width="161">&nbsp;Oracle</td>
</tr>
</tbody>
</table>
<br />
Customer and staff-facing applications:
<br />
<table>
<tbody>
<tr>
<td width="170"><strong>Infrastructure</strong></td>
<td width="143"><strong>&nbsp;Software</strong></td>
<td width="161">Persistence</td>
</tr>
<tr>
<td width="170"><strong>&nbsp;Application Servers on *nix</strong></td>
<td width="143">Java, Spring</td>
<td width="161">&nbsp;DB2,&nbsp;Oracle</td>
</tr>
<tr>
<td width="170"><strong>&nbsp;Windows</strong></td>
<td width="143">.Net</td>
<td width="161">&nbsp; SQL Server</td>
</tr>
<tr>
<td width="170"><strong>&nbsp;Browser</strong></td>
<td width="143">&nbsp;Angular, ReactJS</td>
<td width="161"></td>
</tr>
<tr>
<td width="170"><b>Mainframe</b></td>
<td width="143">&nbsp;CICS screens</td>
<td width="161">&nbsp;IMD, DB2</td>
</tr>
</tbody>
</table>
<br />
To marry all these disparate systems, the data and integration architects will most probably come up with an SOA-based application and data integration architecture.

Service Oriented Architecture works well as an application integration architecture.<br />
<br />
For example, the mainframes systems can be integrated with Java front-end system by using an Enterprise service bus or a Webservice exposed from CICS.

But the data is still restricted to the interface the core backend system exposes to the frontend.<br />
<br />
Over the course&nbsp;of time, all new requirements will be catered in the front end layer rather than making changes to the core systems. The reason can be cost, flexibility and human resource.

This leads to data fragmentation and the concept of "single source of truth" no longer applies.<br />
<br />
To counter this the organisation will create a centralised&nbsp;datawarehouse to house all organisation data. This would help in consolidating data at a single place for consumption by the organisation, but most frequently the data is not real time.

The aggregated data in Data warehouses&nbsp;would be flat, complicated and without any logical structure. This data would then be used only for offline reporting or data analysis.<br />
<br />
Even after such complex integrations and data structures, the organisation cannot make any real times decisions on the data.<br />
<br />
To solve this problem there are many products in the market which can help organisations better use their business data to achieve expected business outcomes.

Some of them are
<br />
<ol>
<li>A Hadoop cluster to house enterprise business data.</li>
<li>A real-time global commit log for stream processing.</li>
<li>A graph database/structure to house customer data along with entity relationships.</li>
<li>A NoSQL database like SAP HANA.</li>
</ol>
A typical implementation of a Master Data Management system can be as below
<br />
<ul>
<li>All enterprise data will go through a single communication highway, the Global Commit Log. In this example, I will use Apache Kafka as a distributed commit log.</li>
<li>All the systems first write any of the data updates into the commit log before clients to the log read the data and place them into their individual data stores.</li>
<li>Datawarehouse and Hadoop systems stream data from Apache Kafka at their own pace.</li>
<li>All business entities along with their relationships are moved to a global Graph Database. Example: Neo4j.</li>
<li>Any updates to the entity will be reflected in the Graph on a near real-time basis.</li>
<li>This Graph will be used for any read queries related to organisation data.</li>
<li>All updates/additions still flow through Kafka.</li>
<li>Graph queries can be cached and any updates can be propagated by a push mechanism.</li>
</ul>
<img alt="MDM.jpg" class="alignnone size-full wp-image-88" height="601" src="https://jknowblog.files.wordpress.com/2017/03/mdm.jpg" width="640" />

&nbsp;

&nbsp;</div>
