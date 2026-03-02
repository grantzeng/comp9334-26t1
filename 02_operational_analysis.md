# Operational analysis
Computer systems are modelled as a directed graph of queues, called a _queueing network_. 

> We start in a non-probabilisitic setting of a queuing network on some interval $[0, T]$, and we want to look at "average" behaviour.  Stochastic processes/extreme behaviour for later.

> `TODO: Rewrite explanations in terms of "long run limit behaviour" ` $t \rightarrow \infty$ `type explanations, since this is where all the results come from I think`. 
> `TODO: I think "good enough" proof for me would be derive all these results as limiting behaviour results`

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

## (Equilibrium/flow balance assumption)

$$ 
A = C \implies \lambda = X_0
$$


## Forced flow law 
Jobs might take multiple visits to device $j$ to complete through the whole system so we define 
- **Visit ratio** 
$$
V_j := \frac{C_j}{C_0}
$$
> _Intuition for the definition_: if a job needs a subsystem "3x times more", then there should be three times the completions at $j$ compared to the whole system

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


## (Worked examples)
`TODO: Example demonstrating calculations using the laws and redoing the calculation from first principles`


## Little's law 
`TODO: Change this to the lecture notation`

Little's law is basically an accounting identity relating how many jobs are in a system to the rate jobs arrive and how long it takes for a job to complete. 

$$
\boxed{N_{avg} = X R_{avg}}
$$
where: 
- $N_{avg,j}$ is the average number of jobs in the device $j$
- $R_{avg, j}$ is the average response time of requests in device $j$ (note that this isn't _just_ service demand/time, this _includes_ waiting time if there is any)


The significance of Little's law is that is a invariant at _every_ level of a queueing network.

> E.g. in a system with one queue and one server, $N_{avg} = N_{avg, queue} + N_{avg, server}$ and $R_{avg} = R_{avg, queue} + R_{avg, server} = W + S$ where $W$ is mean wait time and $S$ is mean service time for the whole system, and Little's law holds whether you look at device $0$, just the queue or just the server.  

> Use it to sanity check your sums!


(Proof is complicated, so omitted here.)

> Typically in a probabilistic setting you'll more often see it written as $L = \lambda W$ where $L$ is for "load", $\lambda$ arrival rate, and $W$ cycle/lead time (how much time a job spends in the system)

> _(Utilisation law is just Little's law)_ `TODO`


## (Worked examples - Little's law)
`TODO: Example demonstrating Little's law as accounting`

> https://en.wikipedia.org/wiki/Dimensional_analysis (sanity check your sums)



## Interactive response-time law 

> This _only_  applies to interactive systems and is really just Little's law in disguise

> _Context_: QNs are either open or closed, and if they are closed, they're either an interactive system or a batch system. 

> _Context_: Basically, the reason for pointing out interactive systems is that we can add an additional operational law. For an open system, we actually need more probability than we want to allow right now to analyse e.g. $R$ etc. so for now just gloss over it and for a batch system, this is "just an interactive system with no think time" ($Z = 0$) 

For an interactive system, we can assume that work is generated by a fix population of $M$ users who alternate between _thinking_ and _processing_. 
-  This means they can't send multiple requests, they have to wait for the request to return and process it first.

Define $Z$ as mean thinking time and $R$ as mean response time. $X_0$ is still system throughput. 

If we look at the $M$ users only, by Little's law we have on average the number of busy/thinking users is: 
$$
    M_{avg} = X_0Z
$$
But then if we look at the computer system only and apply Little's law, the average number of requests is: 
$$
    N_{avg} = \lambda R = X_0R
$$
> `TODO: why is \lamdba = X_0 if we assume A=C?`

Since users are either thinking or processing, and if they're processing, then there is the same number of jobs at the computer system we have 
$$
    M = M_{avg} + N_{avg} = X_0Z + X_0R
$$
And hence the the **interactive response time law**
$$
    \boxed{M = X_0(Z + R)}
$$




# (Addendum: Proof of Little's law)

## Handwaving
`TODO`

## Formal proof
`TODO`