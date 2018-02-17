---
layout: single
title:  "Jmeter build using Maven"
date:   2018-02-10 19:20:30 +1100
categories: tech
comments: true
---
<div dir="ltr" style="text-align: left;" trbidi="on">
<div class="separator" style="clear: both; text-align: center;">
<a><img border="0" src="/assets/images/jmeter.jpg"/></a></div>
<br />
Recently I had a requirement to run JMeter scripts in Jenkins/bamboo.<br />
<br />
There is not much information on the web to do the same and I had to spend a significant about off effort to get it working.<br />
<br />
Hopefully, the attached pom should help anyone trying to setup a Jenkins/bamboo build.<br />
<br />
This script assumes that you are trying to use your custom build of JMeter along with plugins. Even though you might not need everything in the pom the dependencies and the attributes that you can set will give you an idea to enhance the pom as required.<br />
<br />
Will update the page with more explanation once I get some time.<br />
<br />
<pre class="a-c-x-Ha a-c-Ma-td-Ib" style="-webkit-user-select: text; background-color: white; font-family: 'Courier New', Courier, monospace, arial, sans-serif; font-size: 14px; white-space: pre-wrap; word-wrap: break-word;">&lt;project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd"&gt;
    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;
    &lt;groupId&gt;com.test&lt;/groupId&gt;
    &lt;artifactId&gt;performance-tests&lt;/artifactId&gt;
    &lt;packaging&gt;pom&lt;/packaging&gt;
    &lt;version&gt;1.2.0-SNAPSHOT&lt;/version&gt;
    &lt;name&gt;test performance tests&lt;/name&gt;
    &lt;dependencies&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;junit&lt;/groupId&gt;
            &lt;artifactId&gt;junit&lt;/artifactId&gt;
            &lt;version&gt;3.8.1&lt;/version&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.codehaus.mojo&lt;/groupId&gt;
            &lt;artifactId&gt;chronos-jmeter-maven-plugin&lt;/artifactId&gt;
            &lt;version&gt;1.1.0&lt;/version&gt;
        &lt;/dependency&gt;
    &lt;/dependencies&gt;
    &lt;reporting&gt;
        &lt;plugins&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.codehaus.mojo&lt;/groupId&gt;
                &lt;artifactId&gt;chronos-report-maven-plugin&lt;/artifactId&gt;
                &lt;version&gt;1.1.0&lt;/version&gt;
                &lt;configuration&gt;
                    &lt;historydir&gt;${project.basedir}/target/history&lt;/historydir&gt;
                &lt;/configuration&gt;
                &lt;reportSets&gt;
                    &lt;reportSet&gt;
                        &lt;id&gt;fixedloadreport&lt;/id&gt;
                        &lt;configuration&gt;
                            &lt;dataid&gt;performancetest&lt;/dataid&gt;
                            &lt;reportid&gt;jmeter-fixedload-report&lt;/reportid&gt;
                            &lt;title&gt;JMeter Fixed Load Test Report&lt;/title&gt;
                            &lt;description&gt;
                                &lt;![CDATA[Fixed Load Test Report]]&gt;
                            &lt;/description&gt;
                        &lt;/configuration&gt;
                        &lt;reports&gt;
                            &lt;report&gt;report&lt;/report&gt;
                            &lt;report&gt;historyreport&lt;/report&gt;
                        &lt;/reports&gt;
                    &lt;/reportSet&gt;
                &lt;/reportSets&gt;
            &lt;/plugin&gt;
        &lt;/plugins&gt;
    &lt;/reporting&gt;
    &lt;build&gt;
        &lt;plugins&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.codehaus.mojo&lt;/groupId&gt;
                &lt;artifactId&gt;chronos-jmeter-maven-plugin&lt;/artifactId&gt;
                &lt;version&gt;1.1.0&lt;/version&gt;
                &lt;configuration&gt;
                    &lt;jmeterhome&gt;${project.basedir}/target/jmeter&lt;/jmeterhome&gt;
                    &lt;input&gt;${project.basedir}/src/test/jmeter/main.jmx&lt;/input&gt;
                    &lt;heap&gt;756m&lt;/heap&gt;
                    &lt;jmeterVariables&gt;
                        &lt;dataid&gt;fixedloadtest&lt;/dataid&gt;
                        &lt;property&gt;
                            &lt;name&gt;gsHost&lt;/name&gt;
                            &lt;value&gt;${gsHost}&lt;/value&gt;
                        &lt;/property&gt;
                        &lt;property&gt;
                            &lt;name&gt;gsPort&lt;/name&gt;
                            &lt;value&gt;${gsPort}&lt;/value&gt;
                        &lt;/property&gt;
                        &lt;property&gt;
                            &lt;name&gt;jmeter.save.saveservice.output_format&lt;/name&gt;
                            &lt;value&gt;xml&lt;/value&gt;
                        &lt;/property&gt;
                        &lt;property&gt;
                            &lt;name&gt;gsProtocol&lt;/name&gt;
                            &lt;value&gt;http&lt;/value&gt;
<span style="font-size: 14px;">&lt;/property&gt;</span>                        &lt;property&gt;
                            &lt;name&gt;gsUserFilePath&lt;/name&gt;
                            &lt;value&gt;${project.basedir}/in/users.csv&lt;/value&gt;
                        &lt;/property&gt;
                        &lt;property&gt;
                            &lt;name&gt;gsPFilePath&lt;/name&gt;
                            &lt;value&gt;${project.basedir}/in/patients.csv&lt;/value&gt;
                        &lt;/property&gt;
                        &lt;property&gt;
                            &lt;name&gt;gsListTemplateFilePath&lt;/name&gt;
                            &lt;value&gt;${project.basedir}/in/payloads/List.json&lt;/value&gt;
                        &lt;/property&gt;
                       
                        &lt;property&gt;
                            &lt;name&gt;gsEnableDataPopulation&lt;/name&gt;
                            &lt;value&gt;0&lt;/value&gt;
                        &lt;/property&gt;
                    &lt;/jmeterVariables&gt;
                &lt;/configuration&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;id&gt;jmeter-tests&lt;/id&gt;
                        &lt;phase&gt;test&lt;/phase&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;jmeter&lt;/goal&gt;
                        &lt;/goals&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
            &lt;/plugin&gt;
            &lt;plugin&gt;
                &lt;artifactId&gt;exec-maven-plugin&lt;/artifactId&gt;
                &lt;groupId&gt;org.codehaus.mojo&lt;/groupId&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;!-- Run our version calculation script --&gt;
                        &lt;id&gt;Generate Users&lt;/id&gt;
                        &lt;phase&gt;generate-sources&lt;/phase&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;exec&lt;/goal&gt;
                        &lt;/goals&gt;
                        &lt;configuration&gt;
                            &lt;executable&gt;${project.basedir}/lib/internal/create-and-copy-users.sh&lt;/executable&gt;
                        &lt;/configuration&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
            &lt;/plugin&gt;
            &lt;plugin&gt;
                &lt;artifactId&gt;maven-resources-plugin&lt;/artifactId&gt;
                &lt;version&gt;2.7&lt;/version&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;id&gt;copy-resources&lt;/id&gt;
                        &lt;!-- here the phase you need --&gt;
                        &lt;phase&gt;validate&lt;/phase&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;copy-resources&lt;/goal&gt;
                        &lt;/goals&gt;
                        &lt;configuration&gt;
                            &lt;outputDirectory&gt;${project.basedir}/target/jmeter&lt;/outputDirectory&gt;
                            &lt;resources&gt;
                                &lt;resource&gt;
                                    &lt;directory&gt;apache-jmeter-2.13&lt;/directory&gt;
                                    &lt;filtering&gt;false&lt;/filtering&gt;
                                &lt;/resource&gt;
                            &lt;/resources&gt;
                        &lt;/configuration&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
            &lt;/plugin&gt;
        &lt;/plugins&gt;
        &lt;pluginManagement&gt;
         &lt;plugins&gt;
          &lt;!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.--&gt;
          &lt;plugin&gt;
           &lt;groupId&gt;org.eclipse.m2e&lt;/groupId&gt;
           &lt;artifactId&gt;lifecycle-mapping&lt;/artifactId&gt;
           &lt;version&gt;1.0.0&lt;/version&gt;
           &lt;configuration&gt;
            &lt;lifecycleMappingMetadata&gt;
             &lt;pluginExecutions&gt;
              &lt;pluginExecution&gt;
               &lt;pluginExecutionFilter&gt;
                &lt;groupId&gt;
                 org.codehaus.mojo
                &lt;/groupId&gt;
                &lt;artifactId&gt;
                 exec-maven-plugin
                &lt;/artifactId&gt;
                &lt;versionRange&gt;
                 [1.4.0,)
                &lt;/versionRange&gt;
                &lt;goals&gt;
                 &lt;goal&gt;exec&lt;/goal&gt;
                &lt;/goals&gt;
               &lt;/pluginExecutionFilter&gt;
               &lt;action&gt;
                &lt;ignore&gt;&lt;/ignore&gt;
               &lt;/action&gt;
              &lt;/pluginExecution&gt;
             &lt;/pluginExecutions&gt;
            &lt;/lifecycleMappingMetadata&gt;
           &lt;/configuration&gt;
          &lt;/plugin&gt;
         &lt;/plugins&gt;
        &lt;/pluginManagement&gt;
    &lt;/build&gt;
&lt;/project&gt;</pre>
</div>
