# Creating a New Translation in Fabric

A Translation is a Fabric Studio object that transforms data from one set of valid values to another in order to enable the execution of various transformation rules. Translation objects can be used as decision tables in Fabric and can be defined either on a Shared Objects level or on a Logical Unit level. 
* Translations defined on a Shared Objects level can be used in all objects included in a Project. 
* When a Translation is used for a Web Service it must be defined on a Shared Objects level.

How Can I Create a New Translation in Fabric?

1.	Go to the **Project Tree**, click **Logical Units**, **<LU Name>**, right click **Translations** and then select New Translation to display the Translation Schema tab.
2.	Define the **Translation Schema**:\
    a. Complete the **Name**, **Direction** (Input / Output), **type**, etc. of each field.\
    b. Select what happens if a Translation match is not found. By default, the action is **Use Default**.
3.	Go to the **Translation Data** tab.
4.	Optional: If the population data exists in a file or is retrieved from the DB, follow the instructions in How Can I Import Translation Data.
5.	To populate the data manually:\
    a. Enter the **Input value** combinations to generate the **Primary Key**. A Primary Key defines data transformation rules and is a combination of all Input fields. Therefore, each combination must be unique.\
    b. Enter the **Output value** combinations of each data Translation rule. The Output value does not need to be unique and can be repeated.\
    c. Optional: if a **Field Type = SQL**, validate the **query** using the **Query Builder**. To do so, click the **SQL** icon in the corner of the field and then click **Execute Query** in the **Query Builder** screen.
6.	Click **Save** to display the **New Item** dialog box.  
7.	Complete the **Name** field and then click **OK**. Note the following:
    a. A name must not include special characters like # or $.
    b. The recommended naming convention to use is the **trn** prefix. For example, **trnMarket**.

## Examples

### Example of a Simple Translation table

The following Translation includes a list of Input and Output combinations where Input has unique values and Output values are repeated.  For example, the Billing and Collection values of a LEGACY_ORD_TYPE Input field return the same Output value of BLG.

### Example of a Translation where Data Type = SQL

In the following Translation the **Field Type = SQL** whereby the query must be validated via the Query Builder.

To validate the query, click the **SQL** icon in the corner of the field and then click **Execute Query** in the **Query Builder** screen.

