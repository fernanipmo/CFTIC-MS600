# Exercise 1: Introduction to SharePoint Framework (SPFx)

## Task 1: Set up your SharePoint Framework development environment

### Ensure Node.js is installed and is the correct supported version



0. Installing Node.js.

   0.1 Downloading the actual version 14.17.6

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_01](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_01.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_02](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_02.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_03](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_03.png)

   

   0.2 Installing the node-v14.17.6-x64.msi package.

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_04](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_04.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_05](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_05.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_06](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_06.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_07](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_07.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_08](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_08.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_09](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_09.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_10](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_10.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_11](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_11.png)

   

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_12](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_12.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_13](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_13.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_14](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_14.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_15](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_15.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_16](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_16.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_17](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_17.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_18](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_18.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_19](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_19.png)

1. Open the PowerShell command prompt execute the following command: `node -v`

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_20](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_20.png)

2. Ensure the version is Node.js **v10.x** and is NOT 9.x nor 11.x (these two are not supported with the SharePoint Framework).

   

### Install Yeoman and gulp

1. From the command prompt execute the following command: `npm install -g yo gulp`

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_21](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_21.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_22](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_22.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_23](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_23.png)

1. From the command prompt execute the following command: `npm install -g @microsoft/generator-sharepoint`

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_24](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_24.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_25](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_25.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_26](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_26.png)

## Task 2: Creating a SharePoint Framework client-side web part

1. From the PowerShell command prompt, change to the C:/LabFiles directory by executing the following command: `cd c:/LabFiles`

1. Make a new directory for your SharePoint project files by executing the following command: `md SharePoint`

1. Navigate to the newly created SharePoint directory by executing the following command: `cd SharePoint`

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_27](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_27.png)

1. Make a new directory for your SharePoint project files by executing the following command: `md HelloWorld`

1. Navigate to the newly created SharePoint directory by executing the following command: `cd HelloWorld`

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_28](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_28.png)

1. Run the SharePoint Yeoman generator by executing the following command: `yo @microsoft/sharepoint`

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_29](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_29.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_30](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_30.png)

    

1. Use the following to complete the prompt that is displayed:

    - **What is your solution name?**: HelloWorld

    - **Which baseline packages do you want to target for your component(s)?**: SharePoint Online only (latest)

    - **Where do you want to place the files?**: Use the current folder

    - **Do you want to allow the tenant admin the choice of being able to deploy the solution to all sites immediately without running any feature deployment or adding apps in sites?**: No

    - **Will the components in the solution require permissions to access web APIs that are unique and not shared with other components in the tenant?**: No

    - **Which type of client-side component to create?**: WebPart

    - **What is your Web part name?**: HelloWorld

    - **What is your Web part description?**: HelloWorld description

    - **Which framework would you like to use?**: No JavaScript framework
    
      ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_31](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_31.png)
    
      ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_32](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_32.png)
    
      ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_33](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_33.png)
    
      ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_34](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_34.png)
    
      ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_35](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_35.png)

### Trusting the self-signed developer certificate

1. From the PowerShell command prompt execute the following command: `gulp trust-dev-cert`

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_36](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_36.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_37](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_37.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_38](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_38.png)

1. After provisioning the folders required for the project, the generator will install all the dependency packages using NPM for Node.js. When NPM completes downloading all dependencies, run the project by executing the following command: `gulp serve`

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_39](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_39.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_40](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_40.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_41](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_41.png)

   

1. The SharePoint Framework's gulp serve task will build the project, start a local web server, and launch a browser open to the SharePoint Workbench.

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_42](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_42.png)

   

1. Select the + web part icon button to open the list of available web parts.

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_43](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_43.png)

1. Select the **HelloWorld** web part.

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_44](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_44.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_45](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_45.png)

   

1. Edit the web part's properties by selecting the pencil (edit) icon in the toolbar to the left of the web part.

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_46](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_46.png)

1. In the property pane that opens, change the value of the **Description** field. Notice how the web part updates as you make changes to the text.

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_47](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_47.png)

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_48](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_48.png)

1. Go back to PowerShell and stop the running process by executing **Ctrl + C**

   ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_49](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_49.png)

1. When prompted to terminate type Y and hit the enter key.

## Task 3: Test with the local and hosted SharePoint Workbench

In this exercise you will work with two different versions of the SharePoint Workbench, the local and hosted workbench, as well as the different modes of the built-in gulp serve task.

1. Open the project in Visual Studio Code by executing the following command: `code .`

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_50](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_50.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_51](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_51.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_52](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_52.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_53](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_53.png)

    

1. From the Visual Studio Code ribbon, select **Terminal > New Terminal**.

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_54](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_54.png)

    

1. Run the project by executing the following command: `gulp serve`

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_55](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_55.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_56](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_56.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_57](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_57.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_58](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_58.png)

1. Select the + web part icon button to open the list of available web parts.

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_59](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_59.png)

1. Select the **HelloWorld** web part.

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_60](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_60.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_61](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_61.png)

1. Leave the project running. Go back to Visual Studio Code.

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_62](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_62.png)

1. Edit the HTML in the web part's **render()** method, located in the **src/webparts/helloWorld/HelloWorldWebPart.ts** file.

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_63](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_63.png)

    1. Locate the style with the class styles.title and update change the title to “**Welcome to Microsoft Learning for SharePoint!**”

       ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_63](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_63.png)

    1. Save the project and then navigate back to the browser and notice your web part title value changes.

       ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_64](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_64.png)

1. Next, in the browser navigate to one of your SharePoint Online sites and append the following to the end of the root site's URL: **/_layouts/workbench.aspx**. This is the SharePoint Online hosted workbench.

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_65](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_65.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_66](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_66.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_67](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_67.png)

    

1. Notice that when you add a web part, many more web parts will appear beyond the one you created; and was the only one showing in the toolbox on the local workbench. This is because you are now testing the web part in a working SharePoint site.

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_68](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_68.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_69](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_69.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_70](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_70.png)

    **Note**:
    The difference between the local and hosted workbench is significant. Consider that a local workbench is not a working version of SharePoint; rather, it's just a single page that can let you test web parts. This means you won't have access to a real SharePoint context, lists, libraries, or real users when you are testing in the local workbench.

1. Let's see another difference with the local versus hosted workbench. Go back to the web part and make a change to the HTML.

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_71](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_71.png)

    ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_72](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_72.png)

    

1. Notice that, after saving the file, while the console displays a lot of commands, the browser that is displaying the hosted workbench does not automatically reload. This is expected. You can still refresh the page to see the updated web part, but the local web server cannot cause the hosted workbench to refresh. Close both the local and hosted workbench and stop the local web server by pressing CTRL+C in the command prompt.

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_74](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_74.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_75](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_75.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_76](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_76.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_77](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_77.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_78](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_78.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_79](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_79.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_80](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_80.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_81](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_81.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_82](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_82.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_83](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_83.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_84](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_84.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_85](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_85.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_86](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_86.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_87](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_87.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_88](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_88.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_89](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_89.png)

     ![02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_90](Evidencia/02-Exercise-1-Introduction-to-SharePoint-Framework-(SPFx)_90.png)

## Review

In this exercise, you learned how to create a SharePoint Framework web part and test the web part using the SharePoint Framework Workbench and SharePoint site.



[Readme.md](https://github.com/fernanipmo/CFTIC-MS600#readme)

