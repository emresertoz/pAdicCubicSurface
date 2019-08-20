# pAdicCubicSurface
Magma package to compute lines, blow-ups, blow-downs,... for tropically smooth cubic surfaces over p-adics.

# Paper

This code performs almost everything explained in Section 4 of our joint paper with Marta Panizzut and Bernd Sturmfels (https://arxiv.org/abs/1908.06106). See `example_usage.mag` on how to use key functionalities.

## Main assumption

The input cubic surface is *assumed* to have all its lines defined over the p-adic field (for user specified p). An error will occur if this is not the case. If the cubic surface is tropically smooth, then this assumption seems to hold. See the paper cited above for the relevant discussion.

# Main usage

In Magma, attach the package:

    Magma> Attach("blowdown.mag");

Specify a prime and a cubic quaternary form:

    Magma> p:=5;
    Magma> f:=3125*w^3 + 25*w^2*x + 25*w^2*y + 5*w^2*z + 25*w*x^2 + w*x*y + w*x*z + 25*w*y^2 + w*y*z + 5*w*z^2 + 3125*x^3 + 5*x^2*y + 25*x^2*z + 5*x*y^2 + x*y*z + 25*x*z^2 + 3125*y^3 + 25*y^2*z + 25*y*z^2 + 3125*z^3;

Now the main function `pAdicCubicSurface` builds a record storing the lines and other data induced from them:

    Magma> S:=pAdicCubicSurface(f,p);

There is a certain amount of randomness involved, in case of failure try again, or increase precision:

    Magma> S:=pAdicCubicSurface(f,p : precision:=5000);

The cubics defining `P2 - -> S`, and the valuation of their coefficients, can be viewed as follows,

    Magma> S`blowup_cubics;
    Magma> [valuation_of_form(form) : form in S`blowup_cubics];

The six base points in `P2` and their valuations:
    
    Magma> pts:=blowdown_lines(S`marking); 
    Magma> [[Valuation(p) : p in pt] : pt in pts];

Tree statistics are obtained as below:
  
    Magma> splits:=[tropicalize_line_in_cubic(S,i) : i in [1..27]]; [#s : s in splits];
    Magma> SetToMultiset([encode_split(split) : split in splits]);

You can also "perturb" the six base points in P2, and the cubics passing through them appropriately to get everything to be over the rationals, while preserving the combinatorial type of the cubic surface:

    Magma> g,newpts,cubs,err:=perturb(S,14 : internal_precision:=20); 

Here `g` is the new cubic surface, `newpts` are the six new points in `P2` rounded from the old ones while keeping `14` digits of p-adic presecision, `cubs` are the cubic curves through them and `err` is the difference in the valuation of the coefficients of `g` and `f`. If `err` is not zero, try again by increasing the two precisions `14` and `20`; the former governs the height of the points and the latter the height of the cubic curves through them.
