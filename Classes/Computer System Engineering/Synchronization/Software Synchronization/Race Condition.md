assuming `buffer` and `counter` are shared between two [[Process|processes]]/[[Thread|threads]]. The instructions `counter ++` and `counter --` are not implemented in a single clock cycle (it is not [[Atomic Operation|atomic]])

> [!NOTE] In a situation where several [[Process|processes]] access and manipulate the same data [[Process#Concurrency|concurrently]], the outcome will depend on the order in which the access takes place.

