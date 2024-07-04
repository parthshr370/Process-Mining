## Applying Decision Trees

1. **Information Gain** tells us the reduction in entropy in decision trees 
2. It quantifies how much knowing the value of an attribute improves our ability to predict the target variable
3. Information Gain measures *how much the attribute A reduces the uncertainty in the dataset*.
4. **Veracity** refers to the *trustworthiness*, *reliability*, and *quality of the data*. In the context of big data, veracity addresses issues such as the *accuracy, consistency, and credibility of the data*


## Core Process Mining 

1. Process Mining road-map has **4 major steps** 
2. *Question* -- *Data extraction -- Data Analysis -- Presentation* 
3. We just need a CSV file with 3 major properties **Case** , **Activity** and **Timestamp**.
4. Each case will have activities in a certain order. Maybe the Order goes like A B C D E , while other A C B D E. Here C happens before B which can be possible if C represents payment which can occur at anytime.
5. Maybe E represents Invoice generation that can only happen when the whole order is completed and the money is received 
6. Some process might take average of 20 days to complete and we can see the graph that most of the processes complete in this time frame . But some at the very end are taking a lot of time ( 80 + days ) And it is not a outlier but rather a common occurrence. We can then take out those processes where we have control over them. This is where we try to improve our model\
7. *Frequency view* tells you about the number of instances it takes to reach from one case to another.
8. *Performance view* on the other hand tells you where the bottlenecks are where the most time in the whole process( with red colour )
9. We might find unnecessary feedback loops which takes up a lot of time in cases
10. Processes are rather an abstract concept but the performance view really helps you to visualise a lot of stuff 
11. Some compliance guidelines are present in each process flow to ensure there are no fraud. There is need for creating a purchase order at the end of P2P to prevent fraud cases 
12.  **Play-Out**: Using a process model to generate possible event logs (simulation of processes).
	- **Play-In**: Using event logs to discover or construct a process model (data-driven model discovery).

13. Process Discovery - Play In model 
14. Conformance Checking = Replay 
15. **Ways to get Event Data -** 
     - *Database System* ( Patient Data in Hospital )
     - *Comma Separated* Value file or Spreadsheet 
     - *Transaction Log* ( Trading System )
     - *Business Suite* / ERP System ( SAP, Oracle etc)
     - *Message Log* ( from IBM Middleware )
     - *Open API Providing Data from Websites* or social media 

16. Mapping Email to Event Log - 
    -  Sender ( from ) - *Resource* 
    - A set of receivers ( To ) - *Activity Name* 
    - A subject - *Case ID* 
    - A timestamp( Date ) - *Timestamp* 
    - Body - *Other Data*

17. Perspectives to Flow - 
    - Control Flow 
    -  Data flow 
    - Time 
    - Resources 
    - Cost 
    - Risks

18. Ways to **represent control flow** 
    - BPMN
    - UML 
    - Event Driven Process Chains 
    - Petri Net Variants 
    - Casual Nets 
    - Hidden Markov Chains 
    - Process Algebra ( CSP )
    - Fuzzy Models 
    - YAWL Model 
    - Declare Model 

19. The best models is the one that captures reality really well based on what the end user needs 
20. Fuzzy models are not executable like petri nets but they allow for simpler representation 
21. Traffic Light Petri Net 
	 - Network is **static** and composed of places and transitions 
	 - Places instead *hold tokens where tokens can move* but the whole architecture remains the static 
	 - Transitions produce or consume tokens 
	 - Marking is the state of the token it may be present at A  in a process chain of ABCDE


22. Reachability Graph help us describe distributed systems, Rechability graph helps us explore the possible states of petri nets 
### 1. **Understanding Petri Nets**

A Petri net consists of:

- **Places (P):** Represent states or conditions.
- **Transitions (T):** Represent events that may change the state.
- **Tokens:** Used to mark the places, indicating the current state of the system.
- **Arcs:** Connect places to transitions and transitions to places, indicating the flow.

### 2. **Marking**

A **marking** is a distribution of tokens across the places. It represents a specific state of the Petri net. The initial marking is the starting state of the system.

### 3. **Reachability Set**

The reachability set is the collection of all possible markings that can be reached from the initial marking by firing a sequence of transitions.

### 4. **Reachability Graph**

The reachability graph is a directed graph where:

- **Nodes (Vertices):** Represent markings.
- **Edges (Arcs):** Represent the firing of transitions that change one marking to another.

#### Constructing the Reachability Graph:

1. **Start from the Initial Marking:** Begin with the initial marking M0M_0M0​.
2. **Generate New Markings:** For each marking MMM, determine all possible transitions that can fire. For each transition that can fire, compute the new marking M′M'M′.
3. **Create Nodes and Edges:**
    - Add M′M'M′ as a new node if it hasn't been encountered before.
    - Draw a directed edge from MMM to M′M'M′ labeled with the transition that led to M′M'M′.
4. **Repeat:** Continue this process for each new marking M′M'M′ until no new markings can be generated.

### Example

Consider a simple Petri net with:

- Two places: P1,P2P1, P2P1,P2
- One transition: T1T1T1
- Initial marking: M0=(1,0)M_0 = (1, 0)M0​=(1,0) (one token in P1P1P1, none in P2P2P2)

#### Steps to Create the Reachability Graph:

1. **Initial Marking:** M0=(1,0)M_0 = (1, 0)M0​=(1,0)
2. **Fire Transition T1T1T1:**
    - T1T1T1 is enabled if there is a token in P1P1P1.
    - Firing T1T1T1 moves the token from P1P1P1 to P2P2P2, resulting in the new marking M1=(0,1)M_1 = (0, 1)M1​=(0,1).
3. **Create Nodes and Edges:**
    - Nodes: M0,M1M_0, M_1M0​,M1​
    - Edge: M0→T1M1M_0 \xrightarrow{T1} M_1M0​T1​M1​
4. **Further Transitions:**
    - In M1=(0,1)M_1 = (0, 1)M1​=(0,1), T1T1T1 cannot fire (no token in P1P1P1).
    - Therefore, no new markings are generated.

The reachability graph consists of:

- Nodes: M0,M1M_0, M_1M0​,M1​
- Edge: M0→T1M1M_0 \xrightarrow{T1} M_1M0​T1​M1​



23. Boundedness 
   - A place p is k bounded if there is no reachable marking with more than k tokens in p 
   - A petri net is k bounded if all places are k bounded 
   - A place/petri net is bounded if there exists such a k
   - P2 is 2 bounded because the total number of tokens in p1 and p2 is 2 
   - A safe place/petri net is 1 bounded

24. Deadlock 
   -  Marking is dead if no transition is enavles in it 
   - Petri net has a potential deadlock if there is reachable dead marking 
   - Petri net is deadlock free if each reachable marking enables at least one transition 

25. Liveness
  - Transition t is live if from any reachable marking it is possible to reach a marking that enables t 
  - Petri net is live if all transitions are live 
  - A live petri net is deadlock free but the reverse is bi

26. Questions we need to ask 
   - Is the petri net bounded 
   - Is the petri net safe 
   - Is the petri net deadlock free 
   - Is the petri net live 


## Different Types of Process Models

27. Naive approach for classification 
   - **True positives** - Traces possible in model and also possible in real process 
   - **True Negative** - Traces not possible in model and also not possible in real process 
   - **False Positive** - Traces possible in models but not possible in real process 
   - **False Negative** - Traces not possible model but possible in real process 

28. It is difficult to apply classic examples of *recall* and *precision* to this.
29. We can never find any negative examples in the event log since there is none 
30. Log contain only a fraction of possible traces 
31. **Things we care about in process model** - 
   - Fitness 
   - Simplicity 
   - Precision 
   - Generalisation 

32. Due to **concurrency** , loops and choices the search space has complex structures and the log typically contains only a fraction of all possible behaviour 
33. There is no direct relation between the size of the model and its behaviour ( smaller model may generate more or less behaviour although classical analysis and evaluation methods typically assume some monotonic property )
34. **Vicious cycle paradox** - 
   - If one blocks , *both should block* (due to symmetry)
   - If both block then *there will never be a second token*. Hence the choice to block was wrong 
   - If one is not blocked both *can potentially progress* (due to symmetry)
   - If both progress there will be e second token hence the choice to progress was wrong 

35. **Fuzzy models** in process mining refer to a type of process modelling that handles uncertainty and imprecision in event data. They are particularly useful when dealing with complex and unstructured processes where traditional process models may struggle to accurately capture the variability and ambiguities present in the observed data. Here’s an overview of fuzzy models in the context of process mining:
36. **C-net**, or "**Causal net**," is a type of process model *used in process mining to represent the causal relationships between different activities in a process*. Unlike other models that may focus more on sequences and structures, C-nets are particularly designed to capture and emphasize causality, making them useful for understanding how activities influence one another directly.
37. Learning **Transition Systems** - Two phase approach 
     - Create a transition system from the event log 
     - Convert the transition system to a petri net by detecting concurrency  - The petri net is then converted to BPMN 

38. **Defining states in a a transition system** 
    - *Past Focused* - Activities and their order before a given point 
    - *Future focused* - Known future activities from a point in complete traces 
    - *Combined* - Past and future activities 

39. State Abstractions
	- **Full Sequence**: Order and frequency of all activities.
	- **Set Abstraction**: Activities without order or frequency.
	- **Multiset Abstraction**: Frequencies without order.
	- **Time Window (k-tail)**: Last k events.

40. Practical Application
	- **Attributes in Event Logs**: States can incorporate resources, locations, costs, etc.
	- **Filtering**: Remove infrequent paths and activities.
	- **Postprocessing**:
	    - Remove self-loops.
	    - Improve diamond structures for concurrency.
	    - Merge states with similar inputs/outputs.


41. State based region - We lock in a certain area in the petri net and then try to apply certain rules in the area (like a should always leave the area, b should always enter the area )
42. A region is a set of states such that if a transition exits the region then all the equally labelled transitions exit the region and it a transition enters the region then all equally labelled transitions enter the region. All events not entering or exiting the region do not cross the region.
43. We need to select the right region to get the best process model 
44. At max the number of regions that a graph can have is 2(n+1) regions and have 2^n states 
45. Every subset of states for a region.Hence there are 2^(n+1) regions 
46. We only include the non-trivial minimum regions 
47. **Non Trivial** 
    - The empty set and the set of all states are regions by definition 
    - These trivial regions carry no information and should not be included 

48. **Minimal**
    - A region is minimal if it cannot be decomposed into smaller (non trivial) ones 
    - Non minimal regions are implied by smaller ones and should not be included 


49. Basic **Algo to construct a petri net** 
    1. For each transition label in the transition system a transition is added to the petri net 
    2. The *minimal non trivial regions* are computed 
    3. For each minimal non trivial region in the transition system a place is added to the petri net 
    4. The corresponding *arcs* are generated
    5. The *token* is added to each place that corresponds to a regions containing the initial state 
    6. The resulted petri net is called the minimal saturated net

## Process Discovery Techniques and Conformance checking 

50. Weakness of approach based on state ased regions 
    - Inability to discover particular process constructs ( can be handled through extensions of the basic algorithm)
    - Inability to balance the four forces (fitness, precision, generalisation and simplicity)

51. Petri net can simulate the behaviour of the transition system but not the other way around ( no bisumlation)
52. Region based techniques can be used to discover complex process patterns 
53. Provide insights into the essence of process discovery 
54. But - 
     - Over-fitting may be a problem (make sure the initial transition system is general enough)
     - Inability to leave out infrequent behaviour ( but can be done by transition systems)
     - Noise and incompetence cannot be handled well 

55. We had *alpha algorithm* , *state based algo* and now the third one ***Language based region*** that says -
     - Says places will never go negative 
     - any solution (x,y,c) is a region 
     - Any region (x,y,c) is a feasible place ( acts like linear algebra )
56. Genetic Mining 
     - For larger processes or event logs - Very Very slow 
     - Very flexible - easy to add new forces ( add quality measures)
     - Often used when confronted with a new question followed by a more efficient approach 

57. We split an event log and create a big matrix first . T*he bigger matrix is then split into more and more common properties until it cannot be reduced* 
58. **Audits** are performed to ascertain the validity and reliability of information about organisations and their associated processes 
59. This is done to check *whether business processes are executed within certain boundaries set by managers* governments and other stakeholders 
60. **Conformance checking approaches** - 
    - Conformance checking using casual footprints 
    - Conformance checking based on token based replay 
    - Alignment based conformance checking 

61. Casual footprints in conformance checking refer to the analysis and comparison of actual process execution logs with a predefined process model to identify and understand deviations.
62. **Limitations** - 
    - Frequencies are not used 
    - Behaviour is only considered indirectly (DFG)
    - Aims to capture fitness precision and generalisation of a single metric

63. It captures various behaviour like - 
	1. **Directly Follows Relations**: This indicates that one activity directly follows another in a sequence.
	2. **Causal Relations**: This shows a dependency where one activity causes or enables the occurrence of another.
	3. **Parallel Relations**: This identifies activities that can occur concurrently.
	4. **Choice Relations**: This captures branching behavior where different activities may follow a given activity based on conditions or decisions.

64. Benefits of Casual Footprints in Conformance Checking
	- **Detection of Deviations**: Helps in identifying where the real process deviates from the model, allowing for corrective actions.
	- **Understanding Process Behavior**: Provides insights into actual process flows and their alignment with the intended design.
	- **Improvement Opportunities**: Highlights inefficiencies, bottlenecks, and areas where the process can be improved.
	- **Compliance and Quality Assurance**: Ensures that processes comply with regulatory requirements and internal standards.

65. **Token-Based Replay Mechanism**
	1. **Initialization**: Start by placing tokens in the initial places of the Petri net.
	2. **Replay Events**: For each event in the event log, fire the corresponding transition in the Petri net if it is enabled.
	3. **Token Movement**: When a transition fires, tokens are consumed from the input places and produced in the output places.
	4. **Check Conformance**:
	    - **Fit**: The event can be replayed according to the model.
	    - **Deviations**: If an event cannot be replayed because the corresponding transition is not enabled, it indicates a deviation between the model and the observed behavior.

66. **Example Scenarios**
	1. **Perfect Fit**:
	    - The model perfectly matches the event log, meaning every event can be replayed without deviations.
	2. **Missing Events**:
	    - Some events in the log cannot be replayed because the corresponding transitions are not enabled in the model at the required time.
	3. **Extra Events**:
	    - The model allows for certain transitions that do not appear in the event log, indicating over-generalization.
	4. **Incorrect Ordering**:
	    - The sequence of events in the log does not match the sequence allowed by the model.
	
	**Common Issues and Solutions**
	
	- **Missing Tokens**: Introduce artificial tokens to allow for the continuation of the replay, marking the missing tokens as deviations.
	- **Unmatched Events**: Log the unmatched events and provide feedback to adjust either the model or the process to improve alignment.

67. Aligning Observed and Modeled Behavior
	**Aligning Techniques**
	
	1. **Synchronous Moves**: Both the model and the log move in tandem, matching events directly to transitions.
	2. **Model Moves**: Only the model moves, usually to consume tokens that are not matched by any event in the log.
	3. **Log Moves**: Only the log moves, indicating that an event in the log does not correspond to any transition in the model at that moment.
	
	**Alignment Process**
	
	- Use algorithms to find the best possible alignment between the event log and the model.
	- The alignment aims to minimize the cost associated with mismatches, where each type of move (synchronous, model, log) is assigned a cost.
	
	**Practical Applications**
	
	- **Diagnosis**: Identify specific points of deviation for process improvement.
	- **Compliance**: Ensure that the actual process adheres to regulatory and internal standards.
	- **Optimization**: Enhance process efficiency by understanding and eliminating frequent deviations.


## Enrichment of Process Models

68. Types of process enhancement - Extensions and repair 
69. **Extend** - Add additional persepectives to the model using the event data 
70. **Repair** - Improving the quality of model using the event data 
71. Mining Decision Points - 
	- Input - *Event log* and *process Model* 
	- Assumption - Log and model have been aligned 
		- Mapping of activity names in log and model 
		- Every trace can be related to a path through the model

72. Decision points are places in the petri net where major event and decisions take place 
73. Places with multiple output arcs from decision points 
74. These form different types of decision tree problems for us to solve 
75. Case variables are variables that do not depend on a particular event and do not change over a lifetime of an object 
76. Predictor variable may also be based on the context of the process instance 
	- Number of *cases running* ( skip check if busy)
	- Number of *resources present* 
	- *Workload of resources* 
	- *Day* of the week 
	- *Weather* 

77. **Discovering the guards -** 
	- Taking output of a decision tree and *translating it into a data aware process model* 
	- Guards tell us what kind of path will the *decision tree take if we chose a particular path in the decision point* 
	- At any one point of time *the guards evaluate to true It cannot be that multiple guards evaluate to true* 
	- Data aware petri nets can also be *used for conformance checking* 

78. Bottlenecks - 
	- **Activity bottleneck** - These occurs when *specific activities or tasks within a process take longer than expected , causing delays* 
	- **Resource Bottleneck** - These arise when there are *insufficient resources are to handle the workload* 
	- **Handover bottlenecks** - Transition of task from one *department to another* 
	- **Decision point bottleneck** - These arise at points in the process *where decisions are made* . This decision making makes the process slow 

79. **Sociometry** - Present data on a n interpersonal relationship in graph or matrix form 
80. **Social Network Analysis** - 
	 - Arcs: Weights or inverted distance 
	 - Metrics to Denote the importance -
	   - Centrality 
	   - Closeness 
	   - Betweenness 

81. **Organisational Entity** - Resource Person , role , department 
82. **Degree Centrality** - Number of *connections a particular node has* 
83. **Closeness Centrality** - 1 Divided by the sum of all shortest pats to a particular node 
84. **Betweenness Centrality** - Fraction of shortest paths between any two nodes passing a particular node 
85. Sometimes we have **explicit role** or group information - 
    - Information system can provide such information (like an address book or directory)
    - It may also be recorded with the event itself 
    - Lets assume 3 roles - Assistant , Expert and Manager 

86. **Clustering** in process mining can be used for - 
    - *Grouping cases* (process variants)
    - *Grouping Resources* (identifying roles)

87. Starting with control flow perspective  - 
     1. Obtain an event log 
     2. Create or discover process model 
     3. Connect events in the log to activities in the model 
     4. Extend the model 
     5. add organisational perspective - time perspective - case perspectice - other 
     6. Return integrated model 
88. **Time perspective** - 
    - Replay evet log to compute waiting time and service times (distribution or just mean and variance)
    - Also capturing routing probabilities 

89. Resources are *discovered automatically* (clustering based on resource - activity matrix ) or obtain from information system 
90. **Cartography**: Process models as maps 
     - **Discover** - This activity is concerned with the extraction ( process ) models 
     - **Enhance** - When exisiting process models ( either discovered or hand made ) can be related to event logs it is possible to enhance ( extend and repair ) these models 
     - **Diagnose** - This does not directly use event logs and focuses on classical model based analysis 

91. **Auditing** : Confronting model and reality 
	 - **Detect** - Compares the models with correct pre mortem data . The moment a pre determined rule is violated , an alert is generated 
	 - **Check** - The goal of this activity is to pinpoint deviations and quantify the level of compliance 
	 - **Compare** - Defacto models can be compares with the models to see in what way reality deviates from what was planed or expected 
	 - **Promote** - Promote parts of the de facto model to a new model 

92. **Navigation**: Supporting and guiding process execution 
     - **Explore** - The combination of event data and models can be used to explore business processes at run time 
     - **Predict** - By combining information about running cases with models , it is possible to make predictions about the future . eg - remaining time flow and probability of success 
     - **Recommend** - The information used for predicting the future can also be used to recommend suitable actions 

## Operational Support and Conclusion

93. **Event Data is provided by** - 
    - Database systems like hospitals
    - A message log ( IBM Middleware )
    - Comma seperated values or spreadsheets 
    - An open API providing data from websites or social media 
    - Transaction Log ( Trading system )
    - Business Suite/ERP system like SAP Oracle 

94. **Conceptual model of XES Event log** 
     - Model Level - Process + Activity
     - Instance Level - Activity Instance -- Case -- Attribute 
     - Event Level - Event -- attribute 
     - Along with Timestamp -- resource -- costs -- transaction 

95. The challenge is not the **sytactical conversion** but 
	 - Locating the relevant data 
	 - Identifying process instances 
	 - Scoping 

96. The problem is SAP has a lot of tables ( 10 thousands of tables ) -- It becomes a challenge to identify the relevant table information 
97. In a hospital one can easily find one thousand patient related tables 
98. One of the biggest challenge one can face is the flattening of the event data 
99. In process mining, flattening of event logs refers to the transformation of the event log data into a more analysis-friendly format. This process involves *restructuring the log so that it can be easily processed* and interpreted by process mining algorithms and tools.
100. In their raw form, these logs are often in a nested or hierarchical structure, which can be challenging to analyze directly.

Example of Raw event log - 
```sql 
Case ID | Events
-----------------
1       | [Activity A at Time T1, Activity B at Time T2]
2       | [Activity A at Time T3, Activity C at Time T4, Activity B at Time T5]
```

Flattened Event log - 
```sql
Case ID | Activity  | Timestamp | Resource | Other Attributes
-------------------------------------------------------------
1       | Activity A| T1        | Resource1| Attr1
1       | Activity B| T2        | Resource2| Attr2
2       | Activity A| T3        | Resource1| Attr1
2       | Activity C| T4        | Resource3| Attr3
2       | Activity B| T5        | Resource2| Attr2
```


101. We have a lot of tables in the database and now we derrive out a lot of entities from the batch . We then decide which entity to get the process model about. 
102. **Data Quality problems -** 
	 - Missing Data ( Things are not recorded )
	 - Incorrect Data ( Things are recorded incorrectly )
	 - Imprecise data ( Things are not recorded at the desired level of granularity )
	 - Irrelevant Data ( things are submerged in poorly structured data )

103. **Problems while creating event logs -** 
![Problems](https://github.com/parthshr370/Process-Mining/blob/main/Pasted%20image%2020240629221001.png)

104. Events are things that happen and that are described by references and attributes 
105. References have a reference name and an identifier that refers to some object (Person, case , ticket , machine , room etc)
106. Attributes have a name and value ( eg Age = 48 , Time = 28-6-2014 )

## Guidelines for Logging 

107. **Reference and attribute names should have clear semantics**, ie they should have the same meaning for all people involved in creating and analysing event data. Diff stakeholders should interpret event data in the same way 
108. **There should be a structured and manages collection of references and attribute names ideally names** are grouped hierarchically (like taxonomy and ontology) a new reference and attribute name can only be added after there is consensus on its value and meaning 
109. **References should be stable** ( identifiers should not be reused or rely on the context ) for example , references should not be time region or language dependent . Some systems create different logs depending on the language settings . This is unnecessary complicating analysis 
110. **Attribute values should be as precise as possible** . If the value does not have the desired precision this should be indicated explicitly ( though a quantifier ) . For example , if for some events only the date is known but not the exact timestamp, this should be stated explicitly.\
111. **Uncertainty with respect to the occurrence of the event or its references or attributes should be captured** through appropriate qualifiers. For example , due to communication errors some values may be less reliable than usual note that uncertainty is diff from imprecision 
112. **Events should be at least partially ordered** . Ordering of events may be stored explicitly ( using a list )  or implicitly through an attribute denoting the events timestamp. If the recording of timestamps is unreliable or imprecise , there may still be ways to order events based on observed causalities( usage of data )
113. **If possible also store transactional information about the event** ( start , complete , abort , schedule ,assign ,  suspend , resume , withdraw ) . Having start and complete events allows for the computation of activity duration.
114. **Perform regularly automated consistency and correctness checks** to ensure the syntactical correctness of the event log. Check for missing references or attributes , and reference attribute names not agreed upon, Event quality assurance is continuous process( to avoid degradation of log quality )
115. **Ensure comparability of event logs over time and different groups of cases or process variants** . The logging itself should not change over time ( without being reported ) . For comparative process mining , its vital that the same logging principles are used.\
116. **Do not aggregate events in the event logs used as input for the analysis process**. Aggregation should be done during analysis and now before ( since it cannot be undone ) Event Data should be as raw as possible.
117. **Do not remove events and ensure provenance**. Reproduciblity is the key for process mining . For example do not remove a student from the database after he dropped out since this may lead to misleading analysis results . Also concerts are not deleted they are cancelled employees are not deleted, they are fired.
118. **Ensure privacy without losing meaningful correlation**. Sensitive or private data should be removed as early as possible . However if possible one should avoid removing correlations . Hashing can be a powerful tool in the trade off between privacy and analysis 

##  How to do a process Mining Project 

119. **Extract** - 
     - *Locate extract* and *transform event data* ( non trivial )
     - Morover, collect - Models and other artefacts , objectives KPI and questions 
     - Exploit existing domain knowledge 

120. Create **control flow model** and **connect event logs** - 
     - Control flow i the backbone of any process 
     - Therefore first create a suitable control flow model well connected to the available event data 
     - Conformance checking and alignment is the key 

121. **Create integrated process model** 
     - Replay event data on control flow model to learn about other perspective ( time resources or data )
     - Merge into an overall model showing the different perspective 


122. **Operational Support** - 
     - Use current (pre-mortem) data for on the fly deviation detection, prediction and recommendations
     - Only possible for lasagne processes 

123. In process mining, "**Lasagna processes**" refer to structured and predictable processes with a clear, hierarchical sequence of steps. These processes are characterized by their layered nature, similar to the layers in a lasagna dish
