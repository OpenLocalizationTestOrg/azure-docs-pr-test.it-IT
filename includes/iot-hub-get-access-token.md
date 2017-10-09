## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="9ce2e-101">Ottenere un token di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9ce2e-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="9ce2e-102">Azure Active Directory deve autenticare tutte le attività da eseguire sulle risorse con Gestione risorse di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="9ce2e-102">Azure Active Directory must authenticate all hello tasks that you perform on resources using hello Azure Resource Manager.</span></span> <span data-ttu-id="9ce2e-103">Hello esempio illustrato di seguito utilizza l'autenticazione di password, per altri approcci, vedere [richiede l'autenticazione di Azure Resource Manager][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="9ce2e-103">hello example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="9ce2e-104">Aggiungere i seguenti toohello codice hello **Main** metodo in Program.cs tooretrieve un token da Azure AD tramite l'id dell'applicazione hello e una password.</span><span class="sxs-lookup"><span data-stu-id="9ce2e-104">Add hello following code toohello **Main** method in Program.cs tooretrieve a token from Azure AD using hello application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. <span data-ttu-id="9ce2e-105">Creare un **ResourceManagementClient** dell'oggetto che utilizza hello token aggiungendo hello successivo toohello codice alla fine di hello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="9ce2e-105">Create a **ResourceManagementClient** object that uses hello token by adding hello following code toohello end of hello **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="9ce2e-106">Creare o ottenere un riferimento, hello nel gruppo di risorse in uso:</span><span class="sxs-lookup"><span data-stu-id="9ce2e-106">Create, or obtain a reference to, hello resource group you are using:</span></span>
   
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