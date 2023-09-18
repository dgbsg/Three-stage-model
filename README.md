# Three-stage-model
This library provides simulation code for [Exact solution of a three-stage model of stochastic gene expression including
cell-cycle dynamics](https://www.biorxiv.org/content/10.1101/2023.08.29.555255v2.full.pdf)
## Requirements
- Mathematica v13.2.1.0
- pandas v1.3.2
- numpy  1.16.5<=v<=1.23.0
- scipy v1.7.1
## File description
- "SSA_model _II _t10.csv" is SSA result for Model II.
- "exact_solution_Model_II.nb" is exact solution for Model II.
- "population_SSA_IV.ipynb" is population SSA for Model IV.
- "stationary_statistics_Model_III.nb" is exact solution for Model III.

## Examples
__1. Exact solution of Model II.__  

The full time domain exact protein distribution of Model II can be obtained by using
```
G = G0 + G1 /. param;
Bins = 80;
Gp = G /. w1 -> 0;
PP = ResourceFunction["NSeries"][Gp, {w2, -1, Bins}][[3]];
v = Table[{i - Bins - 1, Re[PP[[i]]]}, {i, Bins + 1, 2*Bins + 1}];
pG = ListPlot[v, PlotRange -> All]
```
`G` is the generating function. If you care about the probability distribution of mRNA, swap the positions of w1 and w2. For more details, please refer to [exact_solution_Model_II.nb]().

__2. The population SSA of Model IV.__  

The population SSA results of Model IV can be invoked with `population_SSA`
```
data=population_SSA(m0,G0,G1,p0,t0,phase0,age0,Tmax,Ncycle,Tcycle,son,soff,rho,lam,dm)
```
`G0`,`G1`,`m0`,`p0`,`t0`,`phase0`,`age0` are initial conditions.  
`Tmax` is simulation ending time.  
Calculate the parameter `k` for the exponential distribution by using `k`=`Ncycle`/`Tcycle`.  
`son`,`sof`,`rho`,`lam`,`dm` are kintic parameters.  
`data` is a matrix with seven rows, stores values of 
absolute time、 acitve gene、 inactive gene、 mRNA、 protein、 cell age and cell phase respectively. For more details, please refer to [population_SSA_IV.ipynb]().  

__3. The exact statistics of Model III.__  

The exact statistics of Model III in stationary state can be obtained by [stationary_statistics_Model_III.nb]()


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
