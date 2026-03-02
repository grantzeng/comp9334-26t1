# Operationl analysis 
Computer systems are modelled as a directed graph of queues, called a _queueing network_. 


> We start in a non-probabilisitic setting of a queuing network on some interval $[0, T]$, and basically want to look at "average case" behaviour.  Stochastic processes for later. 


### Open versus closed queuing networks


### (Terminology)
Requests/work in an _open_ queueing network are called _transactions_ whereas in a _closed_ queueing network they are called _jobs_. 
> This terminology is fairly loose though, and they're used interchangeably.

Components of a queueing network are called _devices_ and you add a subscript $j$ to indicate which device you want to talk about.  
- By convention, device $0$ defined as the whole queueing network/system. 

> The reason for the subscripts is that the operational laws all apply at different levels of the system and we would like to talk about how parts of the system relate to the whole system (e.g. where does bottleneck happen?)

# Operational laws 
Consider some measurement/time interval $[0, T]$.
> The reason for phrasing it like this is that in practice when you take measurements this is how you'd be thinking about it. 

## Utilisation law
For device $j$, define $A_j$ as the count of job arrivals during $[0, T]$, and $C_j$ as the number of job completions during $j$ and $B_j$ the amount of time device $j$ was busy during $[0, T]$

Then we can define some derived quantities: 
- **Utilisation**- the % of time the device was busy during the interval
$$U_j := \frac{B_j}{T}$$
- **Throughput** - the output rate/job completion rate
$$X_j :=\frac{C_j}{T}$$
- **Mean service time** - how long on average each completion took. 
$$S_j := \frac{B_j}{C_j}$$

> "Mean service time" is a bit of a misnomer, what you'd really want to do is define $S_j$ as a r.v. and then call $\mathbb{E}(S_j)$ the mean service time, and $\hat{S_j}$ as an estimator for it.  But this is not necessary because we just want to do some simple back-of-envelope calcs. 

These three quantities can be related:
$$
U_j = \frac{B_j}{T} = \frac{(C_j S_j)}{T} = \frac{C_j}{T} S_j 
$$

And hence the **utilization law**: 
$$
\boxed{ U_j = X_j S_j }
$$

## (Equilibrium assumption)

?? 


## Forced flow law 
Jobs might take multiple visits to device $j$ to complete through the whole system so we define 
- **Visit ratio** 
$$
V_j := \frac{C_j}{C_0}
$$
> _Intuition for why it's defined like this_: if a job needs a subsystem 3x times more, then there should be three times the completions at $j$ compared to the whole system

Since throughputs at $j$ and the whole system are defined as $X_j := C_j/T$ and $X_0 := C_j/T$, we have: 
$$
    V_j = \frac{C_j}{C_0} = \frac{(X_jT)}{(X_0T)}
$$
and hence the **forced flow law**

$$ 
\boxed{V_j = \frac{X_j}{X_0}}
$$

## Service demand law 
We need to distinguish between _service time_ and _service demand_. A job might take multiple visits but each visit has a service time. We call the _sum_ of those service times, service demand. 

$$  
D_j := \text{($\Sigma$ service times required from device $j$ per job completion)}
$$

Since $S_j$ is the mean service time, and $V_j$ is the (average) number of times a job visits $j$, it seems that (on average) we can also define this as: 
$$  
D_j := V_j S_j
$$

We can relate system throughput to utilisation of device $j$ with the forced flow and utilisation laws 
$$
D_j = V_j S_j = \left (\frac{X_j}{X_0} \right )  S_j = \frac{(X_jS_j)}{X_0}
$$

And hence the **service demand law**
$$
\boxed{D_j = \frac{U_j}{X_0}}
$$


> This law is very important for determining where (on average) system bottleneck happens!

## Little's law 
Little's law is basically an accounting identity relating how many jobs are in a system to arrival rate and how long it takes for the job to complete. 

$$
\boxed{\bar{N}_j = X_j \bar{R_j}}
$$
where: 
- $\bar{N_j}$ is the average number of jobs in the device $j$
- $\bar{R_j}$ is the average response time of requests (note that this isn't _just_ service demand/time, this _includes_ waiting time)


> The significance of Little's law is that it applies at _every_ level of a queueing network (check if your sums balance!)

(Proof is complicated, so omitted here.)


> Typically in a probabilistic setting you'll more often see it written as $L = \lambda W$ where $L$ is for "load", $\lambda$ arrival rate, and $W$ cycle/lead time (how much time a job spends in the system)

> _(Utilisation law is just Little's law)_ `TODO`


# (Worked examples)
`TODO`


# Proof of Little's law

## Handwaving
`TODO`

## Formal proof
`TODO`