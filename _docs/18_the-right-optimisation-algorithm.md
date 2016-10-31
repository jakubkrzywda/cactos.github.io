---
title: "Select the right optimisation algorithm"
permalink: /docs/tutorials/the-right-optimisation-algorithm/
---

{% include base_path %}

{% include toc %}

Selection of proper optimisation and placement policies is a crucial task that can have a big impact on the total power consumption of a data center and the performance of hosted applications.
In CACTOS we have implemented a set of optimisation and placement services. The most advanced algorithms are wrapped in the **Causa** optimisation and placement services.

## Optimisation
The main configuration file for optimisation is **cactoopt_optimisationalgorithm.cfg**. Other configuration files (if apply) are relevant only for particular optimisation services.

### cactoopt_optimisationalgorithm.cfg
This configuration file allows to choose the optimisation service that will be used for migrations, the algorithm for horizontal autoscaling, and enable resource control (vertical scaling). Available options are listed below.
    
    optimisationName = Causa, Random, LoadBalancing, Consolidation, LinKernighan
    autoscalerAlgorithmName = Hist, AKTE, Reg, or React
    resourceControlEnalbed = true, false
    
The description of the autoscaler algorithms is provided in D3.3 Extended Optimization Model (http://www.cactosfp7.eu/wp-content/uploads/2015/11/D3.3-Extended-Optimization-Model.pdf pp. 23--24).

### cactoopt_opt_causa.cfg
*Relevant only if* optimisationName = Causa *in* **cactoopt_optimisationalgorithm.cfg**.

Sets the migration algorithm used by Causa optimisation service.

    algorithm = NONE, LOAD_BALANCING, CONSOLIDATION, ENERGY_EFFICIENCY, FRAGMENTATION, CP_LOAD_BALANCING, CP_CONSOLIDATION, GD_LOAD_BALANCING, HIGH_TO_LOW_LOAD_BALANCING, SINGLE_MIGRATION_LOAD_BALANCING, SINGLE_MIGRATION_CONSOLIDATION

Enables / disables the control of powering up/down physical servers.

    managePhysicalNodeActions = true, false
    
If the control of powering up/down is enabled, the further configuration is possible by setting the following variables:
    
    minServersOn = 2
    numberOfEmptyServersPoweredOn = 1
    
*minServersOn* specify the minimum number of servers that shall be alwasy powered up and *numberOfEmptyServersPoweredOn* defines the size of the buffer of empty machines that shall be powered up in order to keep available resources for new virtual machines.
    
The description of the migration algorithms is provided in D3.3 Extended Optimization Model (http://www.cactosfp7.eu/wp-content/uploads/2015/11/D3.3-Extended-Optimization-Model.pdf pp. 36--45).

## Placement
The main configuration file for optimisation is **cactoopt_placement.cfg**. Other configuration files (if apply) are relevant only for particular placement services.

### cactoopt_placement.cfg 
This configuration file allows to choose the service that will be used for placement.
    
    placementName = causa, firstFit, bestFitCpu, bestFitMemory, loadBalancing, consolidation

### cactoopt_placement_causa.cfg
*Relevant only if* placementName = causa *in* **cactoopt_placement.cfg**.

Sets the initial placement algorithm used by Causa placement service.

    algorithm = NONE, BEST_FIT,
    LOAD_BALANCING_RAM, CONSOLIDATION_RAM, CONSOLIDATION, FRAGMENTATION, ENERGY_EFFICIENCY,
    MOLPRO_BEST_FIT, MOLPRO_LOAD_BALANCING_RAM, MOLPRO_CONSOLIDATION_RAM

The description of the placement algorithms is provided in D3.3 Extended Optimization Model (http://www.cactosfp7.eu/wp-content/uploads/2015/11/D3.3-Extended-Optimization-Model.pdf pp. 36--45).

MOLPRO_* placement algorithms are aware of special requirements of Molpro jobs depending on the application type (e.g., dft jobs require a computational node with a local storage).
