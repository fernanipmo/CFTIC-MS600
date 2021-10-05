# Exercise 5: Implementing authorization to consume an API

This exercise demonstrates how a JavaScript single-page application (SPA) can:

- Sign in personal accounts, as well as work and school accounts.

- Acquire an access token.

- Call the Microsoft Graph API or other APIs that require access tokens from the Microsoft identity platform endpoint.

The sample application used in this exercise enables a JavaScript SPA to query the Microsoft Graph API or a web API that accepts tokens from the Microsoft identity platform endpoint. In this scenario, after a user signs in, an access token is requested and added to HTTP requests through the authorization header. Token acquisition and renewal are handled by the Microsoft Authentication Library (MSAL).

![06-Exercise-5-Implementing-authorization-to-consume-an-API_Arch_00](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_Arch_00.png)

## Task 1: Download sample project

1. Download the sample project for Node.js:

    1. To run the project by using a local web server, such as Node.js, download the project files to your **C:/Labfiles** directory.

        Visit [https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/releases](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/releases) and download the latest release: **Source code (zip)**.
        
        ![06-Exercise-5-Implementing-authorization-to-consume-an-API_01](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_01.png)
        
        ![06-Exercise-5-Implementing-authorization-to-consume-an-API_02](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_02.png)


1. Navigate to where the download zip file is and unblock file.

    1. Right-select and select **Properties**.

    1. Select the **Unblock** checkbox and select **OK**.

1. Extract the zipped file.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_03](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_03.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_04](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_04.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_05](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_05.png)

1. Open the project in Visual Studio Code.

    1. Launch Visual Studio Code as Administrator and browse for the **active-directory-javascript-graphapi-v2-quickstart** root directory and open.
    
       ![06-Exercise-5-Implementing-authorization-to-consume-an-API_06](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_06.png)
    
       ![06-Exercise-5-Implementing-authorization-to-consume-an-API_07](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_07.png)
       
       

## Task 2: Register an application

1. On the left menu, navigate to **App registrations**.

     ![06-Exercise-5-Implementing-authorization-to-consume-an-API_08](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_08.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_09](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_09.png)

1. Select **New Registration**.

     ![06-Exercise-5-Implementing-authorization-to-consume-an-API_10](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_10.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_11](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_11.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_12](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_12.png)

1. From the **Register an application** pane, perform the following actions:

    1. In the **Name** text box, enter a meaningful application name that will be displayed to users of the app, for example **JavaScript-SPA-App**.

    1. Under **Supported account type**, select **Accounts in any organizational directory and personal Microsoft accounts**.
    
       ![06-Exercise-5-Implementing-authorization-to-consume-an-API_07](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_07.png)
    
       ![06-Exercise-5-Implementing-authorization-to-consume-an-API_08](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_08.png)
    
       

### For setting a redirect URL for the Node.js project

Follow these steps if you choose to use the Node.js project. For Node.js, you can set the web server port in the server.js file. This project uses port 30662, but you can use any other available port.

1. To set up a redirect URL in the application registration information, switch back to the **Application Registration** pane, and do either of the following:

    1. Set **`http://localhost:30662/`** as the **Redirect URL**.

    1. If you're using a custom TCP port, use **`http://localhost:[port]/`** (where **[port]** is the custom TCP port number).

1. Select **Register**.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_13](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_13.png)

1. On the app **Overview** page, note the **Application (client) ID** value for later use.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_14](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_14.png)

1. This sample project requires the **Implicit grant flow** to be enabled. In the left pane of the registered application, select **Authentication**.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_15](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_15.png)

1. In **Advanced** settings, under **Implicit grant**, select the **ID tokens** and **Access tokens** check boxes. ID tokens and access tokens are required because this app must sign in users and call an API.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_16](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_16.png)

1. Select **Save**.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_17](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_17.png)

## Task 3: Permission and scope setup

### Update the App API permissions

1. In the left navigation, navigate to **API Permissions**.

1. Select **Add a permission**.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_18](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_18.png)

1. Next, select **Microsoft Graph** from **Microsoft APIs**.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_19](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_19.png)

1. Select **Delegated Permissions** and under **Select permissions**, search for **calendars** and select **Calendars.Read**.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_20](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_20.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_21](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_21.png)

1. ![06-Exercise-5-Implementing-authorization-to-consume-an-API_22](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_22.png)Search for people and select **People.Read** permission and provide admin consent.

1. Select **Add permissions**.

    1. Wait for **Preparing for consent** to finish then select **Grant admin consent for Contoso**.

    1. From the Permissions requested dialog, select **Yes**.

       ![06-Exercise-5-Implementing-authorization-to-consume-an-API_23](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_23.png)
    
       ![06-Exercise-5-Implementing-authorization-to-consume-an-API_24](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_24.png)
    
    1. Your **JavaScript-SPA-App** app is now configured and authorized to use the Calendars.Read and People.Read permissions for Microsoft Graph.
    
       ![06-Exercise-5-Implementing-authorization-to-consume-an-API_25](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_25.png)

### Update solution code

1. Navigate back to Visual Studio Code and open the **index.html** file.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_26](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_26.png)

1. Locate and select the following code:

    ```html
    <div class="leftContainer">
        <p id="WelcomeMessage">Welcome to the Microsoft Authentication Library For Javascript Quickstart</p>
        <button id="SignIn" onclick="signIn()">Sign In</button>
    </div>
    ```

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_27](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_27.png)

    

1. Replace the selected code with the following, to add a new button to the application:

    ```html
    <div class="leftContainer">
        <p id="WelcomeMessage">Welcome to the Microsoft Authentication Library For Javascript Quickstart</p>
        <button id="SignIn" onclick="signIn()">Sign In</button>
    <button id="Share" onclick="acquireTokenPopupAndCallMSGraph()">Share</button>
    </div>
    ```

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_28](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_28.png)

    

1. Locate the object **requestObj** and change the scopes to **people.read**.

    ```javascript
    var requestObj = {
            scopes: ["people.read"]
        };
    ```

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_29](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_29.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_30](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_30.png)

1. Update the graph API URL to call the people object.

    ```javascript
    var graphConfig = {
            graphMeEndpoint: "https://graph.microsoft.com/v1.0/me",
            graphPeopleEndpoint: "https://graph.microsoft.com/v1.0/people"
        };
    ```

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_31](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_31.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_32](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_32.png)

1. Create a new endpoint for **people.read** and replace the method **acquireTokenPopupAndCallMSGraph** with the code below.

    ```javascript
    function acquireTokenPopupAndCallMSGraph() {
            //Always start with acquireTokenSilent to obtain a token in the signed in user from cache
            myMSALObj.acquireTokenSilent(requestObj).then(function (tokenResponse) {
                callMSGraph(graphConfig.graphMePeopleEndpoint, tokenResponse.accessToken, graphAPICallback);
            }).catch(function (error) {
                console.log(error);
                // Upon acquireTokenSilent failure (due to consent or interaction or login required ONLY)
                // Call acquireTokenPopup(popup window)
                if (requiresInteraction(error.errorCode)) {
                    myMSALObj.acquireTokenPopup(requestObj).then(function (tokenResponse) {
                        callMSGraph(graphConfig.graphPeopleEndpoint, tokenResponse.accessToken, graphAPICallback);
                    }).catch(function (error) {
                        console.log(error);
                    });
                }
            });
        }
    ```

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_33](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_33.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_34](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_34.png)

1. Find the **var msalConfig** code block and replace the following:

    1. `<Enter_the_Application_Id_here>` is the **Application (client) ID** for the application you registered.

    1. `<Enter_the_Tenant_info_here>` is set to one of the following options:

        ![06-Exercise-5-Implementing-authorization-to-consume-an-API_35](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_35.png)

        - If your application supports **Accounts in this organizational directory**, replace this value with the **Tenant ID** or **Tenant** **name** (for example, **contoso.microsoft.com**).
        - If your application supports **Accounts in any organizational directory**, replace this value with **organizations**.
        - If your application supports **Accounts in any organizational directory and personal Microsoft accounts**, replace this value with **common**. To restrict support to Personal Microsoft accounts only, replace this value with **consumers**.
        
        ![06-Exercise-5-Implementing-authorization-to-consume-an-API_36](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_36.png)
        
        ![06-Exercise-5-Implementing-authorization-to-consume-an-API_37](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_37.png)

## Task 4: Run the application

1. From **Visual Studio Code**, open **Terminal**. Type the following and hit ENTER:

    ```typescript
    npm install
    ```

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_38](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_38.png)

1. From the Terminal, type the following and hit ENTER.

    ```typescript
    node server.js
    ```

1. From the browser, launch: **`http://localhost:30662`**

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_39](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_39.png)

    

1. Select **Sign In**.

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_40](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_40.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_41](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_41.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_42](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_42.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_43](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_43.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_44](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_44.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_45](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_45.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_46](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_46.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_47](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_47.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_48](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_48.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_49](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_49.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_50](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_50.png)

    ![06-Exercise-5-Implementing-authorization-to-consume-an-API_51](Evidencia/06-Exercise-5-Implementing-authorization-to-consume-an-API_51.png)

1. If the **Permissions requested** dialog opens, select **Accept**.

    ![Call localhost 30662 showing sign in screen.](../../Linked_Image_Files/l01_exercise_5_task_3_image_5.png)

1. You should now be authenticated successfully.

    ![Logged in successfully to sample project.](../../Linked_Image_Files/l01_exercise_5_task_3_image_6.png)

1. Go back to the Visual Studio Code project. Stop the running project by selecting **Ctrl + C**.

1. Exit Visual Studio Code.

## Review

In this exercise, you implemented authorization and incremental consent using the Microsoft Identity.



[Readme](https://github.com/fernanipmo/CFTIC-MS600#readme)

