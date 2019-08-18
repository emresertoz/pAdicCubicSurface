# pAdicCubicSurface
Magma package to compute lines, blow-ups, blow-downs,... for tropically smooth cubic surfaces over p-adics.

# Paper

This code performs almost everything explained in Section 4 of our joint paper with Marta Panizzut and Bernd Sturmfels. See `example_usage.mag` on how to use key functionalities.

The code will fail if the input equation for the cubic surface does not have all its lines defined over the p-adic field (for user specified p).  If the cubic surface is tropically smooth, then all its lines seem to be defined over the p-adics. See the paper cited above for the relevant discussion.
