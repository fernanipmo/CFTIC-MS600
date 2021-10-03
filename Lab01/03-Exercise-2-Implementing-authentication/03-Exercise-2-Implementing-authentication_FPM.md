﻿# Exercise 2: Implementing authentication

This exercise will demonstrate the different account types that are used within the Microsoft identity platform.

**Note**:
This exercise demonstrates signing into a web application using two different accounts. These two accounts will come from two organizations, one of them being the organization where the Azure AD application is registered. Therefore, in order to complete the exercise, you'll need access to two user accounts in different Azure AD directories.

## Task 1: Create application that only allows single organization sign in

In this task, you will register an application in the Azure portal that allows users from the current organization to sign in.
### Register a single-tenant Azure AD application

1. From the Azure portal [https://portal.azure.com](https://portal.azure.com/), navigate to **Azure Active Directory**.

    ![03-Exercise-2-Implementing-authentication_01](Evidencia/03-Exercise-2-Implementing-authentication_01.png)

    

1. Select **Manage > App registrations** in the left-hand navigation.

    ![03-Exercise-2-Implementing-authentication_02](Evidencia/03-Exercise-2-Implementing-authentication_02.png)

1. On the **App registrations** page, select **New registration**.

    ![03-Exercise-2-Implementing-authentication_03](Evidencia/03-Exercise-2-Implementing-authentication_03.png)

1. On the **Register an application** page, set the values as follows:

    - **Name**: Hello ASPNET Core Identity 01

    - **Supported account types**: Accounts in this organizational directory only (Single tenant)

1. Select **Register** to create the application.

    ![03-Exercise-2-Implementing-authentication_04](Evidencia/03-Exercise-2-Implementing-authentication_04.png)

1. On the **Hello ASPNET Core Identity 01** page, copy the values **Application (client) ID** and **Directory (tenant) ID**; you'll need these values later in this exercise.

    ![03-Exercise-2-Implementing-authentication_05](Evidencia/03-Exercise-2-Implementing-authentication_05.png)

1. On the **Hello ASPNET Core Identity 01** page, select the **Add a Redirect URI** link under the **Redirect URIs**.

    ![03-Exercise-2-Implementing-authentication_06](Evidencia/03-Exercise-2-Implementing-authentication_06.png)

    ![03-Exercise-2-Implementing-authentication_07](Evidencia/03-Exercise-2-Implementing-authentication_07.png)

1. Locate the section **Redirect URIs** and add the following two URLs:

    - **https://localhost:3007**

    - **https://localhost:3007/signin-oidc**

      ![03-Exercise-2-Implementing-authentication_08](Evidencia/03-Exercise-2-Implementing-authentication_08.png)

1. Add the following **Logout URL**: **https://localhost:3007/signout-oidc**

    ![03-Exercise-2-Implementing-authentication_09](Evidencia/03-Exercise-2-Implementing-authentication_09.png)

    

1. Locate the section **Implicit grant** and select both **Access tokens** and **ID tokens**. This tells Azure AD to return these tokens the authenticated user if requested.

1. Select **Save** when finished setting these values.

![03-Exercise-2-Implementing-authentication_10](Evidencia/03-Exercise-2-Implementing-authentication_10.png)

![03-Exercise-2-Implementing-authentication_11](Evidencia/03-Exercise-2-Implementing-authentication_11.png)

![03-Exercise-2-Implementing-authentication_12](Evidencia/03-Exercise-2-Implementing-authentication_12.png)

## Task 2: Create a single organization ASP.NET core web application

In this first application, you'll create an ASP.NET Core web application that allows users from the current organization to sign in and display their information.
1. Open your command prompt, navigate to a directory where you want to save your work, create a new folder, and change directory into that folder. For example:

    ```powershell
    Cd c:/LabFiles
    md SingleOrg
    cd SingleOrg
    ```

    ![03-Exercise-2-Implementing-authentication_13](Evidencia/03-Exercise-2-Implementing-authentication_13.png)

1. Execute the following command to create a new ASP.NET Core MVC web application:

    ```powershell
    dotnet new mvc --auth SingleOrg
    ```

    ![03-Exercise-2-Implementing-authentication_14](Evidencia/03-Exercise-2-Implementing-authentication_14.png)

1. Open the folder in Visual Studio code by executing from the project directory: `code .`

    ![03-Exercise-2-Implementing-authentication_15](Evidencia/03-Exercise-2-Implementing-authentication_15.png)

### Configure the web application with the Azure AD application you created

1. Locate and open the **./appsettings.json** file in the ASP.NET Core project.

1. Set the **AzureAd.Domain** property to the domain of your Azure AD tenant where you created the Azure AD application (*for example: contoso.onmicrosoft.com*).

   ![03-Exercise-2-Implementing-authentication_16](Evidencia/03-Exercise-2-Implementing-authentication_16.png)

   ![03-Exercise-2-Implementing-authentication_17](Evidencia/03-Exercise-2-Implementing-authentication_17.png)

1. Set the **AzureAd.TenantId** property to the **Directory (tenant) ID** you copied when creating the Azure AD application in the previous step.

1. Set the **AzureAd.ClientId** property to the **Application (client) ID** you copied when creating the Azure AD application in the previous step.

   ![03-Exercise-2-Implementing-authentication_18](Evidencia/03-Exercise-2-Implementing-authentication_18.png)

   

   ![03-Exercise-2-Implementing-authentication_18a](Evidencia/03-Exercise-2-Implementing-authentication_18a.png)

### Update the web application's launch configuration

1. Locate and open the **./Properties/launchSettings.json** file in the ASP.NET Core project.

   ![03-Exercise-2-Implementing-authentication_19](Evidencia/03-Exercise-2-Implementing-authentication_19.png)

1. Set the **iisSettings.iisExpress.applicationUrl** property to **https://localhost:3007**.

1. Set the **iisSettings.iisExpress.sslPort** property to **3007**.

   ![03-Exercise-2-Implementing-authentication_20](Evidencia/03-Exercise-2-Implementing-authentication_20.png)

   

### Update the user experience

1. Finally, update the user experience of the web application to display all the claims in the OpenID Connect ID token.

1. Locate and open the **./Views/Home/Index.cshtml** file.

    ![03-Exercise-2-Implementing-authentication_21](Evidencia/03-Exercise-2-Implementing-authentication_21.png)

1. Add the following code to the end of the file:

    ```powershell
    @if (User.Identity.IsAuthenticated)
    {
    <div>
        <table cellpadding="2" cellspacing="2">
            <tr>
                <th>Claim</th>
                <th>Value</th>
            </tr>
            @foreach (var claim in User.Claims)
            {
                <tr>
                    <td>@claim.Type</td>
                    <td>@claim.Value</td>
                </tr>
            }
        </table>
    </div>
    }
    ```

![03-Exercise-2-Implementing-authentication_24](Evidencia/03-Exercise-2-Implementing-authentication_24.png)

![03-Exercise-2-Implementing-authentication_24a](Evidencia/03-Exercise-2-Implementing-authentication_24a.png)

![03-Exercise-2-Implementing-authentication_25](Evidencia/03-Exercise-2-Implementing-authentication_25.png)



## Task 3: Build and test the single organization web app

1. Execute the following command in a command prompt to compile and run the application:

    ```powershell
    dotnet build
    dotnet run
    ```

    ![03-Exercise-2-Implementing-authentication_26](Evidencia/03-Exercise-2-Implementing-authentication_26.png)

    

1. Open a browser and navigate to the url **https://localhost:5001**. The web application will redirect you to the Azure AD sign in page.

    ![03-Exercise-2-Implementing-authentication_27](Evidencia/03-Exercise-2-Implementing-authentication_27.png)

1. Sign in using a Work and School account from your Azure AD directory. Azure AD will redirect you back to the web application. Notice some of the details from the claims included in the ID token.

    ![03-Exercise-2-Implementing-authentication_28](Evidencia/03-Exercise-2-Implementing-authentication_28.png)

1. Take special note of the **tenantid** and **upn** claim. These claims indicate the ID of the Azure AD directory and ID of the user that signed in. Make a note of these values to compare them to other options in a minute.

    ![03-Exercise-2-Implementing-authentication_28a](Evidencia/03-Exercise-2-Implementing-authentication_28a.png)

    ![03-Exercise-2-Implementing-authentication_28b](Evidencia/03-Exercise-2-Implementing-authentication_28b.png)

1. Now try logging in as a user from a different organization. Select the **Sign out** link in the top left. Wait for Azure AD and the web application signs out the current user. When the web application reloads, repeat the sign in process, except this time try signing in as a user from a different organization or use a Microsoft Account.

    ![03-Exercise-2-Implementing-authentication_28c](Evidencia/03-Exercise-2-Implementing-authentication_28c.png)

    ![03-Exercise-2-Implementing-authentication_28d](Evidencia/03-Exercise-2-Implementing-authentication_28d.png)

    ![03-Exercise-2-Implementing-authentication_29](Evidencia/03-Exercise-2-Implementing-authentication_29.png)

    ![03-Exercise-2-Implementing-authentication_30](Evidencia/03-Exercise-2-Implementing-authentication_30.png)

    ![03-Exercise-2-Implementing-authentication_31](Evidencia/03-Exercise-2-Implementing-authentication_31.png)

    ![03-Exercise-2-Implementing-authentication_32](Evidencia/03-Exercise-2-Implementing-authentication_32.png)

    

1. Notice Azure AD will reject the user's sign in, explaining that the user's account doesn't exist in the current tenant.

    ![03-Exercise-2-Implementing-authentication_33](Evidencia/03-Exercise-2-Implementing-authentication_33.png)

1. Stop the web server by pressing **CTRL+C** in the command prompt.

    ![03-Exercise-2-Implementing-authentication_34](Evidencia/03-Exercise-2-Implementing-authentication_34.png)

    ![03-Exercise-2-Implementing-authentication_36](Evidencia/03-Exercise-2-Implementing-authentication_36.png)

## Task 4: Create application that allows any organization's users to sign in

In this task, you will register an application in the Azure portal that allows users from any organization or Microsoft Accounts to sign in.
### Register a multi-tenant Azure AD application

1. From the Azure portal [https://portal.azure.com](https://portal.azure.com/), navigate to **Azure Active Directory**.

1. Select **Manage > App registrations** in the left-hand navigation.

1. On the **App registrations** page, select **New registration**.

    ![03-Exercise-2-Implementing-authentication_35](Evidencia/03-Exercise-2-Implementing-authentication_35.png)

1. On the **Register an application** page, set the values as follows:

    - **Name:** Hello ASPNET Core Identity 02

    - **Supported account types**: Accounts in any organizational directory only (Any Azure AD directory - Multitenant)

1. Select **Register** to create the application.

    ![03-Exercise-2-Implementing-authentication_37](Evidencia/03-Exercise-2-Implementing-authentication_37.png)

    ![03-Exercise-2-Implementing-authentication_38](Evidencia/03-Exercise-2-Implementing-authentication_38.png)

1. On the **Hello ASPNET Core Identity 02** page, copy the values **Application (client) ID** and **Directory (tenant) ID**; you'll need these values later in this exercise.

    ![03-Exercise-2-Implementing-authentication_39](Evidencia/03-Exercise-2-Implementing-authentication_39.png)

1. On the **Hello ASPNET Core Identity 02** page, select the **Add a Redirect URI** link under the **Redirect URIs**.

    ![03-Exercise-2-Implementing-authentication_40](Evidencia/03-Exercise-2-Implementing-authentication_40.png)

    ![03-Exercise-2-Implementing-authentication_41](Evidencia/03-Exercise-2-Implementing-authentication_41.png)

1. Locate the section **Redirect URIs** and add the following two URLs:

    - **https://localhost:3007**

    - **https://localhost:3007/signin-oidc**

      ![03-Exercise-2-Implementing-authentication_42](Evidencia/03-Exercise-2-Implementing-authentication_42.png)

1. Add the following **Logout URL**: **https://localhost:3007/signout-oidc**

    ![03-Exercise-2-Implementing-authentication_43](Evidencia/03-Exercise-2-Implementing-authentication_43.png)

1. Locate the section **Implicit grant** and select both **Access tokens** and **ID tokens**. This tells Azure AD to return these tokens the authenticated user if requested.

1. Select **Save** when finished setting these values.

     ![03-Exercise-2-Implementing-authentication_44](Evidencia/03-Exercise-2-Implementing-authentication_44.png)

     ![03-Exercise-2-Implementing-authentication_45](Evidencia/03-Exercise-2-Implementing-authentication_45.png)



## Task 5: Create a multiple organization ASP.NET core web application

In this second application, you'll create an ASP.NET Core web application that allows users from any organization or Microsoft Accounts to sign in and display their information.

1. Open your command prompt, navigate to a directory where you want to save your work, create a new folder, and change directory into that folder. For example:

    ```powershell
    Cd c:/LabFiles
    md MultiOrg
    cd MultiOrg
    ```

1. Execute the following command to create a new ASP.NET Core MVC web application:

    ```powershell
    dotnet new mvc --auth MultiOrg
    ```

    ![03-Exercise-2-Implementing-authentication_46](Evidencia/03-Exercise-2-Implementing-authentication_46.png)

1. Open the folder in Visual Studio code by executing from the project directory: `code .`

    ![03-Exercise-2-Implementing-authentication_47](Evidencia/03-Exercise-2-Implementing-authentication_47.png)

### Configure the web application with the Azure AD application you created

1. Locate and open the **./appsettings.json** file in the ASP.NET Core project.

   ![03-Exercise-2-Implementing-authentication_48](Evidencia/03-Exercise-2-Implementing-authentication_48.png)

1. Set the **AzureAd.ClientId** property to the **Application (client) ID** you copied when creating the Azure AD application in the previous step.

   ![03-Exercise-2-Implementing-authentication_49](Evidencia/03-Exercise-2-Implementing-authentication_49.png)

   ![03-Exercise-2-Implementing-authentication_50](Evidencia/03-Exercise-2-Implementing-authentication_50.png)

### Update the web application's launch configuration

1. Locate and open the **./Properties/launchSettings.json** file in the ASP.NET Core project.

   ![03-Exercise-2-Implementing-authentication_51](Evidencia/03-Exercise-2-Implementing-authentication_51.png)

1. Set the **iisSettings.iisExpress.applicationUrl** property to **https://localhost:3007**.

1. Set the **iisSettings.iisExpress.sslPort** property to **3007**.

   ![03-Exercise-2-Implementing-authentication_52](Evidencia/03-Exercise-2-Implementing-authentication_52.png)

   ![03-Exercise-2-Implementing-authentication_53](Evidencia/03-Exercise-2-Implementing-authentication_53.png)

### Update the user experience

1. Finally, update the user experience of the web application to display all the claims in the OpenID Connect ID token.

1. Locate and open the **./Views/Home/Index.cshtml** file.

    ![03-Exercise-2-Implementing-authentication_54](Evidencia/03-Exercise-2-Implementing-authentication_54.png)

1. Add the following code to the end of the file:

    ```powershell
    @if (User.Identity.IsAuthenticated)
    {
    <div>
        <table cellpadding="2" cellspacing="2">
            <tr>
                <th>Claim</th>
                <th>Value</th>
            </tr>
            @foreach (var claim in User.Claims)
            {
                <tr>
                    <td>@claim.Type</td>
                    <td>@claim.Value</td>
                </tr>
            }
        </table>
    </div>
    }
    ```

    ![03-Exercise-2-Implementing-authentication_55](Evidencia/03-Exercise-2-Implementing-authentication_55.png)

1. Save the above all changes.

    ![03-Exercise-2-Implementing-authentication_56](Evidencia/03-Exercise-2-Implementing-authentication_56.png)

## Task 6: Build and test the multiple organization web app

1. Execute the following command in a command prompt to compile and run the application:

    ```powershell
    dotnet build
    dotnet run
    ```

    ![03-Exercise-2-Implementing-authentication_57](Evidencia/03-Exercise-2-Implementing-authentication_57.png)

1. Open a browser and navigate to the url **https://localhost:5001**. The web application will redirect you to the Azure AD sign in page.

    ![03-Exercise-2-Implementing-authentication_58](Evidencia/03-Exercise-2-Implementing-authentication_58.png)

1. Sign in using a Work and School account from your Azure AD directory. Azure AD will redirect you back to the web application. Notice some of the details from the claims included in the ID token.

    ![03-Exercise-2-Implementing-authentication_60](Evidencia/03-Exercise-2-Implementing-authentication_60.png)

    ![03-Exercise-2-Implementing-authentication_61](Evidencia/03-Exercise-2-Implementing-authentication_61.png)

    ![03-Exercise-2-Implementing-authentication_62](Evidencia/03-Exercise-2-Implementing-authentication_62.png)

    ![03-Exercise-2-Implementing-authentication_63](Evidencia/03-Exercise-2-Implementing-authentication_63.png)

1. Take special note of the **tenantid** and **upn** claim. These indicate the ID of the Azure AD directory and ID of the user that signed in. Make a note of these values to compare them to other options in a minute.

    ![03-Exercise-2-Implementing-authentication_34](Evidencia/03-Exercise-2-Implementing-authentication_34.png)

1. Now try logging in as a user from a different organization. Select the **Sign out** link in the top left. Wait for Azure AD and the web application signs out the current user.

    ![03-Exercise-2-Implementing-authentication_65](Evidencia/03-Exercise-2-Implementing-authentication_65.png)

    ![03-Exercise-2-Implementing-authentication_66](Evidencia/03-Exercise-2-Implementing-authentication_66.png)

    ![03-Exercise-2-Implementing-authentication_67](Evidencia/03-Exercise-2-Implementing-authentication_67.png)

1. This time, the user is prompted to first trust the application:

    ![03-Exercise-2-Implementing-authentication_68](Evidencia/03-Exercise-2-Implementing-authentication_68.png)

    ![03-Exercise-2-Implementing-authentication_69](Evidencia/03-Exercise-2-Implementing-authentication_69.png)

1. Select **Accept**.

1. Notice the web application's page loads with different claims, specifically for the **tenantid** and **upn** claim. This indicates the user is not from the current directory where the Azure AD application is registered:

    ![03-Exercise-2-Implementing-authentication_70](Evidencia/03-Exercise-2-Implementing-authentication_70.png)

    ![03-Exercise-2-Implementing-authentication_71](Evidencia/03-Exercise-2-Implementing-authentication_71.png)

    ![03-Exercise-2-Implementing-authentication_72](Evidencia/03-Exercise-2-Implementing-authentication_72.png)

1. Stop the web server by going back to the running project in Visual Studio Code. From the Terminal, press **CTRL+C** in the command prompt.

    ![03-Exercise-2-Implementing-authentication_73](Evidencia/03-Exercise-2-Implementing-authentication_73.png)

## Review

In this exercise, you learned how to create different types of Azure AD applications and use an ASP.NET Core application to support the different sign in options that support different types of accounts.



 [Readme.md](https://github.com/fernanipmo/CFTIC-MS600#readme)
