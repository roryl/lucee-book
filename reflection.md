# Reflection

With Lucee, components and Java classes can be introspected at runtime to obtain meta data about them such as their name, what functions they implement, and the properties that they have; among other data. Reflection, combined with Lucee's meta programming and mixin capability, can provide powerful runtime solutions for certain scenarios.

Use of Reflection in Lucee and modifying classes at runtime is an advanced feature and should be used only for advanced situations, as runtime modifications are not easy to track down, and can bypass much of the type system. 