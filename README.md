# Privacy-Optimized RR for Sharing Multi-Attribute Data

This contains Python codes of our experiments on privacy level (for the entire dataset), example of data analysis (using genome statistics), and run time.

In the evaluation of privacy level, we compared our two methods (optimal solution that solves a linear programming problem and heuristic method) with the existing Kronecker product-based method [[Wang et al., 2016](https://ceur-ws.org/Vol-1558/paper35.pdf)], when the privacy level for each attribute information is given. 

As an analysis example using our method, we considered the case where the privacy level for the entire dataset is fixed and evaluated the accuracy of output (differentially private) $\chi^2$-statistics in genomic statistical analysis.

The run time results show that our heuristic method can be performed in about $1$ second even for a large dataset with $k = 1,000$. In Run Time folder, we also provide the results when $k = 10,000$, $k = 100,000$, and $k = 12$ for reference. When $k = 12$, our optimal method took about $2$ hours, which seems to be the limit at which it can be performed in a practical time.

## Important Note
$X_j$ described in Methods Section is the probability of an individual event that holds the condition associated with $X_j$, under the context of Randomized Response. In this study, we assume that the probabilities of these events are equally $X_j$.

For example,  
$X_{2^k - 1} = \Pr[\mathrm{Output}[1] = p_1 \ \land \ \mathrm{Output}[2] = p_2 \ \land \cdots \land \mathrm{Output}[k] = p_k \ | \ \mathrm{Input}[1] = d_1 \ \land \ \mathrm{Input}[2] = d_2 \ \land \cdots \land \mathrm{Input}[k] = d_k]$
$\ \ \ \ \ \ \ \ \ \ = \Pr[\mathrm{Output}[1] = p'_1 \ \land \ \mathrm{Output}[2] = p'_2 \ \land \cdots \land \mathrm{Output}[k] = p'_k \ | \ \mathrm{Input}[1] = d'_1 \ \land \ \mathrm{Input}[2] = d'_2 \ \land \cdots \land \mathrm{Input}[k] = d'_k]$  
$\ \ \ \ \ \ \ \ \ \ = \cdots\ \ \ ,$  
where $d_1 \neq p_1 \ \land \ d_2 \neq p_2 \ \land \cdots \land \ d_k \neq p_k$, $d'_1 \neq p'_1 \ \land \ d'_2 \neq p'_2 \ \land \cdots \land \ d'_k \neq p'_k$, and $d_i, \ d'_i, \ p_i, \ p'_i$ are possible attribute values.

Note that $X_{2^k - 1}$ is not equal to $\Pr[\mathrm{Input}[1] \neq \mathrm{Output}[1] \ \land \ \mathrm{Input}[2] \neq \mathrm{Output}[2] \ \land \cdots \land \ \mathrm{Input}[k] \neq \mathrm{Output}[k]]$ or $\Pr[\mathrm{Input}[1] = d_1 \ \land \ \mathrm{Output}[1] = p_1 \ \land \ \mathrm{Input}[2] = d_2 \ \land \ \mathrm{Output}[2] = p_2 \ \land \cdots \land \mathrm{Input}[k] = d_k \ \land \ \mathrm{Output}[k] = p_k]$.

## One Possible Policy to Distribute Privacy Budgets (when using our methods)

Set the minimum privacy level to be guaranteed for each of the $k$-attribute information as $\epsilon_1, \epsilon_2, \dots, \epsilon_k$, respectively. Under this condition, consider increasing the accuracy of data analysis as much as possible, when the privacy level for the entire dataset is fixed.

1. If $\epsilon_1, \epsilon_2, \dots, \epsilon_k$ are all distributable, distribute as is.
2. If not distributable, prioritize reducing the budget for information that does not require a high degree of accuracy or that can be expected to be accurate even with a small $\epsilon$. (Distibute a budget of almost $\epsilon_i$ as much as possible for information that requires a high degree of accuracy.)
3. Check whether the updated budgets are distributable, using our methods each time.
4. Ultimately, create a situation where privacy guarantees of $\epsilon_1, \epsilon_2, \dots, \epsilon_k$ or better are achieved for all information.

Note that our methods are expected to distribute more privacy budgets than the existing Kronecker product-based method (as shown in our results of analysis example).

Although it is also possible to regard $k$-attribute information collectively as single attribute information and employ the most basic randomized response, the privacy level for each attribute information cannot be varied in such a case; therefore, we did not discuss it in this study.

## Future Directions
・The required privacy level for each information should vary depending on the kinds of data and the analysis purpose. In the future, it would be desirable to evaluate not only the privacy level as in our experiments, but also the accuracy in more detail for each analysis method. Ultimately, it would be fascinating to develop an optimal randomized response in terms of the trade-off between privacy and utility.

・Improving and theoretically analyzing the optimality of our heuristic method (especially when $\epsilon_i$ is small or $a_i$ is large), with reference to the discussion in Experiments and Discussion Section of our paper. (We should consider a few more matrix elements as variables for events that more than one attribute values differ. ← In this study, all those values are set to equal in the heuristic method.)

・Developing better heuristic methods that can achieve the privacy levels that are as close to the input ones as possible. (We feel that this task is not be as easy as it may seem. Our proposed algorithm can achieve privacy levels closer to the input ones by changing the order of attributes, for example, but a method that does not require such a procedure like parameter-tuning would be more desirable.) 

・Developing optimal methods for multi-dimensional "numeric" data. (This study focused on categorical data.) ← One possible derection is to extend [Duchi et al., 2018](https://doi.org/10.1080/01621459.2017.1389735) and [Wang et al., 2019](https://ieeexplore.ieee.org/abstract/document/8731512)'s methods by combining them with our methods.

・Enhancing our methods under other concepts of differential privacy like One-Sided Differential Privacy [[Kotsogiannis et al., 2020](https://ieeexplore.ieee.org/document/9101725)].

## Note

For details of our methods and discussion, please see our paper entitled "Privacy-Optimized Randomized Response for Sharing Multi-Attribute Data".

### Contact
Akito Yamamoto

Division of Medical Data Informatics, Human Genome Center,

the Institute of Medical Science, the University of Tokyo

a-ymmt@ims.u-tokyo.ac.jp
