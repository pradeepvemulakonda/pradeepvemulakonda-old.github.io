---
layout: page-collection
title: 'C# for Java Developers: Types'
categories: csharp
comments: true
classes: wide
repository: pradeepvemulakonda
staticman.branch: master
---
### CLS and JVM Types:

Both specifications defines how types are declared, used, and managed in the language runtime([VES](https://en.wikipedia.org/wiki/Virtual_Execution_System), [JVM](https://en.wikipedia.org/wiki/Java_virtual_machine)) and is also an important part of the runtime's support for cross-language integration.

* Enables type safety and high performant code across platforms and languagues.
* Defines rules that the languague must follow, which ensures objects created in different languagues can intercat with each other.
  ([VB.Net](https://en.wikipedia.org/wiki/Visual_Basic_.NET) can talk to C# libraries, [Groovy](https://en.wikipedia.org/wiki/Apache_Groovy) can use Java libraries).
* Provides primitive types used in application development.

This topic contains the following sections:

* [Types](#headTypes)
* [Type definitions](#headDef)
* [Type members](#headMem)
* [Characteristics of Type members](#headChar)

#### <a name="headTypes"></a> Types

|     | Types                                                                                                       |
| --- | ----------------------------------------------------------------------------------------------------------- |
| CLR | {::nomarkdown}<li>Classes</li><li>Structures</li><li>Enumerations</li><li>Interfaces</li><li>Delegates {:/} |
| JVM | {::nomarkdown}<li>Classes</li><li>Arrays</li><li>Enumerations</li><li>Interfaces {:/}                       |

#### <a name="headDef"></a> Type definitions

Class:

<div class="ctable">
    <div class="column head">
        <div>Keyword</div>
    </div>
    <div class="column content">
        <div class="content-wrapper">
            <div>
                <div class="lang"><img alt="csharp" src="/assets/images/cs.svg"></div>
                <div class="desc">
                Class in C# is defined by the keyword 'class'
                    <div class="high-background">
                   
{% ihighlight csharp %} 
class ClassA {

}
{% endihighlight %}
                    </div> 
                </div>
            </div>
            <div>
                <div class="lang"><img alt="csharp" src="/assets/images/java.svg"></div>
                <div class="desc">
                    <div class="high-background">
{% ihighlight csharp %} 
class ClassA {
    
}
{% endihighlight %}
                    </div> 
                </div>
            </div>
        </div>
    </div>
</div>

#### <a name="headMem"></a> Type members

#### <a name="headChar"></a> Characteristics of Type members
