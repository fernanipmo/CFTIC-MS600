# Exercise 1: Collecting user input with task modules

In this exercise, you'll learn the basics of task modules in Microsoft Teams and how to collect input from users in a custom task module. After creating a new Microsoft Teams personal tab, you'll add two task modules to it.

One is a standard HTML page that accepts the ID of a video on YouTube. When the task module is invoked, it will display the video using the YouTube embedded player. This task module will get the video ID from the query string, but it will not need to return any information back to the tab.

The other task module is implemented using React, the same way custom tabs are implemented using the Yeoman Generator for Microsoft Teams. This task module enables the user to specify the ID of the YouTube video to display. Once changed, when the user saves their changes, it will use the callback to close submit the new ID back to the tab.

## **Previous Tasks**

![02-Exercise-1-Collecting-user-input-with-task-modules_03a](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_03a.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_09](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_09.png)



![02-Exercise-1-Collecting-user-input-with-task-modules_01](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_01.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_02](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_02.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_04](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_04.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_05](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_05.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_06](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_06.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_07](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_07.png)




## Task 1: Create Microsoft Teams app

1. Open your command prompt, navigate to a directory where you want to save your work, create a new folder **learn-msteams-taskmodules**, and change directory into that folder.

1. Run the Yeoman Generator for Microsoft Teams by running the following command:

    ```console
    yo teams
    ```

    

1. Yeoman will launch and ask you a series of questions. Answer the questions with the following values:

    - **What is your solution name?**: YouTubePlayer
    
    - **Where do you want to place the files?**: Use the current folder
    
    - **Title of your Microsoft Teams App project?**: YouTube Player
    
    - **Your (company) name? (max 32 characters)**: Contoso
    
    - **Which manifest version would you like to use?**: v1.8
    
    - **Quick scaffolding**: Yes
    
    - **What features do you want to add to your project?**: A Tab
    
    - **The URL where you will host this solution?**: (Accept the default option)

    - **Would you like to show a loading indicator when your app/tab loads?** No
    
    - **Default Tab name? (max 16 characters)**: YouTube Player 1
    
    - **What kind of Tab would you like to create?**: Personal (static)
    
    - **Do you require Azure AD Single-Sign-On support for the tab?** No
    
      ![02-Exercise-1-Collecting-user-input-with-task-modules_08](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_08.png)
    
      ![02-Exercise-1-Collecting-user-input-with-task-modules_11](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_11.png)
    
    > [!NOTE]
    > Most of the answers to these questions can be changed after creating the project. For example, the URL where the project will be hosted isn't important at the time of creating or testing the project.
    
    After answering the generator's questions, the generator will create the scaffolding for the project and then execute `npm install` that downloads all the dependencies required by the project.
    
    ![02-Exercise-1-Collecting-user-input-with-task-modules_12](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_12.png)

### Test the personal tab

1. Before customizing the tab, let's test the tab to see the initial developer experience for testing.

1. From the command line, navigate to the root folder for the project and execute the following command:

    ```console
    gulp ngrok-serve
    ```

    This gulp task will run many other tasks all displayed within the command-line console. The **ngrok-serve** task builds your project and starts a local web server (http://localhost:3007). It then starts ngrok with a random subdomain that creates a secure URL to your local webserver.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_13](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_13.png)

    > [!NOTE]
    > Microsoft Teams requires all content displayed within a tab be loaded from an HTTPS request. In development, can be done using the tool [ngrok](https://www.ngrok.com) that creates a secure rotatable URL to your local HTTP webserver. Ngrok is included as a dependency within the project so there is nothing to setup or configure.

    > [!IMPORTANT]
    > Each time ngrok is started, it will generate a new dynamic subdomain for the URL. If you have to restart ngrok, you will need to repackage and and update the app in Microsoft Teams to make the installed app aware of the new URL. The optional licensed version of ngrok allows you to define and reuse the same subdomain.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_14](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_14.png)

1. Open a browser and navigate to the ngrok URL displayed in the console:

    ![02-Exercise-1-Collecting-user-input-with-task-modules_15](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_15.png)

1. Update the URL in the browser to load the tab created by the scaffolding process. Here you can see the page can determine that it isn't running within the Microsoft Teams client.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_16](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_16.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_17](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_17.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_18](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_18.png)

1. Now let's load the tab in Microsoft Teams. In the browser, navigate to **https://teams.microsoft.com** and sign in with the credentials of a Work and School account.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_19](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_19.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_20](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_20.png)

    > [!NOTE]
    > Microsoft Teams is available for use as a web client, desktop client and a mobile client. In this module, we will use the web client but any of the clients can be used.

1. Using the app bar navigation menu, select the **More added apps** button. Then select **More apps**.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_21](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_21.png)

1. On the **Browse available apps and services** page, select **Upload a custom app** > **Upload for me or my teams**.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_22](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_22.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_23](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_23.png)

1. In the file dialog that appears, select the Microsoft Teams package in your project. This app package is a ZIP file that can be found in the project's **./package** folder.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_24](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_24.png)

1. Once the package is uploaded, Microsoft Teams will display a summary of the app. Here you can see some "todo" items to address. *None of these "todo" items are important to this exercise, so you will leave them as is.*

1. Select the **Add** button to install the app, adding a new personal tab to your **More added apps** dialog:

    ![02-Exercise-1-Collecting-user-input-with-task-modules_25](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_25.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_26](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_26.png)

1. Select the app to navigate to the new tab:

     ![02-Exercise-1-Collecting-user-input-with-task-modules_27](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_27.png)

     ![02-Exercise-1-Collecting-user-input-with-task-modules_28](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_28.png)

     ![02-Exercise-1-Collecting-user-input-with-task-modules_29](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_29.png)

     Notice that when the content page is loaded in a tab within the Microsoft Teams client, it's displaying the value of the `entityId` property of the tab, not the message "This isn't hosted in Microsoft Teams" as you saw when viewing the content page in the browser. The tab can detect if it's loaded within the Microsoft Teams client using the Microsoft Teams JavaScript SDK.

     The next step is to make some changes to the project.

1. Next, stop the local web server by pressing <kbd>CTRL</kbd>+<kbd>C</kbd> in the console to stop the running process.

     ![02-Exercise-1-Collecting-user-input-with-task-modules_30](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_30.png)

### Implement the personal tab's user interface

Now you can implement the user interface for the tab. The simple tab will have a basic interface.

1. Locate and open the file that contains the React component used in the project: **./src/client/youTubePlayer1Tab/YouTubePlayer1Tab.tsx**.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_31](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_31.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_32](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_32.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_33](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_33.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_34](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_34.png)

    

1. Update the `import` statements in this file to add components from the Fluent UI - React library. Find the following `import` statement at the top of the file that imports components from the Fluent UI - React library:

    ```typescript
    import { Provider, Flex, Text, Button, Header } from "@fluentui/react-northstar";
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_35](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_35.png)

    Replace the previous statement with the following `import` statement:

    ```typescript
    import { Provider, Flex, Text, Button, Header, Input } from "@fluentui/react-northstar";
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_36](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_36.png)

1. Update the state of the component to contain a video ID. Add the following statement after the existing `useState` statements in the **YouTubePlayer1Tab.tsx** file:

    ```typescript
    const [youTubeVideoId, setYouTubeVideoId] = useState<string | undefined>("VlEH4vtaxp4");
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_37](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_37.png)

1. Add the following methods to the `YouTubePlayer1Tab` class. These methods will handle updating the state when specific events happen on the form you'll add to the component:

    ```typescript
    const onShowVideo = (): void => {
    };
    
    const onChangeVideo = (): void => {
    };
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_38](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_38.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_39](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_39.png)

1. Locate the `return` statement and update to the following code. The component will now display state with a brief copyright statement:

    ```tsx
    return (
      <Provider theme={theme}>
        <Flex fill={true} column styles={{
          padding: ".8rem 0 .8rem .5rem"
        }}>
          <Flex.Item>
            <Header>Task Module Demo</Header>
          </Flex.Item>
          <Flex.Item>
            <div>
              <div>
                <Text>YouTube Video ID:</Text>
                <Input value={youTubeVideoId} disabled></Input>
              </div>
              <div>
                <Button content="Change Video ID" onClick={() => onChangeVideo()}></Button>
                <Button content="Show Video" primary onClick={() => onShowVideo()}></Button>
              </div>
            </div>
          </Flex.Item>
          <Flex.Item styles={{
            padding: ".8rem 0 .8rem .5rem"
          }}>
            <Text content="(C) Copyright Contoso" size="smaller"></Text>
          </Flex.Item>
        </Flex>
      </Provider>
    );
    ```

![02-Exercise-1-Collecting-user-input-with-task-modules_40](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_40.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_41](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_41.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_42](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_42.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_43](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_43.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_44](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_44.png)

The next step is to add some interactivity to the tab.

### Test the personal tab

At this point, our Microsoft Teams app, implemented as a custom person tab is set up and working. Verify this by starting ngrok again and refreshing the Microsoft Teams interface.

1. Increment the `version` property in the app's **./manifest/manifest.json** file so you can update the previously deployed Teams app.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_45](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_45.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_46](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_46.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_47](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_47.png)

1. From the command line, navigate to the root folder for the project and execute the following command:

    ```console
    gulp ngrok-serve
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_48](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_48.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_50](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_50.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_49](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_49.png)

1. Upgrade the previously deployed Teams app with the updated app package.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_51](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_51.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_52](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_52.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_53](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_53.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_54](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_54.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_55](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_55.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_56](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_56.png)

    

1. In the browser, navigate back to the tab and notice the new UI you've implemented for the tab:

    ![02-Exercise-1-Collecting-user-input-with-task-modules_57](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_57.png)

    Now you can update the project and add task modules to the custom Microsoft Teams app.

1. Stop the local web server by pressing <kbd>CTRL</kbd>+<kbd>C</kbd> in the console to stop the running process.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_58](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_58.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_59](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_59.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_60](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_60.png)

## Task 2: Add video player task module

1. A task module can be a web page implemented with HTML and JavaScript. Create the video player task module by creating a new file, **player.html** in the **./src/public/youTubePlayer1Tab** folder in your project.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_61](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_61.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_62](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_62.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_63](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_63.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_64](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_64.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_65](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_65.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_66](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_66.png)

    

1. Add the following HTML to the **player.html** file:

    ```html
    <!DOCTYPE html>
    <html lang="en">
    
    <head>
      <title>YouTube Player Task Module</title>
      <style>
        #embed-container iframe {
          position: absolute;
          top: 0;
          left: 0;
          width: 95%;
          height: 95%;
          padding-left: 20px;
          padding-right: 20px;
          padding-top: 10px;
          padding-bottom: 10px;
          border-style: none;
        }
      </style>
    </head>
    
    <body>
      <div id="embed-container"></div>
    </body>
    
    </html>
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_67](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_67.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_68](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_68.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_69](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_69.png)

    The video player task module will use the YouTube embedded player to show the specified video. The video will be defined in the query string when the **player.html** file is loaded.

1. Implement the `<iframe>` embedded video player by adding the following JavaScript before the closing `</body>` tag in the **player.html** file:

    ```html
    <script>
      function getUrlParameter(name) {
        name = name.replace(/[\[]/, '\\[').replace(/[\]]/, '\\]');
        var regex = new RegExp('[\\?&]' + name + '=([^&#]*)');
        var results = regex.exec(location.search);
        return results === null ? '' : decodeURIComponent(results[1].replace(/\+/g, ' '));
      };
    
      var element = document.createElement("iframe");
      element.src = "https://www.youtube.com/embed/" + getUrlParameter("vid");
      element.width = "1000";
      element.height = "700";
      element.frameborder = "0";
      element.allow = "autoplay; encrypted-media";
      element.allowfullscreen = "";
    
      document.getElementById("embed-container").appendChild(element);
    </script>
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_70](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_70.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_71](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_71.png)

    Now, implement the task module in the personal tab.

1. Locate and open the **./src/client/youTubePlayer1Tab/YouTubePlayer1Tab.tsx** file.

    

1. First, add the following utility method to the `YouTubePlayer1Tab` component:

    ```typescript
    const appRoot = (): string => {
      if (typeof window === "undefined") {
        return "https://{{HOSTNAME}}";
      } else {
        return window.location.protocol + "//" + window.location.host;
      }
    }
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_72](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_72.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_73](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_73.png)

1. Next, add the following code to the `onShowVideo()` method:

    ```typescript
    const onShowVideo = (): void => {
      const taskModuleInfo = {
        title: "YouTube Player",
        url: appRoot() + `/youTubePlayer1Tab/player.html?vid=${youTubeVideoId}`,
        width: 1000,
        height: 700
      };
      microsoftTeams.tasks.startTask(taskModuleInfo);
    }
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_74](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_74.png)
    
    This code will create a new `taskInfo` object with the details of the task module. It will then launch the task module. This task module does nothing but display information, so we don't need to implement the callback.

### Test the video player task module

1. Increment the `version` property in the app's **./manifest/manifest.json** file so you can update the previously deployed Teams app.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_75](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_75.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_76](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_76.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_77](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_77.png)

1. From the command line, navigate to the root folder for the project and execute the following command:

    ```console
    gulp ngrok-serve
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_78](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_78.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_79](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_79.png)

1. Upgrade the previously deployed Teams app with the updated app package.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_80](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_80.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_81](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_81.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_82](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_82.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_83](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_83.png)

    

    ![02-Exercise-1-Collecting-user-input-with-task-modules_85](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_85.png)

    

1. In the browser, navigate back to the tab in the Microsoft Teams interface. Select the **Show video** button. Microsoft Teams will load the video player task module with the specified video loaded in the embedded player:

    ![02-Exercise-1-Collecting-user-input-with-task-modules_86](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_86.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_87](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_87.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_88](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_88.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_89](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_89.png)

1. Stop the local web server by pressing <kbd>CTRL</kbd>+<kbd>C</kbd> in the console to stop the running process.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_90](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_90.png)

## Task 3: Add video selector task module

Now let's update the project to include a task module that will enable the user to change the video loaded in the player task module. For this task module, you'll implement it similar to how the custom tab is implemented: as a React app.

### Create the task module's React app web page host

1. Create a new file, **selector.html**, in the **./src/public/youTubePlayer1Tab** folder.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_91](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_91.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_92](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_92.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_93](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_93.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_94](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_94.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_95](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_95.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_96](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_96.png)

1. Add the following HTML to it:

    ```html
    <!DOCTYPE html>
    <html>
    
    <head>
      <meta charset="UTF-8">
      <title>YouTube Video Selector</title>
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <!-- inject:css -->
      <!-- endinject -->
      <style>
        #app {
          margin-left: 20px;
          margin-right: 20px;
          margin-top: 10px;
          margin-bottom: 10px;
        }
      </style>
    </head>
    
    <body>
      <div id='app'>
        Loading...
      </div>
      <!-- inject:js -->
      <!-- endinject -->
      <script type='text/javascript'>
        youTubePlayer.render(youTubePlayer.VideoSelectorTaskModule, document.getElementById('app'), {});
      </script>
    </body>
    
    </html>
    ```

![02-Exercise-1-Collecting-user-input-with-task-modules_97](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_97.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_98](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_98.png)



### Register the new page

Next, register the page you created in the last step with the project's hosting infrastructure. This will also add the necessary HTTP headers to the page's response to ensure it can be loaded within an IFRAME, but only within a Microsoft Teams client.

1. Create a new file, **VideoSelectorTaskModule.ts**, in the **./src/server/youTubePlayer1Tab** folder.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_99](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_99.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_100](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_100.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_101](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_101.png)

1. Add the following code to the file:

    ```typescript
    import { PreventIframe } from "express-msteams-host";
    
    @PreventIframe("/youTubePlayer1Tab/selector.html")
    
    export class VideoSelectorTaskModule { }
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_102](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_102.png)

1. Now register the page by adding the following line to the end of the **./src/server/TeamsAppComponents.ts** file:

    ```typescript
    export * from "./youTubePlayer1Tab/VideoSelectorTaskModule";
    ```

![02-Exercise-1-Collecting-user-input-with-task-modules_103](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_103.png)

![02-Exercise-1-Collecting-user-input-with-task-modules_104](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_104.png)

### Implement the React app for the selector task module

With the selector's page created and registered, the next step is to implement the React app that is loaded in the page.

1. Create a new file, **VideoSelectorTaskModule.tsx**, in the folder **./src/client/youTubePlayer1Tab**.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_105](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_105.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_106](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_106.png)

1. Add the following code to the page. Most of this code mirrors what you would see if you created a new tab.

    ```typescript
    import * as React from "react";
    import { Provider, Flex, Text, Button, Header, Input } from "@fluentui/react-northstar";
    import { useState, useEffect } from "react";
    import { useTeams, getQueryVariable } from "msteams-react-base-component";
    import * as microsoftTeams from "@microsoft/teams-js";
    ```


    export const VideoSelectorTaskModule = () => {
    
      const [{ inTeams, theme, context }] = useTeams();
      const [entityId, setEntityId] = useState<string | undefined>();
      const [youTubeVideoId, setYouTubeVideoId] = useState<string | undefined>("VlEH4vtaxp4");
    
      useEffect(() => {
        if (inTeams === true) {
          microsoftTeams.appInitialization.notifySuccess();
        } else {
          setEntityId("Not in Microsoft Teams");
        }
      }, [inTeams]);
    
      useEffect(() => {
        if (context) {
          setEntityId(context.entityId);
          setYouTubeVideoId(getQueryVariable("vid"));
        }
      }, [context]);
    
      return (
      );
    };
    ```

![02-Exercise-1-Collecting-user-input-with-task-modules_107](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_107.png)

1. Implement the user interface of the task module by adding the following code to the `return()` statement:

    ```tsx
    <Provider theme={theme}>
      <Flex column gap="gap.smaller">
        <Text size="medium">
          Enter the ID of a YouTube video to show in the task module player.
        </Text>
        <Input value={youTubeVideoId} onChange={(e) => handleOnChanged(e)}></Input>
        <Button content="Update" primary onClick={() => handleOnClick()}></Button>
      </Flex>
    </Provider>
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_108](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_108.png)

1. Next, implement the two handlers referenced in the `render()` method. Add these two functions to the `VideoSelectorTaskModule` class:

    ```typescript
    const handleOnChanged = (event): void => {
      setYouTubeVideoId(event.target.value);
    };
    
    const handleOnClick = (): void => {
      microsoftTeams.tasks.submitTask(youTubeVideoId, undefined);
    };
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_109](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_109.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_110](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_110.png)

    The `handleOnChanged()` method updates the state with the value specified in the input control, while the `handleOnClick()` method uses the Microsoft Teams SDK to pass the ID of the video back to the personal tab.

1. Make this React class available to the rest of the application by adding the following line to the **./src/client/client.ts** file:

    ```typescript
    export * from "./youTubePlayer1Tab/VideoSelectorTaskModule";
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_111](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_111.png)

1. The last step is to wire this task module up to the tab. Within the **./src/client/youTubePlayer1Tab/YouTubePlayer1Tab.tsx** file, locate the method `onChangeVideo()`. Add the following code to the method:

    ```typescript
    const taskModuleInfo = {
      title: "YouTube Video Selector",
      url: appRoot() + `/youTubePlayer1Tab/selector.html?theme={theme}&vid=${youTubeVideoId}`,
      width: 350,
      height: 150
    };
    
    const submitHandler = (err: string, result: string): void => {
      console.log(`Submit handler - err: ${err}`);
      setYouTubeVideoId(result);
    };
    
    microsoftTeams.tasks.startTask(taskModuleInfo, submitHandler);
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_113](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_113.png)
    
    ![02-Exercise-1-Collecting-user-input-with-task-modules_114](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_114.png)
    
    This code will first create the `taskInfo` object that defines the task module. It also creates a callback that will take the result from the task module and use it to update the state of the React app.

### Test the video selector task module

1. Increment the `version` property in the app's **./manifest/manifest.json** file so you can update the previously deployed Teams app.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_115](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_115.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_116](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_116.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_117](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_117.png)

1. From the command line, navigate to the root folder for the project and execute the following command:

    ```console
    gulp ngrok-serve
    ```

    ![02-Exercise-1-Collecting-user-input-with-task-modules_118](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_118.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_119](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_119.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_120](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_120.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_121](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_121.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_122](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_122.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_123](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_123.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_124](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_124.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_124a](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_124a.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_125](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_125.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_126](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_126.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_127](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_127.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_128](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_128.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_129](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_129.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_130](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_130.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_131](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_131.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_132](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_132.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_133](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_133.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_134](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_134.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_135](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_135.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_136](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_136.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_137](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_137.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_138](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_138.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_139](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_139.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_140](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_140.png)

    

1. Upgrade the previously deployed Teams app with the updated app package.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_141](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_141.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_142](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_142.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_143](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_143.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_144](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_144.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_145](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_145.png)

1. In the browser, navigate back to the tab in the Microsoft Teams interface.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_146](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_146.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_147](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_147.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_148](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_148.png)

1. Select the **Change Video ID** button. Microsoft Teams will load the video selector task module with the ID of the currently selected video in the text control.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_149](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_149.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_150](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_150.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_151](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_151.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_152](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_152.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_153](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_153.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_154](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_154.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_155](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_155.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_156](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_156.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_157](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_157.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_158](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_158.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_159](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_159.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_160](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_160.png)

    

1. Enter the ID of another YouTube video and select the **Update** button. Notice the ID of the video has changed. Now when you select the **Show video** button, the player task module loads with the new video.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_161](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_161.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_162](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_162.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_163](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_163.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_164](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_164.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_165](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_165.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_166](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_166.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_167](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_167.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_168](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_168.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_169a](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_169a.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_169b](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_169b.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_170](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_170.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_171](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_171.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_172](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_172.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_173](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_173.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_174](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_174.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_175](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_175.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_176](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_176.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_177](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_177.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_178](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_178.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_179](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_179.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_180](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_180.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_181](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_181.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_182](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_182.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_183](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_183.png)

    

1. Stop the local web server by pressing <kbd>CTRL</kbd>+<kbd>C</kbd> in the console to stop the running process.

    ![02-Exercise-1-Collecting-user-input-with-task-modules_184](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_184.png)

    ![02-Exercise-1-Collecting-user-input-with-task-modules_185](Evidencia/02-Exercise-1-Collecting-user-input-with-task-modules_185.png)

## Summary

In this exercise, you learned the basics of task modules in Microsoft Teams and how to collect input from users in a custom Teams tab. After creating a new Microsoft Teams personal tab, you added two task modules to it.