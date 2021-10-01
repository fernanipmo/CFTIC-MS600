﻿# Exercise 7: Deploying SPFx solutions to Microsoft Teams

## Task 1: Create your project

1. From the PowerShell command prompt, change to the C:/LabFiles/SharePoint directory by executing the following command: `cd c:/LabFiles/SharePoint`

1. Make a new directory for your SharePoint project files by executing the following command: `md SPFxTeamsTab`

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_01](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_01.png)

1. Navigate to the newly created SharePoint directory by executing the following command: `cd SPFxTeamsTab`

1. Run the SharePoint Yeoman generator by executing the following command: `yo @microsoft/sharepoint`

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_02](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_02.png)

1. Use the following to complete the prompt that is displayed:

    - **What is your solution name?**: SPFxTeamsTab

    - **Which baseline packages do you want to target for your component(s)?:** SharePoint Online only (latest)

    - **Where do you want to place the files?**: Use the current folder

    - **Do you want to allow the tenant admin the choice of being able to deploy the solution to all sites immediately without running any feature deployment or adding apps in sites?**: Yes

    - **Will the components in the solution require permissions to access web APIs that are unique and not shared with other components in the tenant?**: No

    - **Which type of client-side component to create?**: WebPart

    - **What is your Web Part name?**: SPFx Teams Together

    - **What is your Web Part description?**: SPFx Teams Together description

    - **Which framework would you like to use?**: No JavaScript framework

      ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_03](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_03.png)

      ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_04](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_04.png)

      ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_05](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_05.png)

      

1. After provisioning the folders required for the project, the generator will install all the dependency packages using NPM.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_06](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_06.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_07](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_07.png)

1. Open the project in an editor such as Visual Studio Code.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_08](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_08.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_09](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_09.png)

1. Enable the web part to be used in Microsoft Teams:

    1. Locate and open the file **./src/webparts/spFxTeamsTogether/SpFxTeamsTogetherWebPart.manifest.json**.

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_10](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_10.png)

    1. Within the web part manifest file, locate the property **supportedHosts**: `"supportedHosts": ["SharePointWebPart"],`
    
    1. Add another option to enable this web part to be used as a tab in a Microsoft Teams team: `"supportedHosts": ["SharePointWebPart", "TeamsTab"],`
    
       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_11](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_11.png)

## Task 2: Creating and deploying the Microsoft Teams app package

Notice the project contains a folder **teams** that contains two images. These are used in Microsoft Teams to display the custom tab.

You may notice there is no **manifest.json** file present. The manifest file can be generated automatically by SharePoint from the App Catalog site. However, at this time, this functionality is not fully operational.

Alternatively, you can manually create the manifest file if you want to have more control over the default values that SharePoint will create.

The automatic generation and deployment of the Microsoft Teams manifest is not currently operational; you will manually create the Microsoft Teams manifest and app package:

1. Create a **manifest.json** file in **./teams** folder, use the following manifest file as a template:
    ```json
    {
        "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
        "manifestVersion": "1.5",
        "packageName": "{{SPFX_COMPONENT_ALIAS}}",
        "id": "{{SPFX_COMPONENT_ID}}",
        "version": "0.1",
        "developer": {
            "name": "Parker Porcupine",
            "websiteUrl": "https://contoso.com",
            "privacyUrl": "https://contoso.com/privacystatement",
            "termsOfUseUrl": "https://contoso.com/servicesagreement"
        },
        "name": {
            "short": "{{SPFX_COMPONENT_NAME}}"
        },
        "description": {
            "short": "{{SPFX_COMPONENT_SHORT_DESCRIPTION}}",
            "full": "{{SPFX_COMPONENT_LONG_DESCRIPTION}}"
        },
        "icons": {
            "outline": "{{SPFX_COMPONENT_ID}}_outline.png",
            "color": "{{SPFX_COMPONENT_ID}}_color.png"
        },
        "accentColor": "#004578",
        "staticTabs": [
            {
            "entityId": "com.contoso.personaltab.spfx",
            "name": "My SPFx Personal Tab",
            "contentUrl": "https://{teamSiteDomain}/_layouts/15/TeamsLogon.aspx?SPFX=true&dest=/_layouts/15/teamshostedapp.aspx%3Fteams%26personal%26componentId={{SPFX_COMPONENT_ID}}%26forceLocale={locale}",
            "scopes": [
                "personal"
            ]
            }
        ],
        "configurableTabs": [
            {
            "configurationUrl": "https://{teamSiteDomain}{teamSitePath}/_layouts/15/TeamsLogon.aspx?SPFX=true&dest={teamSitePath}/_layouts/15/teamshostedapp.aspx%3FopenPropertyPane=true%26teams%26componentId={{SPFX_COMPONENT_ID}}%26forceLocale={locale}",
            "canUpdateConfiguration": true,
            "scopes": [
                "team"
            ]
            }
        ],
        "validDomains": [
            "*.login.microsoftonline.com",
            "*.sharepoint.com",
            "spoprod-a.akamaihd.net",
            "resourceseng.blob.core.windows.net"
        ],
        "webApplicationInfo": {
            "resource": "https://{teamSiteDomain}",
            "id": "00000003-0000-0ff1-ce00-000000000000"
        }
    }
    ```

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_12](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_12.png)
    
    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_13](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_13.png)
    
    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_14](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_14.png)
    
1. Open the **manifest.json** file. This file contains multiple strings that need to be updated to match the SPFx component. Use the following table to determine the values that should be replaced. The SPFx component properties are found in the web part manifest file: **./src/webparts/spFxTeamsTogether/SpFxTeamsTogetherWebPart.manifest.json**

    | **manifest.json string**| **Property in SPFx component manifest**|
    | :--- | :--- |
    | {{SPFX_COMPONENT_ALIAS}}| alias|
    | {{SPFX_COMPONENT_NAME}}| preconfiguredEntries[0].title|
    | {{SPFX_COMPONENT_SHORT_DESCRIPTION}}| preconfiguredEntries[0].description|
    | {{SPFX_COMPONENT_LONG_DESCRIPTION}}| preconfiguredEntries[0].description|
    | {{SPFX_COMPONENT_ID}}| id|

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_15](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_15.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_16](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_16.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_17](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_17.png)

    **Note**:
    Don't miss replacing **{{SPFX_COMPONENT_ID}}** in **configurableTabs[0].configurationUrl**. You will likely have to scroll your editor to the right to see it. The tokens surrounded by single curly braces (for example, **{teamSiteDomain}**) do not need to be replaced.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_18](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_18.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_20](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_20.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_21](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_21.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_22](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_22.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_23](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_23.png)

1. Create a Microsoft Teams app package by zipping the contents of the **./teams** folder. Make sure to zip just the contents and not the folder itself. This ZIP archive should contain three files at the root: two images and the **manifest.json**.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_24](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_24.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_25](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_25.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_25a](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_25a.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_25b](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_25b.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_25c](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_25c.png)

## Task 3: Create and deploy the SharePoint package

In order to test the web part in SharePoint and Microsoft Teams, it must first be deployed to an app catalog.

1. Open a browser and navigate to your SharePoint Online Tenant-Scoped App Catalog site.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_26](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_26.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_26a](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_26a.png)

   

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_27](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_27.png)

   

1. Select the menu item **Apps for SharePoint** from the left navigation menu.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_28](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_28.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_29](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_29.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_31](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_31.png)

   

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_33](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_33.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_34](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_34.png)

1. Build the project by opening a command prompt and changing to the root folder of the project. Then execute the following command: `gulp build`

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_35](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_35.png)

1. Next, create a production bundle of the project by running the following command on the command line from the root of the project: `gulp bundle --ship`

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_36](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_36.png)

1. Create a deployment package of the project by running the following command on the command line from the root of the project: `gulp package-solution --ship`

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_37](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_37.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_38](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_38.png)

   

1. Locate the file created by the gulp task, found in the **./sharepoint/solution** folder with the name *.sppkg.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_39](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_39.png)

1. Drag this file into **the Apps for SharePoint** library in the browser.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_40](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_40.png)

   

1. In the **Do you trust...?** dialog box, select the check box **Make this solution available to all sites in the organization** and then select **Deploy**.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_41](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_41.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_42](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_42.png)

1. This will make the SPFx web part available to all site collections in the tenant, including those that are behind a Microsoft Teams team.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_43](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_43.png)

## Task 4: Test the web part in SharePoint and Microsoft Teams

Test the SPFx web part in SharePoint:

1. In the browser, navigate to a modern SharePoint page.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_44](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_44.png)

1. Select the **Edit** button in the upper-right portion of the page.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_45](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_45.png)

1. Select the **(+)** icon to open the SharePoint web part toolbox and locate the web part SPFx Teams Together:

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_46](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_46.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_47](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_47.png)

   

1. The SharePoint Framework web part will be displayed on the page.

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_48](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_48.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_49](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_49.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_50](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_50.png)

   ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_51](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_51.png)

   

   

## Task 5: Testing the SPFx web part in Microsoft Teams

1. Create a new Microsoft Teams team.

    1. Using the same browser where you are signed in to SharePoint Online, navigate to [https://teams.microsoft.com](https://teams.microsoft.com/). When prompted, load the web client.

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_52](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_52.png)

    1. If you do not have any teams in your tenant, you will be presented with the following dialog. Otherwise, select **Join or create a team** at the bottom of the list of teams.

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_53](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_53.png)

    1. On the **Create your team** dialog box, select **Build a team from scratch**.

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_54](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_54.png)

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_55](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_55.png)

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_56](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_56.png)

    1. On the **What kind of team will this be?** dialog box, select **Public**.

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_57](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_57.png)

    1. When prompted, use the name **My First Team**.

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_58](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_58.png)

       ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_59](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_59.png)

1. Install the Microsoft Teams application as a new tab that will expose the SharePoint Framework web part in Microsoft Teams:

    1. Select the **My First Team** team previously created.
    1. Select the **General** channel.

1. Add a custom tab to the team using the SPFx web part:

    1. At the top of the page, select the **+** icon in the horizontal navigation.

        ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_60](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_60.png)

    1. In the **Add a tab** dialog box, select **More Apps**.

        ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_62](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_62.png)

    1. Select the **Upload a custom app** > **Upload for ...** from the list of app categories.

        ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_63](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_63.png)

    1. Select the Microsoft Teams application ZIP file previously created. This is the file that contains the **manifest.json** and two image files.

        ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_64](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_64.png)
        
        **Note**:
        After a moment, the application will appear next to your tenant name. You may need to refresh the page for the app to appear if you are using the browser Microsoft Teams client.
        
        ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_65](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_65.png)

1. Select the **SPFx Teams Together** app.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_66](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_66.png)

1. In the **SPFx Teams Together** dialog box, select the **My First Team** in the **Add to a team** drop-down control and select **Install**.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_67](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_67.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_68](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_68.png)

1. In the **SPFx Teams Together is now available for My First Team** dialog box, select the **General** channel and select **Set up**.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_69](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_69.png)

1. The next dialog box will confirm the installation of the app. Select **Save**.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_70](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_70.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_71](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_71.png)

1. The application should now load in Microsoft Teams within the **General** channel under the tab **SPFx Teams Together**.

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_72](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_72.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_73](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_73.png)

    ![08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_74](Evidencia/08-Exercise-7-Deploying-SPFx-solutions-to-Microsoft-Teams_74.png)

## Review

In this exercise, you learned how to create a SharePoint Framework (SPFx) solution that will work in both SharePoint and as a tab in Microsoft Teams.

