# Privacy-Optimized RR for Multi-Attribute Data

This contains Python codes of our experiments on privacy level (for the entire dataset), example of data analysis (using genome statistics), and run time.

In the evaluation of privacy level, we compared our two methods (optimal solution that solves a linear programming problem and heuristic method) with the existing Kronecker product-based method [[Wang et al., 2016](https://ceur-ws.org/Vol-1558/paper35.pdf)], when the privacy level for each attribute information is given. 

As an analysis example using our method, we considered the case where the privacy level for the entire dataset is fixed and evaluated the accuracy of output (differentially private) $\chi^2$-statistics in genomic statistical analysis.

The run time results show that our heuristic method can be performed in about $1$ second even for a large dataset with $k = 1,000$. In Run Time folder, we also provide the results when $k = 10,000$ and $k = 100,000$ for reference.

## One Possible Policy to Distribute Privacy Budgets

Set the minimum privacy level to be guaranteed for each of the $k$-attribute information as $\epsilon_1, \epsilon_2, \dots, \epsilon_k$, respectively. Under this condition, consider increasing the accuracy of data analysis as much as possible, when the privacy level for the entire dataset is fixed.

1. If $\epsilon_1, \epsilon_2, \dots, \epsilon_k$ are all distributable, distribute as is.
2. If not distributable, prioritize reducing the budget for information that does not require a high degree of accuracy or that can be expected to be accurate even with a small $\epsilon$. (Distibute a budget of almost $\epsilon_i$ as much as possible for information that requires a high degree of accuracy.)
3. Ultimately, create a situation where privacy guarantees of $\epsilon_1, \epsilon_2, \dots, \epsilon_k$ or better are achieved for all information, respectively.

Note that our methods are expected to distribute more privacy budgets than the existing Kronecker product-based method.

## Future Directions
・ The required privacy level for each information should vary depending on the kinds of data and the analysis purpose. In the future, it would be desirable to evaluate not only the privacy level as in our experiments, but also the accuracy in more detail for each analysis method. Furthermore, it would be fascinating to develop an optimal randomized response in terms of the trade-off between privacy and utility.

・ Improving the optimality of our heuristic method (especially when $\epsilon_i$ is small or $a_i$ is large). ← We would also like to deal with the fact that when solving the linear programming problem by scipy.optimize.linprog, we often encountered numerical difficulties (especially when $k$ is large).

・ Developing better heuristic methods that can achieve the privacy levels that are as close to the input ones as possible. (We feel that this task is not be as easy as it may seem.) 

## Note

For details of our methods and discussion, please see our paper entitled "Privacy-Optimized Randomized Response for Multi-Attribute Data".

### Contact
Akito Yamamoto

Division of Medical Data Informatics, Human Genome Center,

the Institute of Medical Science, the University of Tokyo

a-ymmt@ims.u-tokyo.ac.jp
