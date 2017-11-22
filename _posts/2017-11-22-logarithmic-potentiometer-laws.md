---
title: 'Modelling logarithmic potentiometer laws'
date: 2017-11-22
permalink: /posts/2017/11/logarithmic-potentiometer-laws
mathjax: true
tags:
  - curve fitting
  - circuit modelling
  - optimisation
---

## Background

Recently I have been looking at circuits with potentiometers. They are everywhere in synthesisers, guitar pedals, etc. and used for controlling aspects of circuit behaviour by changing two resistances between three points.

Potentiometers (pots for short) come in a few flavours: linear, audio, logarithmic, anti-log. This name defines how the resistance changes with respect to the position of the wiper along the track of the pot. A linear pot means that the primary resistance is proportional to the wiper position, while the secondary resistance is the remaining resistance.

$$ R_\mathrm{tot} = R_1 + R_2,\quad R_1 = \alpha R_\mathrm{tot},\quad R_2 = (1-\alpha)R_\mathrm{tot} $$

In this formulation, \\(0 \leq \alpha \leq 1 \\).

Whereas a linear potentiometer can be seen as straight, the remaining potentiometer laws are curvy. A curved mapping is useful for when controlling things such as volume, where our perception fits closely to a curve. In this post a general logarithmic form is shown that can model a variety of curves.

## General form

The general form of the curve is given by

$$ y = a\ b^x + c$$

where \\(x\\) is the wiper position, \\(y\\) is the primary resistance, and \\(a\\) \\(b\\) and \\(c\\) are free parameters for curve fitting.
