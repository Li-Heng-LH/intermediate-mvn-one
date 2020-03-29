# intermediate-mvn
Walk through of Udemy tutorial: Java/Apache Maven: The Truth About Building Java Programs, and other hands on try-outs.


&nbsp;
----
### Some Learning Notes ###
##### About invalid target release error #####
* The root cause of the problem is that you have specified a higher Java version for Maven compiler plugin than what Maven knows in your system.
* A simple solution to this problem is either to reduce your target version in pom.xml 
* or install a new Java version if you want to build your project in a higher version. 
* the key to solving this problem is knowing that Maven picks the Java version from the JAVA_HOME variable and not from the PATH environment variable. 
&nbsp;

##### Project Aggregation #####
* **Project Aggregation is not Project Inheritance.** 
* To achieve project aggregation, module name = artifactId =  directory name
* **Benefits of Project Aggregation: mvn commands that run on parent will be run on children as well.**
&nbsp;
    
##### Project Inheritance Plus Project Aggregation #####
* Benefits: 
  * Avoid redundancy with inheritance
  * Mvn run on parent only
&nbsp;

##### Plugins #####
* Recommend to always run `clean` plugin before default/build lifecycle. To make sure all old stuff is cleaned up
and will not affect the new builds. 
&nbsp;

##### How to override Parent in Children? #####
* Parent: No `<dependencyManagement>` and no properties: Need to state specific dependency fully. 
* Parent: No `<dependencyManagement>` but with properties: Override properties in children. 
* Parent: With `<dependencyManagement>` but no properties: Override by specifying version number. 
* Parent: With `<dependencyManagement>` and with properties: Override properties in children.
&nbsp;

##### How to override GrandParent in Parent? #####
* GrandParent: With `<dependencyManagement>` but no properties: Override with dependency in dependencyManagement of Parent. 
* GrandParent: With `<dependencyManagement>` and with properties: Override properties in Parent. 
&nbsp;

##### Some Rules #####
* No, the property of <artifact.version> does not automatically resolve artifact version. It is just a placeholder.
* Yes, property can inherit from parent. 
* `<version>` can be inherited from `<dependencyManagement>` : if version is defined in the `<dependencyManagement>` of parent, 
 child no need to specify `<version>` in dependency. 
* Maven will pick up the nearest property definition for substitution. 
* `dependencies`: dependencies always imported.    
`dependencyManagement`: dependencies imported only when needed by children.
* In a most basic, non-inheritance project, having `dependencyManagement` only will not import the dependencies. 
&nbsp;
* Inherited dependencies counted as first level. 
* Can exclude inner dependencies layers in. 
* A has `dependencyManagement`. A is used as a dependency library. `dependencyManagement` will not work.   
`dependencyManagement` is for inheritance use.
* Dependency libraries will use the final/resultant/effective versions as well. 
* After overriding dependency library's dependency, library will pick up/use the new version and still work.       


&nbsp;
----
### Useful links ###
* [Introduction to the POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html#)
* [POM Reference](http://maven.apache.org/pom.html)
* [Setting the -source and -target of the Java Compiler](http://maven.apache.org/plugins/maven-compiler-plugin/examples/set-compiler-source-and-target.html)
* [List of Built-in Lifecycle Bindings](http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)
* [How to Fix Invalid Target Release: 1.7, 1.8, 1.9, or 1.10 Error in Maven Build](https://dzone.com/articles/how-to-fix-invalid-target-release-17-18-19-or-110)

