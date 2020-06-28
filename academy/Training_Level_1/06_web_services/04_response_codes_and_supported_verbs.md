# Response Codes and Supported Verbs

After you have created your first  Web Service, let's understand in details, what  are the various reponse codes and their usage, as well as the Web Service various commands, options and examples:

[Response Codes](/articles/15_web_services/11_response_codes.md)

[Supported Verbs-GET](/articles/15_web_services/12_Supported_Verbs_Get.md)

[Supported Verbs-POST](/articles/15_web_services/13_Supported_Verbs_Post.md)

[Supported Verbs-PUT](/articles/15_web_services/14_Supported_Verbs_Put.md)

[Supported Verbs-DELETE](/articles/15_web_services/15_Supported_Verbs_Delete.md)

On top of the supported verbs and the response codes, the following addtional information could give you more insights on the URL structure, Authentication, Encoding, etc.:

[REST API Additions](/articles/15_web_services/16_rest_api_additions.md)

![](/academy/Training_Level_1/03_fabric_basic_LU/images/information.png)Here you can find some  code examples worth reviewing: [Web Services code examples](https://github.com/k2view-academy/K2View-Academy/blob/KB_DROP1_15_Web_Services_Merav/articles/15_web_services/06_web_services_code_examples.md)

### ![](/academy/Training_Level_1/03_fabric_basic_LU/images/Exercise.png) Exercise – Additional Web Service

1. `Create a new Web Service that insert entries into CASES table following considerations:`
   1. `The Web Service can insert multiple subscribers for a give Logical Unit Instance.`
   2. `The Web Service reposnse should include success or failure in the process`
   3. `Perform some basic input validations`
2. `Question: Which supported verbs will you use?`
3. `Question: What should be the input parameters and their data types?`
4. `Question: How will the Web Service be invoked if only the DELETE verb is allowed?`

### ![](/academy/Training_Level_1/03_fabric_basic_LU/images/Solution.png) Solution - Additional Web Service

1. ```java
   Map<String,String> result = new HashMap<>();
   String name ="";
   String message="";
   
   // Parse the input map to extract the values for the delete condition 
   
   //log.info(i_info.toString());
   if ( i_info != null && i_info.size() >0 ){
   	
   	for (int i = 0; i < i_info.size(); i++) {
   		
   		//Map<String,String> m = i_info.get.(i);
   		 if (i_info.get(i) != null){
   			 
   			String activity_id =i_info.get(i).get("activity_id");
   			String case_id =i_info.get(i).get("case_id");
   			String case_date =i_info.get(i).get("case_date");
   			String case_type =i_info.get(i).get("case_type");
   			String status =i_info.get(i).get("status");
   			
   		// Validate that input is not empty or wasn't exceed to number of object array
   			
   			    if (activity_id!=null && !activity_id.isEmpty()){
   						
   		// Insert into CASES table 	
   					fabric().execute("Begin");
   					String sql = "insert into cases (activity_id,case_id,case_date,case_type,status) values (?,?,?,?,?)";
   					ludb("CustomerLU", i_id).execute(sql,activity_id,case_id,case_date,case_type,status);
   					fabric().execute("Commit");
   				}
   			else{
   //Missing values to process 
   					i=i_info.size()+1;
   				    name="Error";
   				    message="MISSING VALUES"; 	
   				    //result.put(name, message);
   				   //return result;
   				}
   			
   			}
   	}
   	name="Complete";
   	message="INSERTED ALL";
   } else {
   
   // Input can not be processed, not data to parse
   	
    name="Not Started";
    message="NO INPUT RECIEVED";
   //message=Integer.toString(i_info.size());
}
   
result.put(name, message);
   return result;
   ```
   
   
   
2. `Answer : POST`

3. ```
   Answer: i_id : String ; i_info: List<Map<String,String>>
   
   Example request body :{
     "i_id": "1",
     "i_info": [
       {
         "activity_id":"437", 
         "case_id":"225",
         "case_date":"2015-08-02 08:33:06",
         case_type":"Network Issue",
         "status":"Open"
       
       }
  ]
   }
```
   
   
   
4. ```http
   Answer: Only by using a URL, DELETE does not support request or response body
   
   http://localhost:3213/api/v1.0/lu/CUSTOMERLU/1/CASES?WHERE=ACTIVITY_ID=437 AND CASE_ID=225&token=test 
   ```

   

 [![Previous](/articles/images/Previous.png)](/academy/Training_Level_1/06_web_services/03_Invoking_a_web_service.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](/academy/Training_Level_1/06_web_services/05_quiz.md)
