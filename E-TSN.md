## TSNkit & E-TSN
E-TSN proposes to use TSN network to schedule events to trigger data flow ET, and proposes three innovative methods to solve the difficulty of ET scheduling, which is that the **occurrence time is unpredictable** , which are probabilistic flow modeling, preferential time slot sharing and cautious time slot reservation.
### 1. Probabilistic stream
The minimum occurrence interval of ET streams is divided into several probabilistic streams, and the delay of each probabilistic stream is delay-T/N, and the probabilistic streams are written into the scheduling task, and these probabilistic streams need to be scheduled, but unlike TT stream scheduling, probability streams from the same ET stream can overlap in the same time interval.
```python


```
### 2. Prioritized slot sharing
According to the algorithm in the paper, the TT stream is extended to achieve low latency of ET stream scheduling, but the sharing is not infinite, but the limited expansion of the TT stream on the shared link.
```python


```
### 3. Prudent reservation
Finally, the algorithm needs to meet the scheduling time slot of the TT flow.
```python


```
