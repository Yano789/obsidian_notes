![[Packet Loss-1.webp]]

[[Packets]] that arrive at a full queue (full buffer) will be dropped (lost). They may be retransmitted by the previous node, source system, or not at all. Loss is random, where each link has an average loss rate or probability.

You can compute end-to-end loss rate probability given per-link loss rate probability. 
$$
(1-(1-\text{loss rate 1})(1-\text{loss rate 2}))\times100\%
$$
For example, given the following network topology and per-link loss rate:
![[Packet Loss.webp]]

We can compute the end-to-end loss rate between A to C as: (1−(0.8∗0.9))∗100%=28%

