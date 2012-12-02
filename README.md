# Gradle common scripts

These scripts are meant at (further) simplifying my project build files.
Some may be useful to others, and some could deserve to be standard part of Gradle distribution.
They can be easily imported through 'apply from: <URL or local copy>'.

## task-rules.gradle

Some task rules that I find handy:

### exec

Pattern: "exec <some groovy code>": Executes the given code within a dynamic task

Sample usage:
    gradle "exec compileJava.classpath.files.each { println it }"
    gradle -Ptype=Wrapper -PgradleVersion=1.3 exec
    
Advanced usage:
    gradle -Ptype=NuGet -PdependsOn=nuget "-Pconfigure=command='push'" exec

### println

Pattern: "println <some groovy code>": Executes the given code within a dynamic task, and print the result

Sample usages:
    gradle "println convention.plugins.base.distsDir"
    gradle "println configurations"
    gradle "println tasks.jar.outputs.files.files"
    
## functions.gradle

Some functions that I find handy:

    FileCollection getTools() : returns tools.jar path for current JDK

    void replaceAssemblyAttribute(def file, String name, String value) : helper to replace Assembly attributes in C# AssemblyInfo.cs file
    
## gradle-plugin-base.gradle

Gradle plugin common build file, with the following features:
 - appends '-SNAPSHOT' to the version unless '-Prelease'
 - '-Psnapshot' enables upload to maven central snapshot repository
 - '-Prelease' enables upload to maven central staging area
 - setup sources for gradle libs in generated eclipse project
 - artifacts setup with jar, groovydoc & sources (mandatory for maven central upload)
    
## ullink-gradle-plugin-base.gradle

Specific common build file for my gradle plugins (uses the above but also sets common POM info)

## GradleDSLD.dsld.custom

A custom DSLD file for Eclipse content assist.
Far from perfect (perfection is unlikely to be achieved through DSLD for Gradle), but I find it better than the default one from SpringSource.
I hope [this annotation](http://groovy.329449.n5.nabble.com/Detailed-proposal-for-DelegatesTo-annotation-td5710777.html) will become standard to save our souls:

    
# License

All these scripts are licensed under the [Creative Commons — CC0 1.0 Universal](http://creativecommons.org/publicdomain/zero/1.0/) license with no warranty (expressed or implied) for any purpose.