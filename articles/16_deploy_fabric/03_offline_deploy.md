# Offline Deploy

The implementation of a new Fabric project or an updated Fabric project must be deployed to the server side. A deployment can be performed either from the Fabric Studio <!--add link to 16.2 --> or from the Fabric Server, and is also known as an Offline Deploy. 

An Offline Deploy is implemented by running the **Deploy** command on the Fabric Server using artifacts that can be created either by the Fabric Studio or by the script on the server side.

### When Should I Use Offline Deploy?

When a Fabric Project is developed by a group of programmers it is important that the environment is always up-do-date. This can be challenging. Fabric provides a solution that enables combining the code changes that have been implemented and committed by several programmers and deploying them to a specific environment. To do so, the Development team should prepare an automated Jenkins process that takes the project's latest sources from the Git or SVN repository and copies them to the server. The process then runs the script that creates the artifacts based on this code and then deploys them on a server. This process can run on the Fabric Server without any dependency on the Fabric Studio. 

Click for more information about Best Practices for working with GIT and <!--add link to 9.7 Best Practices for working with GIT and SVN--> .

### How Do I Perform an Offline Deploy?

There are two ways to perform an Offline Deployment:

- Build and deploy in two steps. First build the artifacts either from the Fabric Studio or from the server using the **buildArtifacts.sh**<!--add link to sub-section here--> script . Then do the deployment by running the **Deploy** command on the server.

- Build and deploy in one step. Build and deploy from the server using the **buildAndDeployArtifacts.sh**<!--add link to sub-section here-->script . It is also possible to deploy without the build, whereby the script only runs a ** **Deploy**** command without creating and deleting artifacts.

##### Build and Deploy in Two Steps

1. To build the artifacts **from the Fabric Studio**:

   a. Right click the **object** (for example, **Web Services**) and click **Build Deploy Artifacts**.

   ![16_03_offline_deploy1](C:\K2View-Academy\articles\16_deploy_fabric\images\16_03_offline_deploy1.png)

   b. Once the artifacts are successfully built, right click the same object and select **Open Folder**. The Windows Explorer opens in the following location: [Your PC Folder]\K2View Fabric Studio\Projects\[Project Name]\Implementation\LogicalUnits\[LU Name]. Take the **ludb.JAR** and **ludbXMLs.ZIP** files and copy them to the server.

2. To build the artifacts **from the server**:

   a. Run the **buildArtifacts.sh** <!--add link to sub-section here--> script .

3. To do the deployment, run the **Deploy**** command using the following syntax <!--add link to sub-section here-->:

   DEPLOY <LUT> WITH JAR <'jar_path'> ZIP_FILE <'zip path'> [WS_METHODS <'string'>] NOSYNC <Boolean>.

   ###### Example:

   <!--TO ADD AN EXAMPLE-->

   Note that if the LUT parameter is populated by a **k2_ws** (Web Service LU Type), you can populate the WS_METHODS using the list of Web Services to be deployed. If this parameter is not populated or is empty, all the WS are deployed into the Fabric Server.

   ###### Example:

   <!--TO ADD AN EXAMPLE-->

   DEPLOY k2_ws WITH JAR '/home/k2view/AutoTests/Data/StudioProject/QA_AutoTests4/Implementation/LogicalUnits/k2_ws/ludb.jar' ZIP_FILE '/home/k2view/AutoTests/Data/StudioProject/QA_AutoTests4/Implementation/LogicalUnits/k2_ws/ludbXMLs.zip' WS_METHODS 'dbQueryOnAnyDB' NOSYNC true;

   ##### Build and Deploy in One Step

   To build the artifacts and the deployment together in one step from the server, run the buildAndDeployArtifacts.sh script  <!--add link to sub-section here-->.

   

   ##### Deployment Scripts Syntax and Options

   The following table describes the syntax and the mandatory/optional parameters for calling the deployment scripts. The scripts are located under /**usr/local/k2view/fabric/scripts** in the Fabric Server.

   <table style="width: 900px;">
<tbody>
   <tr>
<td style="width: 270px;">
   <p style="text-align: left;"><h4>
       <strong>buildArtifacts.sh</strong> for Linux or</p>
   <p><strong>buildArtifacts.bat</strong> for windows</p>
   </td>
   <td style="width: 630px;">
   <p><strong>Description</strong>: Build the artifact files.</p>
   <p><strong>Usage</strong>: ./buildArtifacts.sh&nbsp;[-h --help] -pd [PATH_TO_PROJECT] -l [LUTNAME] -d [OUTPUT DIRECTION]</p>
   <p><strong>Options</strong>:</p>
   <ul>
   <li>-h/--help displays the script usage.</li>
   <li>-pd [PROJ_NAME] - mandatory parameter. Sets the path to the project.</li>
   <li>-l [LUTNAME] &ndash; optional parameter. If not set, the artifacts are created for the entire project.</li>
   <li>-d [OUTPUT DIRECTION] &ndash; optional parameter. If not set, the artifacts are created in the given/each LU folder.</li>
   </ul>
   </td>
   </tr>
   <tr>
   <td style="width: 189px;"><h4>
   <p><strong>buildAndDeployArtifacts.sh</strong> for Linux or <strong>buildAndDeployArtifacts.bat</strong> for Windows</p>
   </td>
   <td style="width: 401px;">
   <p><strong>Description</strong>: Build and deploy the artifact files.</p>
   <p><strong>Usage</strong>: ./buildAndDeployArtifacts.sh -pd [PATH_TO_PROJECT] -s [NOSYNC] -l [LUT_NAME] -u [USER] -p [PASSWORD] -d [DEPLOYONLY]</p>
   <p><strong>Options</strong>:</p>
   <ul>
   <li>-h/--help - displays the script usage.</li>
   <li>-pd [PROJ_NAME] - mandatory parameter. Sets the path to the project.</li>
   <li>-s [NOSYNC] - optional parameter. If not set, the default is True.</li>
   <li>-l [LUTNAME] - optional parameter. If not set, the deploy runs for the entire project.</li>
   <li>-u [USER] - optional parameter. Default is <strong>admin</strong>.</li>
   <li>-p [PASSWORD] - optional parameter. Default is <strong>admin</strong>.</li>
   <li>-d [DEPLOYONLY] - optional parameter. If set to <strong>True</strong>, the script only runs a <strong>deploy</strong> command without creating and deleting the artifacts.</li>
   </ul>
   </td>
   </tr>
   </tbody>
   </table>
   
   ##### Deploy Command Syntax and Options
   
   The following table describes the syntax and the mandatory/optional parameters when invoking the **Deploy** command on the Fabric Server.
   
   <table width="900px">
   <tbody>
   <tr>
   <td width="270px">
   <p><strong>DEPLOY</strong></p>
   </td>
   <td width="630px">
   <p><strong>Usage</strong>: DEPLOY &lt;LUT&gt; WITH JAR &lt;'jar_path'&gt; ZIP_FILE &lt;'zip path'&gt; [WS_METHODS &lt;'string'&gt;] NOSYNC &lt;Boolean&gt;.</p>
   <p><strong>Options</strong>:</p>
   <ul>
   <li>LUT - Logical Unit type name.</li>
   <li>JAR - path to JAR file, relative to USER_DIR (JAR is a must).</li>
   <li>ZIP_FILE - path to ZIP file, relative to USER_DIR (ZIP is a must).</li>
   <li>NOSYNC - gets Boolean value:
   <ul>
   <li>NOSYNC TRUE: any deploy also without any changes triggers a sync the first time the instance is accessed.</li>
   <li>NOSYNC FALSE: only Schema updates trigger the sync after the deploy.</li>
   </ul>
   </li>
   <li>WS_METHODS - For LU Type = Web Services (k2_ws), specify which methods are selected, separated by &ldquo;,&rdquo;. Empty for all.</li>
   </ul>
   </td>
   </tr>
   </tbody>
   </table>
   <p>&nbsp;</p>
   <p>&nbsp;</p>

[![Previous](/articles/images/Previous.png)](/articles/16_deploy_fabric/02_deploy_from_Fabric_Studio.md)