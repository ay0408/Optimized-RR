# Privacy-Optimized RR for Multi-Attribute Data

This contains Python codes of our experiments on privacy level (for the entire dataset), example of real data analysis (using genome statistics), and run time.

In the evaluation of privacy level, we compared our two methods (optimal solution that solves a linear programming problem and heuristic method) with the existing Kronecker product-based method [[Wang et al., 2016](https://ceur-ws.org/Vol-1558/paper35.pdf)], when the privacy level for each attribute information is fixed. 

As an example of real data analysis, we considered the case where the privacy level for the entire dataset is fixed and evaluated the accuracy of output (differentially private) $\chi^2$-statistics in genomic statistical analysis.

We also measured the run time of our methods, and the results show that our heuristic method can be performed in about $1$ second even for a large dataset with $k = 1,000$.

## Future Directions



## Note

For details of our methods and discussion, please see our paper entitled "Privacy-Optimized Randomized Response for Multi-Attribute Data".

### Contact
Akito Yamamoto

Division of Medical Data Informatics, Human Genome Center,

the Institute of Medical Science, the University of Tokyo

a-ymmt@ims.u-tokyo.ac.jp
