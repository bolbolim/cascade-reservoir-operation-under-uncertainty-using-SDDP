A Generalized code package is produced that could be applied to any reservoir cascade system. This package consists of two main parts: optimization and analysis.
The optimization part is written in the Julia programming language and uses the SDDP.jl package \cite{dowson_sddp.jl} to solve the multistage stochastic optimization. The model consists of system, operational, and regulatory constraints and uses the Gurobi \cite{gurobi} solver by default. However, changing the solver based on the user requirements is straightforward. To successfully run the model, the user is only required to create these four input data sets into the model.
•	Run data
o	Number of stages in the main scenario tree
o	Number of rolling horizon scenario trees
o	Start date of the decision horizon
•	Main scenario tree and rolling horizon scenario trees
•	Cascade information 
o	Minimum storage, maximum storage, spill capacity, minimum release, kc coefficient, number of turbines, maximum daily rate of release decrease, maximum daily rate of release increase, evaporation, exclusive flood control, annual flood control and multiple use, and abbreviation for each reservoir
o	Turbines arc capacity
o	Turbines generation capacity
o	Reservoirs connectivity Matrix: Aij
•	Initial state of cascade system
o	Initial storage
o	Initial release
o	Minimum generation contribution required from each reservoir.

The code package also includes a series of scripts written in the Python programming language for analyzing the results. The transition between scripts is performed seamlessly, and no additional task is required from the user. These codes will enable the user to generate tables and graphs to further analyze and visualize the results of the simulations and optimization. To name a few, quantile figure, adaptability figure, spaghetti figures of optimal solutions for the whole cascade system, Table of the optimal solution of each node and Table of solution scenarios are among the features developed for the analysis and post processing stage.
