A Generalized code package is produced that could be applied to any reservoir cascade system. This package consists of two main parts: optimization and analysis. The optimization part is written in the Julia programming language and uses the [odows's SDDP.jl](https://github.com/odow/SDDP.jl) to solve the multistage stochastic optimization. The model consists of system, operational, and regulatory constraints and uses the [Gurobi](https://www.gurobi.com/) solver by default. However, changing the solver based on the user requirements is straightforward. To successfully run the model, the user is only required to create these four input data sets into the model (see example_input folder).

* __Cascade_info.xlsx__
  * _arc_cap_ 
    * Each row represents a reservoir in your system, put the corresponding turbine arc capacity into cells 
    * make sure that the order of reservoirs in the row represents the order of reservoirs in your system 
  * _Max_pwr_ 
    * Follow the same procedure as arc_cap 
  * _Cascade_ 
    * Input your cascade system information  
    * make sure that the order of reservoirs in the row represents the order of reservoirs in your system 
    * make sure that in the “name” column you name the reservoir consistently (same number of letters, no numbers, all capital or lowercase. etc) 
    * If some of your reservoirs don’t have “max_decreae” or “max_increase”, leave them empty (Don’t put zero).
  * _Plotting info_ 
    * Follow the same procedure as Cascade 
  * _A_ 
    * A is a connectivity matrix (how water flows in your system) 
    * Use A matrix if travel time in your system is equal to your stage 
  * _A1 and A2_ 
    * A1 and A2 are a connectivity matrix (how water flows in your system) when  
    * Use A1 and A2 when travel time in your system is more than your stage (part of the water that flows from reservoir 1 reaches reservoir 2 in the next stage)		 
* __To use A1 and A2 matrix instead of A matrix__
   *  _In “C1” code_
      *   Got to cell 27 
      * Commnet out line 31 
      * Activate line 32	 
   * _In Code “C2” code_
      * Got to cell 3 
      * Comment out line 119 
      * Activate line 120 
* __Ground_truth.xlsx__
  * This data set is your observed data, which is used to compare your simulation with reality 
  * Make sure each reservoir has its tab and it follows the same name in the “cascade” and “plotting_info” tabs in “Cascade_info.xlsx” 
* __Initial_conditions.csv__
  * Put the initial condition of each of your reservoir  
  * Make sure the order of columns follows the order of the reservoir in your system 
* __Tree.xlsx__
  * Your main scenario trees 
* __Tree #week shifted#.xlsx__
  * Each of them is your shifted scenario tree which is used for the rolling horizon scenario 
* __User_data.csv__
  * Information on your run  
  * You only need to put the values for the “number of stages” and “number of small trees”  
  * Ignore the other rows 
* __Important notes__
  * Keep in mind that Code “!!A” will delete the results of the previous run, so if you need them, rename the “output” folder 
  * If you decided not to use the default units, you have to check the constraint and variables for homogeneity in both units and scale 
  * In some cases, the initial storage of your reservoir can be too high, which may cause the algorithm to run into infeasibility problems. To overcome this issue a vector called “initial_storage_factor”(cell 5 line 11 in code “!!C1” and cell 3 line 10 in code”!!C2”) is defined to reduce the initial storage of reservoirs. For the first run set all values of the vector to 1. If you face an infeasibility error, you should manually reduce the values from 1 to the highest number (less than 1) that won't cause infeasibility (remember to change the vector length according to the number of reservoirs in your system) 
* __Run data__  
  * Number of stages in the main scenario tree 
  * Number of rolling horizon scenario trees 
  * Start date of the decision horizon 
* __Main scenario tree and rolling horizon scenario trees__ 
* __Cascade information__  
  * Minimum storage, maximum storage, spill capacity, minimum release, kc coefficient, number of turbines, the maximum daily rate of release decrease, the maximum daily rate of release increase, evaporation, exclusive flood control, annual flood control, and multiple use, and abbreviation for each reservoir 
  * Turbine arc capacity 
  * Turbine generation capacity 
  * Reservoirs connectivity Matrix: Aij 
* __Initial state of cascade system__  
  * Initial storage 
  * Initial release 
  * Minimum generation contribution required from each reservoir.

The code package also includes a series of scripts written in the Python programming language for analyzing the results. The transition between scripts is performed seamlessly, and no additional task is required from the user. These codes will enable the user to generate tables and graphs to further analyze and visualize the results of the simulations and optimization. To name a few, quantile figures, adaptability figures, spaghetti figures of optimal solutions for the whole cascade system, a Table of the optimal solution of each node, and a Table of solution scenarios are among the features developed for the analysis and post-processing stage. 
