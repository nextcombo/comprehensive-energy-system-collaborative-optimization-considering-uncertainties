# Comprehensive Energy System Collaborative Optimization Considering Uncertainties in New Energy Output (Matlab Code Implementation) (Matlab Code Implementation)

Table of Contents  
Part One: Literature Review  
1.1 The Product Manufactured by Party A  
1.2 Production According to the Drawings by Party B  
Part Two: Coordinated Optimization Modeling of Electrical Energy Systems Considering Uncertainties in New Energy Generation  
2.1 Introduction  
2.2 Prediction Error Distribution of New Energy Generation  
2.3 Time-Dependent Nature of New Energy Generation  
2.4 Scenario Generation  
2.5 Coordinated Optimization Modeling of Electrical Energy Systems with Capacity Regulation Ability for Temperature Control  
2.6 Nonlinear Constraints on Air Pipeline Gas Flow  
Part Three: Modeling of Subsystems within an Integrated Electric, Gas, and Thermal Energy System  
3.1 Introduction  
3.2 Power Subsystem Modeling  
3.3 Natural Gas Subsystem Modeling  
3.3.1 Construction of Steady State Model for Natural Gas Subsystem  
3.3.2 Linearization of Natural Gas Pipeline Flow Equation  
3.3.3 Natural Gas Pipeline Model  
3.4 Heat Subsystem Modeling  
3.4.1 Heat Source Model  
3.4.2 Heat Network Model  
3.4.3 Heat Load Model  
3.4.4 Conversion of Complicated Pipe Flow Losses  
Part Four: Optimal Multi-energy Flow Solving for Integrated Energy Systems Considering Carbon Emission Costs  
4.1 Introduction  
4.2 Coupling Elements Modeling of Integrated Energy Systems  
4.3 Optimal Multi-energy Flow Model for Integrated Energy Systems  
4.3.1 Objective Function  
4.3.2 Constraint Conditions  
4.3.3 Solving Methodology  
4.4 Case Analysis  
4.4.1 PJM-5 Node Electrical System -7 Node Natural Gas System -6 Node Thermal System Example  
4.4.2 IEEE-39 Node Electrical System -Belgium 20 Node Natural Gas System -6 Node Thermal System Example  
Part Five: MATLAB Code Implementation and Detailed Article
Part 1: Literature Reference "Comprehensive Energy System Collaborative Optimization Considering Uncertainty in New Energy Generation"
0 Introduction
The comprehensive energy system is a system that realizes the complementary and hierarchical utilization of various energies through distribution networks, natural gas networks, wind turbines, photovoltaics, and cogeneration (CCHP) systems.
1.1 Handling Uncertainty in New Energy Generation
The uncertainty in new energy generation mainly refers to the prediction error. To characterize it and improve the accuracy of day-ahead scheduling, this paper first employs a predictive box to statistically analyze historical data to model the distribution of prediction errors. Then, by recursively estimating the covariance matrix to capture the temporal correlation of wind and photovoltaic power, we generate scenarios of possible new energy outputs and reduce multiple scenarios to ease the solution process.
1.1 Prediction Error Distribution in New Energy Generation
1.2 Time Relatedness of New Energy Generation
1.3 Scenario Generation
2. Coordinated Optimization Modeling for Electrical Comprehensive Energy Systems Considering Thermal Control Capability
2.2.1 Nonlinear Constraints on Gas Network Pipeline Airflow
Due to the nonlinearity of the natural gas flow equation, linearization is required. After transformation, the equation is segmented into linear parts.
2.2.1 Linearization of Nonlinear Equation
3. Conversion of Mixed Integer Nonlinear Model
The collaborative optimization model established in Part 2 is a mixed integer nonlinear programming (MINLP) problem, characterized by its NP-hard nature. The challenges in solving MINLP problems include:
① Difficulty in determining whether the obtained solution is globally optimal;
② Decision variables including both integer and continuous variables;
③ The nonlinearity of the problem.
Algorithms for solving MINLP problems include intelligent algorithms, complementary methods, branch and bound algorithms, Bender's decomposition algorithms, and model transformation algorithms [22]. One approach to model transformation involves linearizing the MINLP problem by treating it as a mixed-integer quadratic programming or quadratic programming problem through linearization. This is followed by calling a mature commercial solver to solve the problem. Compared to other algorithms, this method has the advantage of being able to simultaneously address discrete variables while achieving global optimal solutions within a short timeframe. Therefore, this paper adopts segmented linearization and quadratic cone relaxation to linearize the non-linear parts of the model.
The model contains six nonlinear components: Weymouth's equation for pipe gas flow, three nonlinear constraints from CCHP, and two nonlinear constraints from grid power flow.
Editor
Editor
Since the natural gas flow equation is nonlinear, it needs to be linearized. The equation is transformed and then segmented linearized.
3.1 Nonlinear Constraints in Gas Network Pipeline Flows
Segment m=50 (under the premise of pipeline flow direction); if the flow rate is unknown, m=100, with 50 in the first and third quadrants.
(Document cajP18-P19 also presents the segmented linearization treatment of the Weymouth equation, using the same method.)
Section Two: Modeling of the Subsystem of Integrated Energy Systems Comprising Electricity, Gas, and Thermal Energy
2.1 Introduction
2.2 Power Subsystem Modeling
The power subsystem of integrated energy systems often uses an AC power flow model, as shown in equation (2-1).
In the model, P and Q represent the active power and reactive power at nodes respectively; Y represents the node admittance matrix of the power subsystem; U is the vector of node voltages. To reduce the difficulty of solution and subsequent research needs, the power subsystem model adopts a linear model, i.e., DC power flow model, without considering the reactive power and voltage in the power subsystem. The DC power flow equation can be expressed as follows:
In the formula, fll represents the power flowing from point m to point n on line l; B is the admittance parameter of line l; ​editors are the voltage phase angles of nodes m and n at both ends of line l. To ensure the safe and stable operation of the power subsystem, it must meet certain constraints, including generation capacity constraints, ramp-up constraints for units, flow path constraints, and node power balance constraints. These are expressed as follows:  
​editor  
​editor  
2.3 Natural Gas System 2.3.1 Construction of the Steady-State Model for the Natural Gas Subsystem The natural gas subsystem mainly consists of natural gas sources, pipelines, compressors, and load demands, with a structural diagram shown in Figure 2-2.  
​editor  
The modeling of the natural gas subsystem includes the modeling of various components in the system and the modeling of pipeline flow rates. The method of modeling can be analogous to that used in the power subsystem for modeling various components and line flows, as shown in Table 2-1.  
​editor  Natural gas transmission through pipelines is influenced by factors such as temperature, flow rate, and pipeline friction. These factors lead to changes in node pressure and pipeline flow rates. To reduce computational complexity, the natural gas subsystem in integrated energy systems often adopts a steady-state model, ignoring the impact of these factors on node pressure and pipeline flow rates.  
1) Natural Gas Source  
​editor  
2) Node Pressure Constraint  
​editor  
3) Pipeline Flow Rate  
Natural gas pipeline flow rates are related to factors such as pipeline diameter, temperature, and pressure, and are nonlinear. There are multiple formulas for describing the natural gas pipeline flow rate equation, including those from the American Gas Association, Colebrook-White formula, Panhandle A formula, Weymouth formula, etc. In this chapter, we use the Weymouth steady-state model [23l] to describe the natural gas pipeline flow rate, which states that the flow rate is only related to the pressure at both ends of the pipeline and flows from the node with higher pressure to the node with lower pressure. Taking the pipeline k-n in Figure 2-2 as an example, the specific expression for the natural gas flow rate through this pipeline is:  
​editor  
​editor  
4) Compressor
Due to the influence of natural gas's material and external factors during transmission, pressure drops occur. To maintain node air pressure at a normal level and reduce the likelihood of gas pipeline blockages during peak gas load periods, compressors are installed along the natural gas pipeline. Commonly, compressors can be divided into gas compressors and electric compressors [24]. For simplicity in calculations, this article retains only the relationship between node air pressure at both ends of the compressor, disregarding the energy consumed by the compressor. The specific expression is as follows:

Edit (Compression ratio taken as 1.5)
5) Node flow balance equation

2.3.2 Nonlinearization of Natural Gas Pipeline Flow Equation
To reduce the difficulty of solving the subsystem model of natural gas and also simplify the coupling complexity between the power subsystem and the natural gas subsystem, this section linearizes the nonlinear natural gas pipeline flow equation through a segmented linearization method, thereby converting the existing natural gas subsystem model into a mixed integer linear programming model.

Edit
Edit
Edit
Edit
The above segmented linearization process is conducted within the first quadrant of the Cartesian coordinate system. Given the definite direction of natural gas flow in the pipeline, the above analysis method is applicable to any natural gas system. However, in some natural gas systems, such as the Belgium 20-node natural gas system, when the direction of natural gas flow in the pipeline cannot be determined, the above segmented linearization method will no longer apply. Therefore, to obtain a more applicable segmented linear function, the above segmented linearization process is modified to be conducted within the first and third quadrants, where the number of linear segments N=100 is evenly distributed between the first and third quadrants, each containing 50 segments. The other analysis processes remain the same to ensure that natural gas flow in both positive and negative directions is applicable within the pipeline. The improved segmented linearization diagram is shown in Figure 2-4.

Edit
2.3.3 The establishment of the electrical comprehensive energy system collaborative optimization model for the second part of the natural gas pipeline model is a mixed integer nonlinear programming (MINLP) problem.
The product is characterized by being NP-hard. The difficulty in solving the MINLP problem mainly lies in:
1. It's challenging to determine whether the obtained solution is globally optimal;
2. Decision variables include both integer and continuous variables;
3. The problem has nonlinearity. There are several algorithms for solving MINLP problems, including intelligent algorithms, complementary methods, branch and bound algorithms, Bender's decomposition algorithms, and model transformation algorithms [22]. One approach to transforming a MINLP problem into a mixed-integer quadratic programming (MIQP) or quadratic programming (QP) problem involves linearizing the problem through a process of Weymouth linearization, which then calls a mature commercial solver to solve the problem. This algorithm has the advantage of being able to simultaneously address discrete variables and achieve global optimal solutions within a relatively short time frame compared to other algorithms. Therefore, this paper adopts segmented linearization and quadratic relaxation to linearize the non-linear parts of the model.
The model contains six non-linear terms, namely the Weymouth equation for pipe gas flow, three nonlinear constraints from CCHP, and two nonlinear constraints from grid power flow.
Editor
Editor
Since the natural gas flow equation is nonlinear, it needs to be linearized. After reformulating the equation, it undergoes segmented linearization.
Segment m=50 (under the premise of pipe flow direction); if the flow rate is unknown, m=100, with 50 in the first and third quadrants respectively.
(Document CAJP18-P19 also includes the segmented linearization treatment of the Weymouth equation, using the same method.)
2.4 Heat Subsystem Model
The heat subsystem primarily consists of heat sources, heat networks, and heat loads. Its structural diagram is shown in Figure 2-5. In this figure, the heat network consists of a supply network and a return network with identical topological structures. Through the flow of heat medium (hot water or steam in this chapter), the heat network transmits the heat generated by the source to various heat loads. In Figure 2-5, 1 represents the heat source, 2 represents the heat load, solid lines represent the supply system, and dashed lines represent the return system. Below, we will detail the modeling of each component of the heat subsystem.
2.4.1 Common Heat Sources
The common heat sources include combined heat and power (CHP) units, electric boilers (EB), etc.  
(1) CHP Unit Model
Edited by:
Edited by:
The efficiency and capacity of the CHP unit are shown in the figure below (from other literature, only efficiency is used):
Edited = 0.35 50 0 1.5
Output power from the CHP unit. The thermal power generated by the residual heat boiler of the CHP unit.
Edited = 2.58 (2.58 is an empirical value)
Edited 
Gas turbine consumption of natural gas:
Edited by:
(2) Electric Boiler Model (EB)
Edited by:
The efficiency of this article is set to 0.85.
2.4.2 Heat Network Model
Edited by:
Edited by:
Edited by:
2.4.3 Heat Load Model
2.4.4 Complicated Pipe Flow Loss Conversion
Part Three: Optimal Multi-energy Flow Solving Considering Carbon Emission Costs
3.1 Introduction
3.2 Coupling Element Modeling of Integrated Energy System - Electricity Subsystem and Natural Gas Subsystem Interact through Gas Turbine, which has fast ramping capability and flexible startup/shutdown characteristics. Unlike conventional coal-fired generating units, gas turbines consume natural gas and generate electrical power. In the electricity subsystem, gas turbines appear as a source of power, while in the natural gas subsystem, they appear as a load. Generally, the electrical power generated by gas turbines is only considered active power, irrelevant to reactive power. The relationship between the amount of natural gas consumed by gas turbines and the active power generated is as follows:
Edited in:
In the formula, Hg represents the amount of natural gas consumed by the gas turbine; ag represents the conversion coefficient of the gas turbine; Pgas represents the active power generated by the gas turbine.
The typical CHP units in the power generation system burn natural gas, oil, or biogas to generate electricity and use thermal recovery devices to capture heat from the turbines. To enhance the coupling effect between electricity, natural gas, and thermal energy, this chapter sets the CHP units in the thermal subsystem as gas-fired CHP units, coupling electricity, gas, and heat through the gas CHP units. Like gas-fired generators, gas-fired CHP units consume natural gas and produce active power, with their conversion relationship also being defined by the same editor.
3.3 Optimal Multi-Energy Flow Model for Electricity, Gas, and Thermal Energy
To achieve low-carbon economic operation of a comprehensive energy system, this section constructs an optimal multi-energy flow linear solver model for multiple time periods that takes into account carbon emission costs. The objective function aims to minimize the total operational cost and carbon emission cost of the comprehensive energy system. The total operational cost includes the operating costs of coal-fired generators, gas-fired generators, and CHP units, as well as the output cost of natural gas sources. Additionally, since different generators consume different fuels and emit different amounts of carbon dioxide per unit of electric power, the carbon emission coefficient is used to calculate the carbon emissions of different generators, and the comprehensive energy system's carbon emission cost is calculated using carbon tax (carbon tax).
3.3.1 Objective Function
​Edit
​Edit
​Edit
​Edit
3.3.3 Solving Method
In Chapter 2, the linearization of the natural gas pipeline flow equation was conducted, converting the comprehensive energy system model into a mixed integer linear programming model. For the optimization model constructed in this chapter, branch and bound method was selected for solving, and the Cplex solver from GAMS software was called to unify the solution of the model constructed in this chapter.
3.4 Example Analysis
3.4.1 PJM-5 Node Electric Power System - 7 Node Natural Gas System - 6 Node Heating System Example
This section studies the comprehensive energy system composed of the PJM-5 node electric power system, 7 node natural gas system, and 6 node heating system. The diagram of the coupled electric-gas-heat comprehensive energy system is shown in Figure 3-1.
Editor
3.4.2 Examples of IEEE-39 Node Power System - Belgian 20 Node Natural Gas System - 6 Node Thermal System Coupling
The comprehensive energy system, composed of the P.JM-5 node power system, 7 node natural gas system, and 6 node thermal system coupled together, has proven the accuracy and effectiveness of the proposed model in reducing carbon emissions and total costs. This section continues to study the comprehensive energy system formed by the coupling of the IEEE-39 node power system, the Belgian 20 node natural gas system, and the 6 node thermal system, as shown in Figure 3-5.
Editor
This example sets both generators at nodes 33 and 37 in the IEEE-39 node power system as gas generators, with the consumed natural gas provided by nodes 6 and 19 in the Belgian 20 node natural gas system; a CHP unit is set up at node 30, which also serves as a heat source connected to node 1 in the 6 node thermal system. The Belgian 20 node natural gas system includes 6 sources of gas and 9 natural gas loads. The thermal source in the 6 node thermal system includes a CHP unit and an electric boiler, whose electricity consumption is provided by the CHP unit. To increase the coupling strength between electricity, gas, and heat, the CHP unit is set as a gas unit, with the consumed natural gas provided by node 3 in the natural gas system. Data for the IEEE-39 node power subsystem are taken from standard data in the MATPowER toolkit, while detailed network parameters for the natural gas subsystem are presented in Appendix B. The thermal subsystem data are the same as in the previous section.
(1) Electricity Data
(Second-order cone model, data identical to matpower39 node, with two generators changed to gas generators)
Total of 10 generating units, total installed capacity of 6967MW, total electrical load of 5941.5MW.
Grid node 33
Gas turbine
Node 6 in the gas network supplies gas
Grid node 37
Gas turbine
Node 19 in the gas network supplies gas
Grid node 30
CHP unit
Node 3 in the gas network supplies gas
The heat source of Node 1 in the thermal network.
The remaining 7 power nodes
Coal-fired power units
The IEEE-39 node power system consists of 10 generating units, with a total installed capacity of 6967MW and a total electricity load of 5941.5MW. The cost coefficients for coal-fired and gas-fired generating units are shown in Table 3-5.
Editor
The 20-node natural gas subsystem in Belgium includes six gas sources and nine gas loaders. Among them, there are seven conventional gas loaders and two gas turbine generator loaders, with a total load of 2.4608 edits. The cost of gas source output is set at 0.085 edit (#1-3 gas sources) and 0.062 edit (1#4-6 gas sources).
(2) The basic parameters of the natural gas subsystem, such as Table 3-6, are shown here.
Editor
The thermal subsystem includes a CHP unit, an electric boiler, and three heat loads, with a total load of 50MW. The electrical heating ratio coefficient for the electric boiler is set at 0.8, and its maximum thermal output is set at 30MW. The basic parameters of the CHP unit are shown in Table 3-7.
(3) Annex B: Data for the 20-node natural gas system in Belgium
Editor
Part Four: MATLAB Code Implementation and Detailed Article. This article only showcases a portion of the code, all code and detailed articles can be found in:
Editor
1. Product Technical Requirements
%%\n% Flow Equations\n% Branch Current Constraints\nfor t = 1: n_T\n    C = [C,\n        PF_D(:, t) == Bf*Va(:, t) + Pfinj,\n        ]; \nend\n%%\n% Node Power Balance Constraints (Matrix Form)\nGenIncMatrix = zeros(n_bus, n_gen); \nfor i=1:n_gen\n    GenIncMatrix(gen(i,GEN_BUS),i)=1; \nend\nPowerEBoilerIncMatrix = zeros(n_bus,n_EBoiler); \nfor i=1:n_EBoiler\n    PowerEBoilerIncMatrix(EBoiler(i,2),i)=1; \nend\nfor t = 1: n_T\n    C = [C,\n        GenIncMatrix*gen_P(:,t)-PD(:,t)-PowerEBoilerIncMatrix*PowerEBoiler(:,t) ==  Bbus*Va(:,t)+Pbusinj,\n        ]; \nend\n
​  

## Images

![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](01.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](02.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](03.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](04.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](05.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](06.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](07.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](08.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](09.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](10.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](11.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](12.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](13.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](14.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](15.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](16.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](17.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](18.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](19.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](20.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](21.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](22.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](23.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](24.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](25.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](26.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](27.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](28.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](29.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](30.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](31.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](32.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](33.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](34.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](35.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](36.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](37.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](38.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](39.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](40.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](41.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](42.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](43.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](44.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](45.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](46.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](47.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](48.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](49.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](50.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](51.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](52.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](53.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](54.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](55.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](56.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](57.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](58.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](59.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](60.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](61.png)
![Coordinated Optimization of Electrical Equipment Comprehensive Energy System Considering Uncertainty of New Energy Generation (Matlab Code Implementation) (Matlab Code Implementation)](62.png)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
