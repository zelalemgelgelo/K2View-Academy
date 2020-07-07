# Broadway Flow Overview

**Broadway Flow** is a main Broadway object which represents a business process. A flow acts as a graph (or tree) which is built out of several [Stages]() and each Stage includes one or more [Actor](/articles/99_Broadway/03_broadway_actor.md). The Stages are executed one by one from left to right, while the Actors within each Stage of the flow are executed top down. 

### Simple Flow
Below is a simple flow with 3 stages and 4 actors. The execution order of the Actors within the flow is: **A1 -> B1 -> B2 -> C1**.

![image](/articles/99_Broadway/images/99_16_01_flow1.PNG)

### Flow with 2 Stages on the Same Level
Each Stage can be split into two stages (and so on), so there can be several stages on the same dependency level in the flow and their execution order is also top down. In the below example, the execution order is still the same and it is: **A1 -> B1 -> B2 -> C1**.

![image](/articles/99_Broadway/images/99_16_01_flow2.PNG)

### Flow with Condition
When it's needed to introduce a condition in the flow, such as IF-ELSE, the flow can be split and a stage condition can be added to one of the split parts, while the other part can be set as ELSE. The execution order of the Actors in such flow will be: **A1 -> B1 if true, otherwise B2 -> C1**. Note that Stage condition is a grey object, while a regular Actor is yellow.

![image](/articles/99_Broadway/images/99_16_01_flow3.PNG)

If there are additional Stages on the same dependency level as IF-ELSE condition, thier Actors will be executed as well, in the following execution order: **A1 -> B1 if true, otherwise B2 -> Now1 -> C1**.

![image](/articles/99_Broadway/images/99_16_01_flow4.PNG)


