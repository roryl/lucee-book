# Reflection

With Lucee, components and Java classes can be introspected at runtime to obtain meta data about them such as their name, what functions they implement, and the properties that they have; among other data. Reflection, combined with Lucee's meta programming and mixin capability, can provide powerful runtime solutions for certain scenarios.

Use of Reflection in Lucee and modifying classes at runtime is an advanced feature and should be used only for advanced situations, as runtime modifications are not easy to track down, and can bypass much of the type system. 

##Reflecting/Introspecting Lucee Components
Introspecting Lucee components is accomplished with two functions in the standard library, `getMetaData()` and `getComponentMetaData()`. Both of these functions return the same data, but getMetaData operates on an instantiated class, and getComponentMetaData operates on a source file. 

Take for example the following component:

{% gist id="https://gist.github.com/roryl/2f2a68e2198d7401dd00",file="basicComponent.cfc" %}{% endgist %}

To reflect this component, instantiate it and use the getMetaData() function on it:

{% gist id="https://gist.github.com/roryl/2f2a68e2198d7401dd00",file="reflection_instantiated.cfm" %}{% endgist %}

This example above dumps the result of the metaData variable, which looks like this

>note: For conciseness, some of the data elements dumped have been hidden

![](reflection_dump.png)

Use of `getMetaData()` requires an instantiated component, which is useful when wanting to introspect a component at runtime. However it is also possible to introspect the source file of a component:

{% gist id="https://gist.github.com/roryl/2f2a68e2198d7401dd00",file="reflection_source.cfm" %}{% endgist %}

This will produce the same dump output as in the preceeding example. The string passed to getComponentMetaData() is the dot delimited path to the component. 

The reason one may use getMetaData() rather than getComponentMetaData() is when they do not know the source file of the Component being inspected, but simply have a reference to an already existing Component.

getComponentMetaData is slower than getMetaData because it must read in the source file first.