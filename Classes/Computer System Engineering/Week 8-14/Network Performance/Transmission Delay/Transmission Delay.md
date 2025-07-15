Transmission delay (also known as transmission time) is primarily determined by how **fast** the bits are pushed into the link

![[Transmission Delay - 1.png]]

**Duration**: varies, depends on bandwidth (link technology). The amount of transmission delay is computed as: 
$$
d_{trans}=\frac{L}R
$$
where 
- L is packet length in **bits** and 
- R is link bandwith in bits per second.

**Cause**: Need time to push the whole packet bits, e.g: 512 Bytes from the router to the link itself.