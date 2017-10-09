## <a name="obtain-an-azure-resource-manager-token"></a>Ottenere un token di Azure Resource Manager
Azure Active Directory deve autenticare tutte le attività da eseguire sulle risorse con Gestione risorse di Azure hello hello. Hello esempio illustrato di seguito utilizza l'autenticazione di password, per altri approcci, vedere [richiede l'autenticazione di Azure Resource Manager][lnk-authenticate-arm].

1. Aggiungere i seguenti toohello codice hello **Main** metodo in Program.cs tooretrieve un token da Azure AD tramite l'id dell'applicazione hello e una password.
   
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
2. Creare un **ResourceManagementClient** dell'oggetto che utilizza hello token aggiungendo hello successivo toohello codice alla fine di hello **Main** metodo:
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Creare o ottenere un riferimento, hello nel gruppo di risorse in uso:
   
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