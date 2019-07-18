# carme-slurm-node-weight-shuffle

Considering SLURM **carme-slurm-node-weight-shuffle.sh** is perhaps the most unusual script we have. In the _slurm.conf_ we can define many things and set a lot of default values and parameters for partitions. And there is nearly nothing that you cannot configure. The only problem is you have to know how to do it.

One thing that cannot be configured is the order nodes where used. This is first of all fine and on 90% or the clusters available no problem at all. But there are exceptions. Therefore lets consider the following situation. The number of nodes with GPUs is larger than the number of users on the system that need GPUs. On most clusters this is no problem at all, as the nodes are then used by users that need no GPUs but CPUs. But lets say we want to set up a pure GPU cluster for users that rely on GPUs. If the usage of the cluster is not very high. New jobs will always start on the same nodes. Which is fine. But we have to keep one thing in mind. If the GPU is used the temperature can go up to 95°C. So if the same GPUs are used again and again the will die much earlier than the GPUs that are not used that often. Therefore it can be useful the shuffle the order of the nodes that are allocated by jobs. This can be done in SLURM by adding a **Weight** factor to the definition of a node.

The script goes through all the nodes defined in _CARME\_COMPUTENODES\_1_ (, _CARME\_COMPUTENODES\_2_ and _CARME\_COMPUTENODES\_3_) in _CarmeConfig_, generate a random number and set this random number as new weight of the node.