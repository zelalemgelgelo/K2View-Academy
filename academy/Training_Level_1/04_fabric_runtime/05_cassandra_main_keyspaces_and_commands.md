# Cassandra Main Keyspaces & Commands

### ![](/academy/Training_Level_1/04_fabric_runtime/images/fabric_execute_04.png)

Now that you are able to retrieve and view the data in Fabric, let's understand how the data is being stored in Cassandra, what is the operational information that you can view and what are the commands to access it:

[Cassandra Keyspaces for Fabric](/articles/02_fabric_architecture/06_cassandra_keyspaces_for_fabric.md)

[Cassandra Basic Commands](/articles/02_fabric_architecture/07_cassandra_basic_commands.md)

### ![](/academy/Training_Level_1/03_fabric_basic_LU/images/example.png)Example- Keyspaces & Commands

 Let's view the our Project keyspaces and Product keyspaces:

1. Run **describe keyspaces;** and let's view the Product and Project keyspaces
2. Let's change our current keyspace to the CustomerLU  keyspace, by executing  **use k2view_customerlu;**
3. Let's review the entities in **k2view_customerlu.entity** using the following statement : **select * from k2view_customerlu.entity**;

### ![](/academy/Training_Level_1/03_fabric_basic_LU/images/Exercise.png)Exercise – Keyspaces & Commands

1. `Question: What are the instance Ids that stored in k2view_customerlu?` `How will you list them?`
2. `Question: How will you list the LUTs which were deployed?`

### ![](/academy/Training_Level_1/03_fabric_basic_LU/images/Solution.png)Solution - Keyspaces & Commands

1. `Answer:215, 82;` 

   `cassandra@cqlsh> select id from k2view_customerlu.entity ;`

   

2. `Answer: select lut_name, lut_version, lut_index_status from k2system.k2_lut_info;``or by k2view_* keyspaces being created`



 [![Previous](/articles/images/Previous.png)](/academy/Training_Level_1/04_fabric_runtime/04_fabric_commands.md)