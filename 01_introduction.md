# Introduction 
# What is capacity planning? 
After functional, security and other requirements, computer systems have system performance requirements, e.g. 
 "The computer system must return a database search within 20ms if there are 500 search queries per second?", in this case: 
- _Capacity_ is about resources required to support performance
- _Performance_ is about whether the system achieves some quality of service metric (_under_ a specified _workload_.) 

> _Note_: The performance specification is meaningless _without_ also specifying workload characteristics to be handled!

### Capacity planning problems $\Leftrightarrow$ performance analysis problems duality
The basic outline of any capacity planning problem goes: 
```
Given:  
- workload
- performance specification

Find: 
- capacity (hardware, network, personnel, budget etc.)
```

Whereas a performance analysis problem goes: 
```
Given: 
- workload  
- capacity

Find: 
- performance achievable
```

> _For example:_ "If a webserver needs to complete a HTTP request within 20ms when there's 500 HTTP requests/s what CPU speed do we need (capacity planning problem)" $\Leftrightarrow$ "A webserver has a CPU with $x$ MIPS, when there's 500 HTTP requests/s what is the response time?" (performance analysis question). If we solve for $x$ then can find an appropriate CPU speed. 

> _Moral_: You can solve a capacity planning problems by solving a series of performance analysis problems. 

> Because this is the case we'll be spending the next four weeks learning about tools for performance analysis before moving on to capacity planning problems! 

# Quality of service (QoS)/performance metrics 

### Availability 
Fraction of the time the system is _up and usable_ for users (e.g. "network outage is less than 6hrs per 30 days" $\rightarrow 1 - 6/(30*24) = 99.17\%$ available)

_Why it matters?_ (1) critical infrastructure needs to be available (e.g. phone network coverage for ambulance/police/fire calls) and (2) customer satisfaction. 

### Response time, waiting time, service time
$R = t_2 - t_1$ where $t_1$ is the time the request arrives, and $t_2$ is the time the request is completed and leaves. 

Can specify probabilistically, e.g. specify $\mathbb{E}(R)$, $\sigma_{R}$, $R \sim Y$ where $Y$ is some r.v. with a pdf of interest, etc. 

Often jobs have to queue up, so: 
$$
R = W + S
$$ 
where $W$ is waiting time (in some queue) and $S$ is processing/service time (how long it takes for request to be processed by a server)


### Throughput 
The _rate_ at which _requests_ are completed.  e.g. packets/s, Mb/s, HTTP requests/s, bytes/s, MIPS, FLOPS. 

The throughput of a system is a function of _capacity_ and _load_ placed on the system; where $A$ is arrivals/offered load and $C$ is capacity:  
$$
    T = \min \{A, C\}
$$
- i.e. if $A < C$, then server runs out of work, but if $ A > C$, then we're at capacity. 


_Note_: Some systems experience **thrashing** where when a system is overloaded, throughput _decreases_ e.g. congestion collapse in networks with TCP (without congestion control), thrashing in an OS because RAM is overcommitted. 

### Reliability 
(See later course notes)

### Scalability 
(Not covered in course)


# Tools/techniques, example problems
`TODO`
