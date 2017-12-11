---
title: 'Modelling logarithmic potentiometer laws'
date: 2017-11-22
permalink: /posts/2017/11/logarithmic-potentiometer-laws
mathjax: true
tags:
  - curve fitting
  - circuit modelling
  - optimisation
  - micro-research
  - electronics
---

This post presents a general logarithmic potentiometer law with a curve fit to enable a user to choose a curve that sounds good in their application. The law is computationally expensive as it involves an exponent but is good in terms of flexibility.

## Background

Recently I have been looking at circuits with potentiometers. They are everywhere in synthesisers, guitar pedals, etc. and used for controlling aspects of circuit behaviour by changing two resistances between three points.

Potentiometers (pots for short) come in a few flavours: linear, logarithmic, and anti-log. This name defines how the resistance changes with respect to the position of the wiper along the track of the pot. A linear pot means that the primary resistance is proportional to the wiper position, while the secondary resistance is the remaining resistance.

$$ R_\mathrm{tot} = R_1 + R_2,\quad R_1 = \alpha R_\mathrm{tot},\quad R_2 = (1-\alpha)R_\mathrm{tot} $$

In this formulation, \\(0 \leq \alpha \leq 1 \\).

Whereas a linear potentiometer can be seen as straight, the remaining potentiometer laws are curvy. A curved mapping is useful for when controlling things such as volume, where our perception fits closely to a curve. The definition of the exact curve of a potentiometer is difficult to pin down as they differ with manufacturer and also price. For use in simulation, we can define a set of curves that a user can choose from for their needs.

## Logarithmic general form

The general form of the curve is given by

$$ y = a\ b^x + c$$

where \\(x\\) is the wiper position, \\(y\\) is the primary resistance, and \\(a\\), \\(b\\) and \\(c\\) are free parameters for curve fitting.

This mapping is applied prior to calculating resistances, so will effectively map \\(x\\) to \\(\alpha\\), i.e. \\(y=\alpha\\). For this reason it can be assumed that the limits of both \\(x\\) and \\(y\\) are zero and one. To fit this curve we then have two equations, when both \\(x\\) and \\(y\\) are 0:

$$ 0 = a + c,\quad c = -a $$

And therefore we are given a simpler equation with only two parameters:

$$ y = a\ b^x - a $$

Constraining with our second set of points:

$$ 1 = ab - a,\quad \frac{1}{b-1} = a $$

There is still one equation left to determine the parameter values. I find it useful to map this as a mid-point of the curve, for example saying that when the wiper is at half way I want the resistance to be at 10% of the total. This can be parameterised again so that we can change the midpoint, saying \\(x = 0.5\\), \\(y = y_m\\). This gives our final constraint

$$ y_m = a(\sqrt{b} - 1),\quad y_m = \frac{\sqrt{b} - 1}{b-1},\quad b = \left(\frac{1}{y_m} - 1\right)^2 $$

## Results

By setting the value for \\(y_m\\) we can create a variety of mappings:

<div>
    <a href="https://plot.ly/~benholmes/4/?share_key=8cPOlabSsDaHuJ2drdG1CG" target="_blank" title="log-pot" style="display: block; text-align: center;"><img src="https://plot.ly/~benholmes/4.png?share_key=8cPOlabSsDaHuJ2drdG1CG" alt="log-pot" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="benholmes:4" sharekey-plotly="8cPOlabSsDaHuJ2drdG1CG" src="https://plot.ly/embed.js" async></script>
</div>


[//]: # ![Logarithmic potentiometer laws](/images/log-pot-mappings.png)

Note that when setting \\(y_m = 0.5\\) that \\(b = \infty\\)! But for this value we can just use a linear map so no need to waste the computation time for the exponent.

Choosing for example \\(y_m = 0.15\\) will give quite a good approximation of a log pot, though I say this without measurements or further evidence. For an anti-log pot one could select a value around \\(0.85\\).

If you're interested in further playing around with this, here is the MATLAB gist (although it should be fairly compatible to Octave, and also self-explanatory if you want to port it):

<script src="https://gist.github.com/bencholmes/87ceeaee702ec0dc1d0426283d2ae2f6.js"></script>
