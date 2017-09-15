## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="cc747-101">Ottenere un token di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cc747-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="cc747-102">Azure Active Directory deve autenticare tutte le attività da eseguire sulle risorse con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc747-102">Azure Active Directory must authenticate all the tasks that you perform on resources using the Azure Resource Manager.</span></span> <span data-ttu-id="cc747-103">Nell'esempio illustrato di seguito si usa l'autenticazione della password. Per altri approcci, vedere [Autenticazione delle richieste di Azure Resource Manager][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="cc747-103">The example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="cc747-104">Aggiungere il codice seguente al metodo **Main** in Program.cs per recuperare un token da Azure AD tramite l'id dell'applicazione e la password.</span><span class="sxs-lookup"><span data-stu-id="cc747-104">Add the following code to the **Main** method in Program.cs to retrieve a token from Azure AD using the application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed to obtain the token");
      return;
    }
    ```
2. <span data-ttu-id="cc747-105">Creare un oggetto **ResourceManagementClient** che usa il token aggiungendo il codice seguente alla fine del metodo **Main**:</span><span class="sxs-lookup"><span data-stu-id="cc747-105">Create a **ResourceManagementClient** object that uses the token by adding the following code to the end of the **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="cc747-106">Creare o ottenere un riferimento al gruppo di risorse in uso:</span><span class="sxs-lookup"><span data-stu-id="cc747-106">Create, or obtain a reference to, the resource group you are using:</span></span>
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx