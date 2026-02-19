# Operational analysis
> Tools for analysing queueing models/systems of queues: the math we used to analyse a computer system.  
> First, the main quantities. Then, some simple relationships. Then Little's law

`TODO: Why we want to do this` 

`TODO: How does the fact a system is closed or open affect how we analyse it?`


# Closed/open networks 



# Operational laws 
> For the purposes of the discussion imagine a FIFO queue to simply things. Other than Little's law, these are fairly easy to derive. Little's law is more fundamental so we separate that out. 

> These laws are important because for system we can derive some of the quantities

## Basic quantities
For an observation period $T$, define: 
- $A$ as the number of requests that arrived during $T$
- $C$ ditto. completed during $T$
- $B$ as the amount of time a device spends "busy" during $T$ 
> $B$ only really makes the most sense when there is a single server. 
- $S$ as _mean_ service time per visit. 
> This is about the amount of time required _per visit_ to a device, whereas _service demand_ $D$ is the mean service time required to finish a job, the point being that a job might take more than one visit. `TODO: Check this definition` 

> _Alternative conventions_: In the maths, $S$ is instead defined as a r.v. for service time which would make $\mathbb{E}(S)$ the mean service time. 

Then define some derived quantities:
- $\displaystyle \lambda = \frac{A}{T}$: arrival rate

- $\displaystyle X = \frac{C}{T}$: throughput (requests completed per time)

- $\displaystyle U = \frac{B}{T}$: utilisation (% time server is busy)

- $\displaystyle S = \frac{B}{C}$: mean service time.
 
### (Subscripts)
Subscripts are added to specify arrivals/completions/rates etc. at a device $j$ i.e. $A_j$, $B_j$, $C_j$

> For example, $\displaystyle D = \sum_{i} D_i$

The convention is to add a device $0$ to represent the outside world e.g. $A_0$, $C_0$ for arrivals/completions of the system. 

- This means in a closed system $A_0 = C_0 = 0$ (but note there may be circulation _within_ the system still, so it's non-zero for some subsystem) `TODO: Check this`

### Visit ratios
Define $V_j$ as the number of times a job/transaction visits device $j$. 

$\displaystyle V_j = \frac{C_j}{C_0}$ because if a completion requires $n$ visits to device $j$ then overall there should be $j$ times more completions at $j$ than for the whole system. 

### Service demand 
For a job, define service demand $D_j$ as the total service time required by that job at a device $j$. 

> The point is a job may take more than one access to complete so we need this additional notation. 

$D_j = V_j S_j$ because $V_j$ is the number of times a job visits $j$ (visit ratio), and $S_j$ is the time cost per visit (service time)

`TODO: this is not really a proof but this relationship looks reasonable?`


>_Note_: $D_j$ is important for looking at bottlenecks!

### Requests in system and response time 
Define $N_{avg}$ average number of requests. Define $R_{avg}$ average response time of the requests. 


## (Equilibrium assumption)
Often we assume the system is in equlibrium i.e. $C \approx A$, or $C = A$, since if $A > C$ the system is unstable/will become overloaded.


## Utilisation law 
Given definitions it follows: 
$$
U = \frac{B}{T} = \frac{SC}{T} = \frac{(XT)C}{T} = XS
$$

Although it falls out of the algebra, it's also possible to see this as a special case of Little's law

`TODO: Explain how drawing system boundaries correctly lets you do this`

> "Percent utilisation is equal to throughput times average service time"

## Forced flow law 

Given, $\displaystyle V_j = \frac{C_j}{C_0}$, $\displaystyle X_j = \frac{X_j}{T}$ and $\displaystyle X_0 = \frac{C_0}{T}$, it follows that

$$
V_j = \frac{X_j}{X_0}
$$

> "Visit ratio at $j$ is equal to the throughput at $j$ divided by total throughput"

## Service demand law
Given the forced flow law $\displaystyle V_j = \frac{X_j}{X_0}$ and $D_j = V_j S_j$ it follows: 

$$
D_j = \frac{X_j}{S_j} = \frac{U_j}{X_0}
$$

> This law is important for determining bottlenecks


# Little's law 
> The reason Little's law is important is that it's essentially a conservation law/system invariant. 



### Handwaving proof 

### (Formal derivation)