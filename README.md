# Scheduling-a-dual-resource-flexible-Job-Shop-with-sequence-dependent-setup-times
This repository contains the data supporting the study "Scheduling a dual-resource flexible Job-Shop with sequence-dependent setup times: An industrial case study in garment manufacturing".

They are 79 instances for each class of instance A,B,C,D for a total of 316 instances.
The format of instances is as follows, for notations users are referred to the paper:

## Instance format description
* **Line 1**: instance date in format YYYY-MM-DD, not used
* **Line 2**: $k$, the number of machines
* **Line 3**: $h$, the number of operators
* **Line 4**: $n$, the number of jobs
* **Line 5**: $\tau^{thread}$, duration of the thread pool change (in minutes)
* **Line 6**: $\tau^{config}$, duration of the machine configuration change (in minutes)
* **Line 7**: $\tau^{type}$, duration of the operation type change (in minutes)
* **Line 8**: $\tau^{exp}$, duration of the experience setup (in minutes)
* **Line $9:(9+k-1)$**: list of machines\
    For each line: _ma_id_[^1] _nb_config_[^2] $type$[^3]
* **Line $x=(9+k)$**: jobs and operations:\
    For $i=0..(n-1)$:
    * Line $x+1$: _job_id_[^4] _color_id_[^5] _delivery_date_[^6] $d_i$[^7] _nb_op_[^8] OF[^9]
    * For $j=0..(_nb_op_-1)$:
        * Line $x+2$: _op_id_[^10] $q_{ij}$[^11] _config_id_[^12] _nb_machines_[^13] _nb_operators_[^14] _operation_type_[^15]
        * Line $x+3$: Preceding operations. The first number identify the number of preceding operations, then the preceding operation ids are listed\
        _nb_prec_[^16] [_op_id_ for l=0.._nb_prec_]
        * Line $x+4$: List of compatible machines [_ma_id_[^1] for l=9.._nb_machines_]
        * Line $x+5$: List of compatible operators. 3 numbers for each, _op_id_[^17] $p_{ijh}$[^18] exp[^19]

---
## Notes
* The due date of jobs $d_i$ is computed from the instance date, delivery date of job $i$ and assuming the following number of working hours per week day ${'Mon': 7.67, 'Tue': 7.67, 'Wed':7.67, 'Thu': 7.67, 'Fri': 4.34, 'Sat': 0, 'Sun': 0}$
* The set of operation types $T$ is derived from _operation_type_[^15] of operations
* The binary parameter $\delta_{ijt}$ is determined from the set $T$ and the _operation_type_[^15] of operations
* The binary parameter $\delta_{ijlg}^{type}$ between pairs of operations $o_{ij}$ and $o_{lg}$ is derived from $\delta_{ijt}$
* The binary parameter $\delta_{ijlg}^{config}$ between pairs of operations $o_{ij}$ and $o_{lg}$ is computed from the machine configuration required for operations _config_id_[^12]
* The binary parameter $\delta_{il}^{thread}$ between pairs of jobs $i$ and $l$ is computed from the thread color of jobs _color_id_[^5]
---
[^1]: id of the machine
[^2]: the number of configuration on the machine (identified from 0 to _nb_config-1_)
[^3]: int to identify the type of machine (not used)
[^4]: id of the job ($i$)
[^5]: id for the thread color of the job, thread change setups occur between different _color_id_
[^6]: Delivery date of the job in format YYYY-MM-DD 
[^7]: Due date (in minutes) computed from the instance date and delivery date assuming working hours 
[^8]: The number of operations in the job ($O_i=0..$_(nb_op-1))_
[^9]: OF of the job (not used) 
[^10]: id of the operation ($j$)
[^11]: nominal workload value of the operation
[^12]: configuration id required on the machine 
[^13]: number of compatible machines (_nb_machines_ =$|A_{ij}|$)
[^14]: number of compatible operators (_nb_operators_=$|B_{ij}|$)
[^15]: operation type, setups occur between successive operations with different types (used to define $\delta_{ijt}$)
[^16]: number of operations preceding the current operation (_nb_prec_ $=|R_{ij}|$)
[^17]: id of the operator 
[^18]: processing time of the operation for the operator ($p_{ijh}$)
[^19]: initial experience level for the operation type ($\epsilon_{ht}$)
