# Three-stage-model
Simulation code for [Exact solution of a three-stage model of stochastic gene expression including
cell-cycle dynamics](https://www.biorxiv.org/content/10.1101/2023.08.29.555255v2.full.pdf)
## Requirements
- Mathematica v13.2.1.0
- Pandas v1.3.2
- numpy  1.16.5<=v<=1.23.0
- scipy v1.7.1
## File description
- "SSA_model _II _t10.csv" is the SSA result for Model II in article.
- "exact_solution_Model_II.nb" is the exact solution for Model II in article.
- "population_SSA_IV.ipynb" is the population SSA for Model IV in article.
- "stationary_statistics_Model_III.nb" is the exact solution for Model III in article.

## Examples
The full time domain exact solution of Model II in the article can be obtained by using the code 
```
G = G0 + G1 /. param;
Bins = 80;
Gp = G /. w1 -> 0;
PP = ResourceFunction["NSeries"][Gp, {w2, -1, Bins}][[3]];
v = Table[{i - Bins - 1, Re[PP[[i]]]}, {i, Bins + 1, 2*Bins + 1}];
pG = ListPlot[v, PlotRange -> All]
```

`G` is the Generating function.

The population SSA results of Model IV in the article can be invoked with `population_SSA`
```
data=population_SSA(m0,G0,G1,p0,t0,phase0,age0,Tmax,Ncycle,Tcycle,son,soff,rho,lam,dm)
```
`G0`,`G1`,`m0`,`p0`,`t0`,`phase0`,`age0` are the initial conditions.  
`Tamx` is the simulation ending time.  
`Ncycle` and `Tcycle` is used to calculate the parameter for the exponential distribution Exp(k) by using `k`=`Ncycle`/`Tcycle`.  
`son`,`sof`,`rho`,`lam`,`dm` are the kintic parameters.  
`data` is a matrix with seven rows, stored values of time、 acitve gene、 inactive gene、 mRNA、 protein、 cell age and cell phase respectively.  

The exact solution of Model III in the article can be easily botained by adjust the `param` object in [stationary_statistics_Model_III.nb]()


## Reference
If you found this library useful in your research, please consider citing.
```
@article{wang2023exact,
  title={Exact solution of a three-stage model of stochastic gene expression model including cell-cycle dynamics},
  author={Wang, Yiling and Yu, Zhenhua and Cao, Zhixing and Grima, Ramon},
  journal={bioRxiv},
  pages={2023--08},
  year={2023},
  publisher={Cold Spring Harbor Laboratory}
}
```
