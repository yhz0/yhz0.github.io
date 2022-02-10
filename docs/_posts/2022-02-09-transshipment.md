---
layout: post
date: 2022-02-09 09:46:36
title: "Transshipment Problem Papers"
katex: true
---

Link to papers:

- L. Zhao and S. Sen, "A Comparison of Sample-Path-Based Simulation-Optimization and Stochastic Decomposition for Multi-Location Transshipment Problems," Proceedings of the 2006 Winter Simulation Conference, 2006, pp. 238-245, doi: 10.1109/WSC.2006.323079. [Link](https://doi.org/10.1109/WSC.2006.323079)
- Herer et al., "The multilocation transshipment problem" [Link](https://doi.org/10.1080/07408170500434539)

## Introduction

These two papers are investigating a multi-location single-commodity transshipment problem. Herer's paper formulates the problem (link above). I summarize the model he proposes as follows.

1. One supplier; N retailers at stocking locations. One kind of commodity.
2. At the beginning of each period, there is a known initial inventory level for each retailer (from the previous period).
3. Now we have an estimate distribution of the demands at each retailer. We now need to decide on how much to order at each location.
4. Replenishment arrive at retailers to meet the backlogged orders. The remaining goes to the inventory at the retailer.
5. A demand is observed at each location.
6. The system is allowed to redistribute its inventory on a transshipment network to better meet the demand. For each unit of inventory moved on an edge $ij$, there is a cost $c_{ij}$.
7. The retailer meets demand at each location. If demand at a location $i$ cannot be met, it is backlogged and penalized with a unit cost of $p_i$. If there is a surplus at a location, it is charged a holding cost of $h_i$ per unit, and rolls to the next period.

A more detailed formulation can be found in Zhao's paper (1a)-(1d) and (2).

Herer has shown that:

    Under stationarity and non-shortage inducing policies, there exists an optimal order-up-to policy $s_i$.

In showing this, Herer constructed another system, that differs from the original system in only two aspects:

    1. At the end of the period, after holding and shortage costs are incurred, a retailer can either purchase or sell stock back to the supplier for the same price the stock can purchased at the beginning of the period.
    2. The stock level at each retailer at the end of the period is constrained to be zero, i.e., no inventory and no back-orders are allowed.

I would call that this system has the "reset" property. Then Herer proceeds to prove that each policy in the original system can be mapped to the new system with identical cost. As a corollary, we do not need to care about the future inventory level, and simplify the problem into optimizing the cost in the current period. The simplified problem has an elegant optimal policy: order-up-to $S$ policy.  This is a key result that allows us to avoid a multi-stage problem, effectively replacing it with a two-stage SLP, to find the optimal "order-up-to" level.

## Solution methods

Herer used a sample-path based method IPA to solve the problem. Zhao and Sen then suggested two methods to solve this SLP: Stochastic Quasi-Gradient (SQG) and Stochastic Decomposition (SD), claims IPA and SQG are equivalent for the transshipment problem.

Computational results show that SD is faster for this problem.

## My thoughts

This is an instance where a multi-stage problem is reduced to a two-stage problem. During my meeting with prof Sen, I agree that two-stage problems are more tractable, more stable and simpler than multi-stage ones. So we would like to know how to identify those problems that can be, in fact, solved (or well approximated) by a two-stage problem. In the dynamic programming world, Rollout Algorithm is a heuristic to the original DP problem. We ask: when is it a good solution?

Another task is to formalize the proof outlined in the Herer's paper, in the language of dynamic programming. Herer's proof is mostly ad hoc. Can it be generalized to other dynamic programming instances? For example, [this instance](https://connect.informs.org/communities/community-home/digestviewer/viewthread?GroupId=469&MessageKey=53d7e975-995a-4cae-8606-e03d699d9cab&CommunityKey=1d5653fa-85c8-46b3-8176-869b140e5e3c&tab=digestviewer) has a similar property, namely that a two-stage program approximates the original problem very well, and in fact, can be proven optimal under some reasonable assumptions. Both proofs follow similar outlines, with the "reset" property being the key idea. Yet we have not formalized this "reset" property. This will be left to a future post.
