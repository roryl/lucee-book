#Lambdas

>Note: Lambdas are only available in Lucee 5+

Lambdas in Lucee are a more succienct syntax for creating closures and programming in a functional programming style. Consider this traditional closure:

{% gist id="roryl/115e0f98612e1334fc94549a2d3d820b",file="closure.cfm" %}{% endgist %}

When executed this will output `foo`

The same closure can be written as a lambda like so:

{% gist id="roryl/115e0f98612e1334fc94549a2d3d820b",file="lambda.cfm" %}{% endgist %}






