# Privacy-Optimized RR for Sharing Multi-Attribute Data

This contains Python codes of our experiments on privacy level (for the entire dataset), example of data analysis (using genome statistics), and run time.

In the evaluation of privacy level, we compared our two methods (optimal solution that solves a linear programming problem and heuristic method) with the existing Kronecker product-based method [[Wang et al., 2016](https://ceur-ws.org/Vol-1558/paper35.pdf)], when the privacy level for each attribute information is given. 

As an analysis example using our method, we considered the case where the privacy level for the entire dataset is fixed and evaluated the accuracy of output (differentially private) $\chi^2$-statistics in genomic statistical analysis.

The run time results show that our heuristic method can be performed in about $1$ second even for a large dataset with $k = 1,000$. In Run Time folder, we also provide the results when $k = 10,000$, $k = 100,000$, and $k = 12$ for reference. When $k = 12$, our optimal method took about $2$ hours, which seems to be the limit at which it can be performed in a practical time.

In Supplements.pdf, we provide a review of related studies, concrete descriptions of our methods, and experimental results and discussion on analysis example.

## Important Note

### Elements of Distortion Matrix $\mathbf{P}$

$X_j$ described in Methods Section of our paper is the probability of individual events that hold the condition associated with $X_j$, under the context of Randomized Response. In this study, we assume that the probabilities of all these events are equally $X_j$. (Under this assumption, the distiorion matrix $\mathbf{P}$ becomes a symmetric matrix.)

For example,  
$X_{0} = \Pr[\mathrm{Output}[1] = d_1 \ \land \ \mathrm{Output}[2] = d_2 \ \land \cdots \land \mathrm{Output}[k] = d_k \ | \ \mathrm{Input}[1] = d_1 \ \land \ \mathrm{Input}[2] = d_2 \ \land \cdots \land \mathrm{Input}[k] = d_k]$  
$\ \ \ \ \ = \Pr[\mathrm{Output}[1] = d'_1 \ \land \ \mathrm{Output}[2] = d'_2 \ \land \cdots \land \mathrm{Output}[k] = d'_k \ | \ \mathrm{Input}[1] = d'_1 \ \land \ \mathrm{Input}[2] = d'_2 \ \land \cdots \land \mathrm{Input}[k] = d'_k]$  
$\ \ \ \ \ = \cdots$  ,  
$X_1 = \Pr[\mathrm{Output}[1] = p_1 \ \land \ \mathrm{Output}[2] = d_2 \ \land \cdots \land \mathrm{Output}[k] = d_k \ | \ \mathrm{Input}[1] = d_1 \ \land \ \mathrm{Input}[2] = d_2 \ \land \cdots \land \mathrm{Input}[k] = d_k]$  
$\ \ \ \ \ = \Pr[\mathrm{Output}[1] = p'_1 \ \land \ \mathrm{Output}[2] = d'_2 \ \land \cdots \land \mathrm{Output}[k] = d'_k \ | \ \mathrm{Input}[1] = d'_1 \ \land \ \mathrm{Input}[2] = d'_2 \ \land \cdots \land \mathrm{Input}[k] = d'_k]$  
$\ \ \ \ \ = \cdots$  ,  
where $d_i, \ d'_i, \ p_1, \ p'_1$ are possible attribute values, $d_1 \neq p_1$, and $d'_1 \neq p'_1$.

Note that  
$X_{0}$ is not equal to $\Pr[\mathrm{Input}[1] = \mathrm{Output}[1] \ \land \ \mathrm{Input}[2] = \mathrm{Output}[2] \ \land \cdots \land \ \mathrm{Input}[k] = \mathrm{Output}[k]]$ or $\Pr[\mathrm{Input}[1] = d_1 \ \land \ \mathrm{Output}[1] = d_1 \ \land \ \mathrm{Input}[2] = d_2 \ \land \ \mathrm{Output}[2] = d_2 \ \land \cdots \land \mathrm{Input}[k] = d_k \ \land \ \mathrm{Output}[k] = d_k]$,  
and  
$X_1$ is not equal to $\Pr[\mathrm{Input}[1] \neq \mathrm{Output}[1] \ \land \ \mathrm{Input}[2] = \mathrm{Output}[2] \ \land \cdots \land \ \mathrm{Input}[k] = \mathrm{Output}[k]]$ or $\Pr[\mathrm{Input}[1] = d_1 \ \land \ \mathrm{Output}[1] \neq d_1 \ \land \ \mathrm{Input}[2] = d_2 \ \land \ \mathrm{Output}[2] = d_2 \ \land \cdots \land \mathrm{Input}[k] = d_k \ \land \ \mathrm{Output}[k] = d_k]$ or $\Pr[\mathrm{Output}[1] \neq d_1 \ \land \ \mathrm{Output}[2] = d_2 \ \land \cdots \land \mathrm{Output}[k] = d_k \ | \ \mathrm{Input}[1] = d_1 \ \land \ \mathrm{Input}[2] = d_2 \ \land \cdots \land \mathrm{Input}[k] = d_k]$.

And then, the relations  
$\ \ \ \ \ \ \ \Pr[\mathrm{Output}[i] = u | \mathrm{Input}[i] = u] = \sum_{j\ :\ i \notin S_j} X_j \cdot t_j$  
$\mathrm{and} \ \Pr[\mathrm{Output}[i] = u | \mathrm{Input}[i] = v] = \sum_{j\ :\ i \in S_j} \frac{X_j \cdot t_j}{a_i - 1}$  
hold. (For details, please refer to our paper.)

### Another Solution to Find "Near-Optimal" Solution

We may construct a linear programming problem for $k+1$ variables (from $x_{k,0}$ to $x_{k,k}$ in our proposed method). 

However, our method is (currently) more efficient than solving the linear programming problem (cf. [Cohen, Lee, and Song, 2021](https://doi.org/10.1145/3424305) and [Brand, 2020](https://doi.org/10.1137/1.9781611975994.16)); therefore, to efficiently construct a randomized response that achieves stronger privacy guarantees than the method using the Kronecker product, our method might be more useful (and is more interesting). 

Of course, there may be cases where solving the linear programming problem would be superior, depending on the optimality and the acheved $\epsilon_i$, and this will be an important issue to be addressed in the future.

## One Possible Policy to Distribute Privacy Budgets (when using our methods)

Set the minimum privacy level to be guaranteed for each of the $k$-attribute information as $\epsilon_1, \epsilon_2, \dots, \epsilon_k$, respectively. Under this condition, consider increasing the accuracy of data analysis as much as possible, when the privacy level for the entire dataset is fixed.

1. If $\epsilon_1, \epsilon_2, \dots, \epsilon_k$ are all distributable, distribute as is.
2. If not distributable, prioritize reducing the budget for information that does not require a high degree of accuracy or that can be expected to be accurate even with a small $\epsilon$. (Distibute a budget of almost $\epsilon_i$ as much as possible for information that requires a high degree of accuracy.)
3. Check whether the updated budgets are distributable, using our methods each time.
4. Ultimately, create a situation where privacy guarantees of $\epsilon_1, \epsilon_2, \dots, \epsilon_k$ or better are achieved for all information.

Note that our methods are expected to distribute more privacy budgets than the existing Kronecker product-based method (as shown in our results of analysis example).

Although it is also possible to regard $k$-attribute information collectively as single attribute information and employ the most basic randomized response, the privacy level for each attribute information cannot be varied in such a case; therefore, we did not discuss it in this study.

## Future Directions
・The required privacy level for each information should vary depending on the kinds of data and the analysis purpose. In the future, it would be desirable to evaluate not only the privacy level as in our experiments, but also the accuracy in more detail for each analysis method. Ultimately, it would be fascinating to develop an optimal randomized response in terms of the trade-off between privacy and utility. (Are there any cases where the distortion matrix $\mathbf{P}$ should not be a symmetric matrix?)

・Improving and theoretically analyzing the optimality of our heuristic method (especially when $\epsilon_i$ is small or $a_i$ is large), with reference to the discussion in Experiments and Discussion Section of our paper. (We should consider a few more matrix elements as variables for events that more than one attribute values differ. ← In this study, all those values are set to equal in the heuristic method.)

・Developing better heuristic methods that can achieve the privacy levels that are as close to the input ones as possible. (We feel that this task is not be as easy as it may seem. Our proposed algorithm can achieve privacy levels closer to the input ones by changing the order of attributes, for example, but a method that does not require such a procedure like parameter-tuning would be more desirable.) 

・Developing optimal methods for multi-dimensional "numeric" data. (This study focused on categorical data.) ← One possible derection is to extend [Duchi et al., 2018](https://doi.org/10.1080/01621459.2017.1389735) and [Wang et al., 2019](https://doi.org/10.1109/ICDE.2019.00063)'s methods by combining them with our methods. **As for Algorithm 4 in the paper of Wang et al., given that it can also handle categorical data, our proposed methods already have the potential to increase the privacy budget ($\epsilon/k$) in Step 5 when handling categorical data and improve the output accuracy.**

・Enhancing our methods under other concepts of differential privacy like One-Sided Differential Privacy [[Kotsogiannis et al., 2020](https://doi.org/10.1109/ICDE48307.2020.00049)].

・Considering the Randomized Response techniques under $(\epsilon, \delta)$-differential privacy (cf. the discussion in the Conclusion Section).

## Note

For details of our methods and discussion, please see our paper entitled "Privacy-Optimized Randomized Response for Sharing Multi-Attribute Data" (to appear at IEEE ISCC 2024, full ver. → arXiv: http://arxiv.org/abs/2402.07584).

### Contact
Akito Yamamoto

Division of Medical Data Informatics, Human Genome Center,

the Institute of Medical Science, the University of Tokyo

a-ymmt@ims.u-tokyo.ac.jp
