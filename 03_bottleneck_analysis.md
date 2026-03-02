# Bottleneck analysis

## Where does $X_0$ get throttled? 

> _Note_: You might think, well, surely it would depend on how jobs get routed? The answer to that is we don't care, because we're only interested in _average_ behaviour. 

### (We can get throttled by capacity of worst device)
Rearranging the service demand law we have: 
$$
D_j = \frac{U_j}{X_0} \implies X_0 = \frac{U_j}{D_j}
$$

but since $\forall j: U_j \leq 1$ because it's a percentage, then it follows all devices $j \in \{1, \ldots K\}$

$$
    \forall j: X_0 \leq \frac{1}{D_j} \implies X_0 \leq \frac{1}{\max\limits_{j} D_j} 
$$

The moral is that we can get bottlenecked on the _device with the highest service demand_. 

### (We can get throttled by the number of jobs already in the system: Little's law)

For the whole system by Little's law we have
$$  
    N = X_0R
$$

Define $R_j$ as the contribution of device $j$ to the mean response time $R$. This can be split into $W_j$ waiting time or $S_j$ service time.  
$$
    R = \sum_j V_j(W_j + S_j) 
$$
Now, at best we have no waiting time, and since all $W_j \geq 0$ we have: 

$$
    R \geq \sum_j V_jS_j
$$
Then by the service demand law at each device $j$ we can lower bound $R$
$$
    R \geq \sum_j V_jS_j = \sum_j D_j \implies D = \sum_j D_j \leq R
$$ 
So plugging this inequality into Little's law we get: 
$$ 
    N = X_0 R \geq \sum_j D_j X_0 \implies X_0 \leq \frac{N}{\sum\limits_{j} D_j}
$$
and we have a better bound on $X_0$ as
$$
    \boxed{X_0 \leq \min \left \{ \frac{1}{\max\limits_{j}D_j}, \frac{N}{\sum\limits_{j} D_j} \right\}}
$$

### (Interactive systems: need to use interactive response time law and not just plain Little's law)

The interactive response time law states 
$$
    M = X_0(R + Z) \implies X_0 = \frac{M}{R + Z}
$$

Since $\displaystyle R \geq \sum_j D_j$ from above we get 
$$
    X_0 = \frac{M}{R + Z} \leq \frac{M}{\sum\limits_{j}D_j + Z}  
$$ 
So, 
$$
    \boxed{X_0 \leq \min \left\{ \frac{1}{\max\limits_{j}D_j}, \frac{M}{\sum\limits_{j} D_j + Z} \right\}}
$$




## Example: modification analysis 

`TODO: Do we get the new system? It depends on M`



