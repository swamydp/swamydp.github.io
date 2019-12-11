---
layout: post
title: "Boolean don't care conditions"
date: 2019-12-10
---


### Boolean don't care conditions

Boolean don't care conditions may be divided into two sets. Patterns that may occur at the inputs of 
the network are *controlled* by external environment in which the network is embedded. This constraint on
the sorroundings of the network gives rise to *controllability don't care set* (CDC). 

The below figure shows a Boolean network *E3* (4-input AND gate) embedded in an environment. *E1* is the upstream logic which feeds the inputs of *E3*, while the output of *E3* feeds into the downstream logic network *E2*. Note that *E1* is *only* capable of producing inputs shown in the figure (0110, 1000, 1001, 1100). All other outputs cannot be produced by the upstream logic by design.

<img src="/images/cdc1-page-001.jpg" alt="Controllability don't cares" class="centerimage">

Hence, *E1* *controls* which Boolean inputs may be applied to *E3*. 

Consider the Boolean network below in which the downstream logic now has a single AND gate with output *O1*. The inputs are *r1* and *Y*. Hence, O1 = r1 AND Y. Note that *r1* (which feeds input *a* of the four input AND gate in *E3*, i.e, a = r1) now *controls* propagation of the input Y through the AND gate in downstream logic. 

<img src="/images/cdc2.jpg" alt="Observability don't cares" class="centerimage">

If *r1 = 1*, then O1 = <font color="red"> r1 AND Y </font> = <font color="blue"> 1 AND Y </font> = Y. However, if *r1 = 0*, then *irrespective* of the logic value of Y, O1 is 0. What is the implication of this observation ?

*a = r1* is also the input to the 4-input AND gate whose output is Y. Can the observation above be used to optimize *E3* ? Since *r1 = 0*, *a = 0*. Now, when a = 0, the logic value of Y does not matter, since the AND gate in the downstream logic prevents the propagation of Y to the output O1. Hence, Y *does not matter* means in Boolean logic jargon that Y is *don't care* when *a = 0*. Y is don't care for all the input patterns - abcd = 0XXX (0000, 00001, ..., 0111 patterns at input to *E3*). It is important to note that these don't cares arise due to *observability* of Y (for network *E3*) at output O1 AND the don't care patterns are at the input of network *E3*. This allows for optimization of network *E3* using not only the CDC patterns but also the observability don't care (*ODC*) patterns.  

CDC patterns = {0110, 1000, 1001, 1100}

ODC patterns = {0000, 00001, ..., 0111}

DC patterns for the Boolean network *E3* are induced due to upstream logic network *E1* (CDC) and downstream logic network *E2* (ODC). 

DC patterns = CDC patterns U ODC patterns = {0000, 0001, ...., 0111, 1000, 1001, 1100}

The K-map for network *E3* ignoring the up and down-stream logic is as shown below. 

<table border="1">
  <tr>
    <td>&nbsp;</td>
    <td>c'd'</td>
    <td>c'd</td>
    <td>cd</td>
    <td>cd'</td>
  </tr>
  <tr>
    <td>a'b'</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>a'b</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>ab</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>ab'</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
</table>

Considering the don't cares induced by network *E1* and *E2*, the K-map is updated as shown below.

<table border="1">
  <tr>
    <td>&nbsp;</td>
    <td>c'd'</td>
    <td>c'd</td>
    <td>cd</td>
    <td>cd'</td>
  </tr>
  <tr>
    <td>a'b'</td>
    <td>D</td>
    <td>D</td>
    <td>D</td>
    <td>D</td>
  </tr>
  <tr>
    <td>a'b</td>
    <td>D</td>
    <td>D</td>
    <td>D</td>
    <td>D</td>
  </tr>
  <tr>
    <td>ab</td>
    <td>D</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>ab'</td>
    <td>D</td>
    <td>D</td>
    <td>0</td>
    <td>0</td>
  </tr>
</table>

Optimizing the network *E3* using the don't cares yields, Y = bcd. Thus the input *a* to the 4-input AND gate is eliminated as redundant !!

In the next post, we will try to formalize the above ideas.
