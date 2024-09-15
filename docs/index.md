# Chapter 30 Introduction to Queing Theory
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Itim&display=swap" rel="stylesheet">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Itim&family=K2D:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800&display=swap" rel="stylesheet">

## Queing in a nutshell
ไว้คอยบอกเวลาที่ใช้ในแต่ละ Queue

- Many jobs shares **system resources**
- One job at anytime others wait

## Queing Notation

<p align="center">
<img src="images\queue_component.png" width="400"></img><br/>
Components of a Queue
</p>

##### 1. Arrival Process
- Interarrival times $\tau_j=t_j-t_{j-1}$ (เวลาห่างกันเท่าไหร่)
- $\tau_j=t_j-t_{j-1}$ assumed to be Independent and Identically Distributed **(IID)**
- **Piosson Arrival** is common and interarrival times are **IID** and **Exponentially distributed**
- Also **Erlang** and **Hyperexponential** used
##### 2. Service Time Distribution
- Ex. Service Time = Time each student spends at the terminal
- Assumed that Service time are random variable and IID
- **Exponential Distribution** is commonly used
- Erlang, hyperexponential and general can also be used
##### 3. Number of Servers (ตัวประมวลผล)
- Part of **same queing system**
- Identical ex any student to any terminal
- if **not identical** then group identical with **seperate queue** so each group is a queing system
##### 4. System Capacity
- Number of students can stay in the room (buffer)
- Capacity is **finite** (for most system) but if large, easier to **assume infinite**
##### 5. Population Size
- Number of potential student who can use the computer
- Population is **finite** (for most system) again, if large, it's easier to **assume infinite**
##### 6. Service Discipline
- Order which the students are served
    - FCFS : First Come First Served
    - LCFS : Last Come First Served
    - LCFS-PR : Last Come First Serve with Preempt and Resume
    - RR : Round Robin
    - PS : Processing Sharing (Small Quantum)
    - IS : Infinite Server = Fixed delay
    - SPT : Shorting Processing Time first
    - SRPT : Shorting remaining Processing time first
    - SEPT : Shortest Expected Processing Time first
    - SERPT : Shortest Expected Remaining Processing Time first
    - LVFS : Loudest Voice First Served

### Kendall notation $A/S/m/B/K/SD$
- $A$ : interarrival time distribution
- $S$ : Service time distribution
    - $A$ and $S$ Can be denoted by one-letter symbol as follows
        - $M$ : Exponential
        - $E_k$ : Erlang with parameter k
        - $H_k$ : Hyperexponential with parameter k
        - $D$ : Deterministic
        - $G$ : General
- $m$ : number of servers
- $B$ : number of buffers
- $K$ : Population size
- $SD$ : Service discipline

## Exponential Distribution
- Probability Density Function (pdf)
    - $f(x)=\frac{1}{a}e^{\frac{-x}{a}}$
- Cumulative Distribution Function (cdf)
    - $F(x) = P(X<x) = \int_{0}^{x}f(x)dx=1-e^{-x/a}$
- Mean : $a$
- Variance : $a^2$
- Coefficient of variation (CV) = SD / mean = 1
- **Memoryless** ไม่สนอดีต
    - **Expected time** of next arrival is always $a$

## Erlang Distribution
- Sum of $k$ exponential random variables
    - $X=\sum_{i=1}^k x_i$ where $x_i$ ~ exponential
- pdf
    - $f(x) = \frac{x^{k-1}e^{-x/a}}{(k-1)! a^k}$
- Expected Value : $ak$
- Variance : $a^2k$
- CV : $\frac{1}{\sqrt{k}}$

## Hyper-Exponential Distribution 
(คือไรไม่รู้อ่านก็ไม่รู้เรื่อง)

- The variable takes $i^{th}$ value with prob $p_i$

<figure markdown="span" align="center">
<img src="images\hyper_exponential.png" height="200"></img>
<figcaption>Hyper Exponential</figcaption>
</figure>
$x_i$ is exponentially distributed with mean $a_i$

- Higher variance then exponential (CV > 1)

## Group Arrivals/Service
- Buld arrival/service
- $M^{x}$ : $x$ represents the group size
- $G^{x}$ : $x$ a bulk arrival or service process with general inter-group times

## Key Variables used in Analysis of Single Queue
- $E$ : Expected (mean)
- $\lambda$ : arrival rate = $1/E[\tau]$
- $s$ : Service time per job
- $\mu$ : Mean of service rate per server = $1/E[s]$
- $n$ : queue length
- $n_q$ : Number of jobs waiting
- $n_s$ : Number of jobs reqceiving service
- $r$ : response time = time waiting + time receiving service
- $w$ : waiting time = Time between arrival and beginning of service

## Rules of all Queues
#### Rules that apply to G/G/m Queues
###### 1. Stability Condition : $\lambda < m\mu$
> $\lambda$ : Mean arrival rate = $1/E[\tau]$ <br/>
$m$ : number of servers <br/>
$\mu$ : Mean service rate per server = $1/E[s]$ <br/>

finite-population or finite-buffer always **stable** <br/>
infinite queue = **instability**

###### 2. Number in System VS Number in Queue : $n=n_q+n_s$
> $n_q$ : Number in Queue <br/>
$n_s$ : Number Receiving service <br/>
$n$ : Number of Jobs <br/>

Since it random $E[n]=E[n_q]+E[n_s]$

###### 3. Number VS Time
if jobs are not lost due to in sufficient buffers<br/>
> Mean number of jobs in the **system** <br/>
&nbsp;&nbsp;= arrival rate * mean **response** time <br/>
&nbsp;&nbsp;= $\lambda r$ <br/>

> Mean number of jobs in the **queue** <br/>
&nbsp;&nbsp;= arrival rate * mean **waiting** time <br/>
&nbsp;&nbsp;= $\lambda w$ <br/>

###### 4. Time in System VS time in Queue $r=w+s$
> $r$,$w$,$s$ are random variables <br/>
$E[r] = E[w] + E[s]$ <br/>
if service rate is independent of number of jobs in the queue <br/>
$CV(w,s)=0$ <br/>
$Var[r] = Var[w] + Var[s]$ <br/>

ที่เหลือเดี๋ยวค่อยมาต่อ
