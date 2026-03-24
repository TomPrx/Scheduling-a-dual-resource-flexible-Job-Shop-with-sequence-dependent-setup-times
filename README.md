# Scheduling-a-dual-resource-flexible-Job-Shop-with-sequence-dependent-setup-times
This repository contains the data supporting the study "Scheduling a dual-resource flexible Job-Shop with sequence-dependent setup times: An industrial case study in garment manufacturing".

They are 79 instances for each class of instance A,B,C,D for a total of 316 instances.
The format of instances is as follows, for notations users are referred to the paper:

## Instance format description
1. Line 1: instance date in format YYYY-MM-DD, not used
2. Line 2: $k$, the number of machines
3. Line 3: $h$, the number of operators
4. Line 4: $n$, the number of jobs
5. Line 5: $\tau^{thread}$, duration of the thread pool change (in minutes)
6. Line 6: $\tau^{config}$, duration of the machine configuration change (in minutes)
7. Line 7: $\tau^{type}$, duration of the operation type change (in minutes)
8. Line 8: $\tau^{exp}$, duration of the experience setup (in minutes)
9. Line $9-(9+k-1)$: list of machines\
    For each line: $ma\_id$[^1] $nb\_config$[^2] $type$[^3]
11. Starting from line $x=(9+k)$ are the jobs and operations:\
    For $i=0..(n-1)$:
    * Line $x+1$: job_id[^4] $color\_id$[^5] $delivery\_date$[^6] $d_i$[^7] nb_op[^8] OF[^9]
    * For $j=0..(nb\_op-1)$:
        * Line $x+2$: $op\_id$[^10] $q_{ij}$[^11] $config\_id$[^12] $nb\_machines$[^13] $nb\_operators$[^14] $operation\_type$[^15]
        * Line $x+3$: Preceding operations. The first number identify the number of preceding operations, then the preceding operation ids are listed\
        $nb\_prec$[^16] [$op\_id$ for l=0..$nb\_prec$]
        * Line $x+4$: List of compatible machines [$ma\_id$[^1] for l=9..$nb\_machines$]
        * Line $x+5$: List of compatible operators. 3 numbers for each, $op\_id$[^17] $p_{ijh}$[^18] exp[^19]

---
## Notes
* The due date of jobs $d_i$ is computed from the instance date, delivery date of job $i$ and assuming the following number of working hours per week day ${'Mon': 7.67, 'Tue': 7.67, 'Wed':7.67, 'Thu': 7.67, 'Fri': 4.34, 'Sat': 0, 'Sun': 0}$
* The set of operation types $T$ is derived from $operation\_type$[^15] of operations
* The binary parameter $\delta_{ijt}$ is determined from the set $T$ and the $operation\_type$[^15] of operations
* The binary parameter $\delta_{ijlg}^{type}$ between pairs of operations $o_{ij}$ and $o_{lg}$ is derived from $\delta_{ijt}$
* The binary parameter $\delta_{ijlg}^{config}$ between pairs of operations $o_{ij}$ and $o_{lg}$ is computed from the machine configuration required for operations $config\_id$[^12]
* The binary parameter $\delta_{il}^{thread}$ between pairs of jobs $i$ and $l$ is computed from the thread color of jobs $color\_id$[^5]
---
[^1]: id of the machine
[^2]: the number of configuration on the machine (identified from 0 to $nb\_config-1$)
[^3]: int to identify the type of machine (not used)
[^4]: id of the job ($i$)
[^5]: id for the thread color of the job, thread change setups occur between different $color\_id$
[^6]: Delivery date of the job in format YYYY-MM-DD 
[^7]: Due date (in minutes) computed from the instance date and delivery date assuming working hours 
[^8]: The number of operations in the job ($O_i=0..(nb\_op-1)$)
[^9]: OF of the job (not used) 
[^10]: id of the operation ($j$)
[^11]: nominal workload value of the operation
[^12]: configuration id required on the machine 
[^13]: number of compatible machines ($nb\_machines=|A_{ij}|$)
[^14]: number of compatible operators ($nb\_operators=|B_{ij}|$)
[^15]: operation type, setups occur between successive operations with different types (used to define $\delta_{ijt}$)
[^16]: number of operations preceding the current operation ($nb\_prec=|R_{ij}|$)
[^17]: id of the operator 
[^18]: processing time of the operation for the operator ($p_{ijh}$)
[^19]: initial experience level for the operation type ($\epsilon_{ht}$)
