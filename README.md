Welcome to S4H Tool Guide:

This guide teaches the user how to use S4H tools. Download and extract the project from the zip file and follow the steps carefully to execute them correctly.

HOW TO SUCCESSFULLY RUN YOUR CODE
Preliminary Step: DOWNLOAD ALL NECESSARY LIBRARIES

The user should download a project version (between memoryless and recall-based), extract the main folder and execute the project in a Python environment that supports some existing libraries used in it, such as NumPy, BinaryTree, etc. Download them if they are not already installed.

1.1: INPUT FILES

Firstly, to start, you will need two .txt files representing both the model and the NatATL formula. You can find both of them inside the TESTING folder as exampleModel(n).txt and exampleFormula(n).txt.

We strongly recommend you to begin with these files to understand the whole process, and then customize them as you desire.

To successfully run the entire project, you will need to modify the following paths:

model = ''C:\\Users\\utente\\Desktop\\s4h\\RecallNatATL\\Testing\\LogisticRobot.txt'
formula = ''C:\\Users\\utente\\Desktop\\s4h\\RecallNatATL\\Testing\\formulaNatATL.txt'
result = ''C:\\Users\\utente\\Desktop\\s4h\\RecallNatATL\\Testing\\Result.txt'
atlformula = 'C:\\Users\\utente\\Desktop\\s4h\\RecallNatATL\\Testing\\formulaATL.txt'

Representing respectively the input model, the formula intended in NatATL syntax, a result file where save the results obtained and write the synthetized winning strategy, and the corresponding atl formula for pre-processing phase.

These can be found inside the main.py file and must be replaced with the absolute paths of the files you download from the TESTING folder to your local computer.

Additionally, you have to modify the absolute path for the prunedModel file, which can be found at the beginning of the pruning.py file.

Note: These preliminary steps may seem a bit intricate but are fundamental for properly reading the input files, synthesizing the winning strategy, and working on a copy of the original model. Only exampleModel(n).txt and exampleFormula(n).txt need to be nonempty at the beginning; the other files can be empty!!

1.2: MAIN.PY

If you followed the instructions in section 1.1, you will be able to launch the program by running the main.py file. This file will call the handler NatATL function to manage the other phases.

HOW TO READ RESULTS
We provide a lot of visual outputs to help you understand the whole process, from the input formula to the formula tree building for our parsed formula (read the paper for theoretical background).

Here is an example of how a solution is outputted:

{'res': "Result: #STATESWHEREFORMULAHOLDS", 'initial_state': 'Initial state s0: True'} Solution found! Winning Strategy per agent: #WINNINGSTRATEGY Elapsed time is 0.0019927024841308594 seconds.

Note: The #'s will be replaced during execution by the actual output values.

Conversely, if the current formula cannot be satisfied by the model, the output will be:

We strongly advise against creating a scenario where no solution exists, especially for larger k values, as it will produce every single strategy for all agents involved. If this is the case, take a break, and let the computer work on it.

HOW TO MODIFY INPUT FILES
3.1: FORMULA ALTERATION

To modify a formula, follow the NatATL syntax rules. You can choose between X, G, F, and U temporal operators.

Here are some examples:

<{1}, 2>Xa <{1,3}, 4>Gh !<{1,2,3}, 3>aUb !(<{1,2,3}, 3>Gh && <{1,2,3}, 3>Gb)

Note: Here’s how the formula is structured: <{1}, 2>Xa -> {1} is the coalition, 2 is the complexity bound, and the term outside the angular brackets is your formula. The NOT operator is written using "!" for simplicity, so you can adopt this notation if you want (same goes for && as AND and || as OR).

3.2: MODEL ALTERATION

3.2.1: Memoryless Approach

To modify the model, if you want to add a state, you have to add a new row and a new column to the transition matrix (Transition), placing the idle element in the new diagonal position. Then you have to add an extra row to the label matrix (Labelling), and also add the new state name in the name_state position.

3.2.2: Recall Approach

Using models generator functions in testing directory.

3.3: TOTAL AGENTS ALTERATION

It is also possible (inside the exampleModel file) to define the total number of agents in the model. To add an agent, increase this number by one and add a unique set of actions for the new agent. These actions should also be reported in the Transition Matrix at the agent's new position. For example, if you add an extra agent and now have four agents in the coalition, it is mandatory to adjust all the matrix elements (apart from 0s) by adding a fourth character that matches one of the new agent's actions. For instance, the initial element ADF would become ADFZ.

Conversely, you can reduce the number of agents by subtracting from the total number of agents and removing the corresponding characters from the Transition Matrix that match the removed agent's actions.

3.4: ATOMIC PROPOSITION ALTERATION

To add a new atomic proposition, modify the atomic propositions row inside the exampleModel file. Additionally, add a new column to the Labelling Matrix, placing 1's in the states where you want the proposition to hold (for example, for the first row (s1), your column will have a 1) and 0 elsewhere.

On the other hand, you can reduce the number of atomic propositions by removing it from atomic_propositions and deleting its corresponding column in the Labelling Matrix.

3.5: OTHER CONSIDERATIONS

Some testing functions (such as randomizeFormula) have been left for the user to facilitate these adjustments.

3.5: OTHER CONSIDERATIONS

Some testing functions (such as randomizeFormula) have been left for the user to facilitate these adjustments.

For instance, to use randomizeFormula, go to the function initialize() inside the strategies.py file and look for the Testing commented section. Remember to modify the path, also adding your final destination for the formula that will be generated (this file can be empty at the beginning).

Logistic Robot real world model and formulas are included in their respective Memoryless and Recall-based Testing Directories.

Thanks!
