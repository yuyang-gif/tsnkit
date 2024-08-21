## TSNkit & E-TSN
E-TSN proposes to use TSN network to schedule events to trigger data flow ET, and proposes three innovative methods to solve the difficulty of ET scheduling, which is that the **occurrence time is unpredictable** , which are probabilistic flow modeling, preferential time slot sharing and cautious time slot reservation.
### 1. Probabilistic stream
The minimum occurrence interval of ET streams is divided into several probabilistic streams, and the delay of each probabilistic stream is delay-T/N, and the probabilistic streams are written into the scheduling task, and these probabilistic streams need to be scheduled, but unlike TT stream scheduling, probability streams from the same ET stream can overlap in the same time interval.
```python
if s.s_type == "Prob":
            for i in range(0,N):
                stream_set1._streams.append(
                    Stream(
                    count,
                    s.src,
                    [s.dst],
                    s.size,
                    s.period,
                    s.deadline-s.period/N,
                    s.jitter,
                    s.pro,
                    s.s_type,
                    str(s._id),
                    s.ot+i*(s.period/N),
                )
                )
                count += 1

```
### 2. Prioritized slot sharing
According to the algorithm in the paper, the TT stream is extended to achieve low latency of ET stream scheduling, but the sharing is not infinite, but the limited expansion of the TT stream on the shared link.
```python
et_processed : Dict[int, Set[int]] = {}
        for s1, s2 in tasks.get_pairs(): 
            if s1.s_type == "Prob" and s2.s_type == "Det" and int(s1.shareOrET) not in et_processed.setdefault(int(s2._id),set()):
                for l in tasks.get_shared_links(s1,s2):  
                    task_var[s2][l]["trans"] += task_var[s1][l]["trans"]
                    et_processed[int(s2._id)].add(int(s1.shareOrET))
            elif s2.s_type == "Prob" and s1.s_type == "Det" and int(s2.shareOrET) not in et_processed.setdefault(int(s1._id),set()):
                for l in tasks.get_shared_links(s1,s2):  
                    task_var[s1][l]["trans"] += task_var[s2][l]["trans"]
                    et_processed[int(s1._id)].add(int(s2.shareOrET))

```
### 3. Prudent reservation
Finally, the algorithm needs to meet the scheduling time slot of the TT flow.
```python
add_frame_const
add_flow_trans_const
add_delay_const(delay should be set 5T-5T/N)
add_link_const
add_queue_range_const
add_frame_isolation_const

```

<chrome-extension://bocbaocobfecmglnmeaeppambideimao/pdf/viewer.html?file=https%3A%2F%2Fpeople.gix.tsinghua.edu.cn%2Fdangfan%2Fpublication%2Ficdcs22-etsn%2Ficdcs22-etsn.pdf>
