The average link utilization model is obtained from observation. The model below is assumed based on random and bursty [[Packets]] arrivals:

![[Network Performance - 2.webp]]

The average queueing delay is related to the average link utilization (traffic intensity). It approaches infinity as the average link utilization approaches 1.

The formula for average link utilization is:
$$
\frac{La}R
$$
where 
- L is packet length in bits, 
- a is average packet arrival rate (packets/second), and 
- R is the link’s bandwidth in bits

>[!IMPORTANT]
>Queueing delay is a convex increasing function of utilization:
>- **If average link utilization 0**, average queueing delay is small
>- **If average link utilization is near 1**, average queueing delay is large
>- **If average link utilization > 1**, average queueing delay is infinite (there’s more work arriving that can be serviced)

