pyirt
=====

A python library of IRT algorithm designed to cope with sparse data structure.

The algorithm is described in details by Bradey Hanson(2000), see in the
literature section. We are grateful to Mr.Hanson's word.

- Current version is in early development stage. Use at your own peril.


Model Specification
===================

The current version only supports MMLE algorithm and unidimension two parameter
IRT model.

The prior distribution of theta is uniform rather than beta.


What's New
==========

IRT model is developed for offline test that has few missing data. However,
when try to calibrate item parameters for online testing bank, such assumption
breaks down and the algorithm runs into sparse data problem, as well as severe
missing data problem.

This pacakge uses list rather than matrix format to deal with sparse data.

As for now, missing data are assumed to be ignorable.


run
===
from pyirt import *

(1)load data

data, param = utl.loader.load_sim_data('pyirt/data/sim_data.txt')

(2) setup solver

model = solver.model.IRT_MMLE_2PL()

model.load_data(data)

model.load_config()

model.solve_EM()

(3) print out the result

utl.tools.parse_item_paramer(model.item_param_dict)



requirement
===========
numpy,scipy




Performance Check
=======
The likelihood is not stable in terms of converging. 
To use max iteration improve the performance compared to the MIRT package


##LAST7 example:

MIRT estimation: 
Item, slope, intercept

1 0.584 1.093 

2 0.634 0.475 

3 0.993 1.054 

4 0.452 0.286 

5 0.436 1.091 

pyirt linear constrained estimation:

0 0.61 1.12

1 0.61 -0.01

2 0.75 0.63

3 0.55 -0.24

4 0.48 1.29


pyirt likelihood convergence estimation (2 iterations):

0 0.74 1.03

1 0.73 -0.13

2 0.83 0.54

3 0.7 -0.39

4 0.63 1.2

pyirt 10 iteration estimation:

0 0.42 1.58

1 0.46 0.5

2 0.66 1.3

3 0.33 0.27

4 0.32 1.65



Problem
===========

(1) The unconstrained solver cannot handle students that have all the answers right
or all the answers wrong.

(2) The solver cannot handle polytomous answers

(3) The solver cannot handle multi-dimensional data
