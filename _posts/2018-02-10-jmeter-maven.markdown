---
layout: single
title:  "Jmeter build using Maven"
date:   2018-02-10 19:20:30 +1100
categories: tech
comments: true
classes: wide
---
<div dir="ltr" style="text-align: left;" trbidi="on">
<div class="separator" style="clear: both; text-align: center;">
<a><img border="0" src="/assets/images/jmeter.jpg"/></a></div>
<br />
<h3>POM to automatically run JMeter as part of Continuos Integration (CI)</h3>
<br />
There is not much information on the web to do the same and I had spent a significant about of effort to get it working.<br />
<br />
Hopefully, the attached pom should provide a base for anyone looking for a starting point<br />
<br />
This script assumes that you are trying to use your custom JMeter build along with plugins.<br />
<br />
{% highlight xml %}
<project xmlns="http://maven.apache.org/POM/4.0.0" 
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
        http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.test</groupId>
    <artifactId>performance-tests</artifactId>
    <packaging>pom</packaging>
    <version>1.2.0-SNAPSHOT</version>
    <name>test performance tests</name>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>chronos-jmeter-maven-plugin</artifactId>
            <version>1.1.0</version>
        </dependency>
    </dependencies>
    <reporting>
        <plugins>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>chronos-report-maven-plugin</artifactId>
                <version>1.1.0</version>
                <configuration>
                    <historydir>${project.basedir}/target/history</historydir>
                </configuration>
                <reportSets>
                    <reportSet>
                        <id>fixedloadreport</id>
                        <configuration>
                            <dataid>performancetest</dataid>
                            <reportid>jmeter-fixedload-report</reportid>
                            <title>JMeter Fixed Load Test Report</title>
                            <description>
                                <![CDATA[Fixed Load Test Report]]>
                            </description>
                        </configuration>
                        <reports>
                            <report>report</report>
                            <report>historyreport</report>
                        </reports>
                    </reportSet>
                </reportSets>
            </plugin>
        </plugins>
    </reporting>
    <build>
        <plugins>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>chronos-jmeter-maven-plugin</artifactId>
                <version>1.1.0</version>
                <configuration>
                    <jmeterhome>${project.basedir}/target/jmeter</jmeterhome>
                    <input>${project.basedir}/src/test/jmeter/main.jmx</input>
                    <heap>756m</heap>
                    <jmeterVariables>
                        <dataid>fixedloadtest</dataid>
                        <property>
                            <name>gsHost</name>
                            <value>${gsHost}</value>
                        </property>
                        <property>
                            <name>gsPort</name>
                            <value>${gsPort}</value>
                        </property>
                        <property>
                            <name>jmeter.save.saveservice.output_format</name>
                            <value>xml</value>
                        </property>
                        <property>
                            <name>gsProtocol</name>
                            <value>http</value>
                        </property>                        
                        <property>
                            <name>gsUserFilePath</name>
                            <value>${project.basedir}/in/users.csv</value>
                        </property>
                        <property>
                            <name>gsPFilePath</name>
                            <value>${project.basedir}/in/patients.csv</value>
                        </property>
                        <property>
                            <name>gsListTemplateFilePath</name>
                            <value>${project.basedir}/in/payloads/List.json</value>
                        </property>
                        <property>
                            <name>gsEnableDataPopulation</name>
                            <value>0</value>
                        </property>
                    </jmeterVariables>
                </configuration>
                <executions>
                    <execution>
                        <id>jmeter-tests</id>
                        <phase>test</phase>
                        <goals>
                            <goal>jmeter</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <artifactId>exec-maven-plugin</artifactId>
                <groupId>org.codehaus.mojo</groupId>
                <executions>
                    <execution>
                        <!-- Run our version calculation script -->
                        <id>Generate Users</id>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>exec</goal>
                        </goals>
                        <configuration>
                            <executable>
                             ${project.basedir}/lib/internal/create-and-copy-users.sh
                            </executable>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.7</version>
                <executions>
                    <execution>
                        <id>copy-resources</id>
                        <!-- here the phase you need -->
                        <phase>validate</phase>
                        <goals>
                            <goal>copy-resources</goal>
                        </goals>
                        <configuration>
                            <outputDirectory>
                                 ${project.basedir}/target/jmeter
                            </outputDirectory>
                            <resources>
                                <resource>
                                    <directory>apache-jmeter-2.13</directory>
                                    <filtering>false</filtering>
                                </resource>
                            </resources>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
        <pluginManagement>
         <plugins>
          <!--This plugin's configuration is used to store 
          Eclipse m2e settings only. It has no influence on the Maven build itself.-->
          <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
            <lifecycleMappingMetadata>
             <pluginExecutions>
              <pluginExecution>
               <pluginExecutionFilter>
                <groupId>
                 org.codehaus.mojo
                </groupId>
                <artifactId>
                 exec-maven-plugin
                </artifactId>
                <versionRange>
                 [1.4.0,)
                </versionRange>
                <goals>
                 <goal>exec</goal>
                </goals>
               </pluginExecutionFilter>
               <action>
                <ignore></ignore>
               </action>
              </pluginExecution>
             </pluginExecutions>
            </lifecycleMappingMetadata>
           </configuration>
          </plugin>
         </plugins>
        </pluginManagement>
    </build>
</project>
{% endhighlight %}
</div>
