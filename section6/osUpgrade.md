Q: We need to take node01 out for maintenance. Empty the node of all applications and mark it unschedulable.

A: kubectl drain node01 --ignore-daemonsets
node/node01 cordoned

Q: The maintenance tasks have been completed. Configure the node node01 to be schedulable again.

A: kubectl uncordon node01


Q: 
hr-app is a critical app and we do not want it to be removed and we do not want to schedule any more pods on node01.
Mark node01 as unschedulable so that no new pods are scheduled on this node.

A: kubectl cordon node01