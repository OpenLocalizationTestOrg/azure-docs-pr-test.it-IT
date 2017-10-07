---
title: aaaGet introduttiva hello libreria rete CDN di Azure per .NET | Documenti Microsoft
description: Informazioni su come toomanage di applicazioni .NET toowrite rete CDN di Azure con Visual Studio.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Introduzione allo sviluppo della rete CDN di Azure
> [!div class="op_single_selector"]
> * [Node.JS](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

È possibile utilizzare hello [libreria rete CDN di Azure per .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creazione e la gestione dei profili di rete CDN e gli endpoint.  In questa esercitazione vengono illustrati la creazione di hello di una semplice applicazione console .NET che illustra diverse operazioni hello disponibili.  In questa esercitazione è non è adatto toodescribe tutti gli aspetti di hello libreria rete CDN di Azure per .NET in modo dettagliato.

È necessario Visual Studio 2015 toocomplete questa esercitazione.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) è disponibile gratuitamente per il download.

> [!TIP]
> Hello [progetto completato questa esercitazione](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) è disponibile per il download su MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Creare il progetto e aggiungere i pacchetti Nuget
Ora che è stato creato un gruppo di risorse per i profili di rete CDN e specificati i profili di rete CDN di Azure AD applicazione autorizzazione toomanage e gli endpoint all'interno del gruppo, è possibile iniziare a creare l'applicazione.

All'interno di Visual Studio 2015, scegliere **File**, **New**, **progetto...**  finestra Nuovo progetto di tooopen hello.  Espandere **Visual c#**, quindi selezionare **Windows** nel riquadro a sinistra di hello hello.  Fare clic su **applicazione Console** nel riquadro centrale hello.  Assegnare un nome al progetto e fare clic su **OK**.  

![Nuovo progetto](./media/cdn-app-dev-net/cdn-new-project.png)

Il progetto verrà toouse alcune librerie di Azure contenuti nei pacchetti di Nuget.  Aggiungere tali progetto toohello.

1. Fare clic su hello **strumenti** menu **Gestione pacchetti Nuget**, quindi **Package Manager Console**.
   
    ![Gestisci pacchetti NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. Nella Console di gestione pacchetti hello, eseguire hello successivo comando tooinstall hello **Active Directory Authentication Library (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Eseguire hello seguente hello tooinstall **libreria di gestione della rete CDN di Azure**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Direttive, costanti, metodo main e metodi helper
Possiamo procedere alla struttura di base di questo programma scritto hello.

1. Nella scheda Program.cs hello, sostituire hello `using` direttive all'inizio di hello con seguenti hello:
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. È necessario toodefine alcune costanti che utilizzeranno i metodi.  In hello `Program` (classe), ma prima dell'esecuzione hello `Main` metodo, aggiungere il seguente hello.  Essere tooreplace che segnaposto hello, tra cui hello  **&lt;angolari&gt;**, con valori personalizzati in base alle esigenze.
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Anche a livello di classe hello, definire queste due variabili.  Useremo queste toodetermine successive se il profilo e l'endpoint esiste già.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Sostituire hello `Main` metodo come indicato di seguito:
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. Alcuni dei nostri altri metodi sta utente hello tooprompt con domande "Sì/No".  Aggiungere hello toomake metodo dopo che un po' più semplice:
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

Struttura di base hello di questo programma è stato scritto, si dovrebbe creare metodi hello chiamati da hello `Main` metodo.

## <a name="authentication"></a>Autenticazione
Prima di utilizzare hello libreria di gestione della rete CDN di Azure, è necessario dell'entità servizio tooauthenticate e ottenere un token di autenticazione.  Questo metodo Usa token hello tooretrieve ADAL.

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

Se si utilizza l'autenticazione utente, hello `GetAccessToken` metodo avrà un aspetto leggermente diverso.

> [!IMPORTANT]
> Usare questo esempio di codice solo se si sceglie l'autenticazione utente toohave anziché un'entità servizio.
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

Tooreplace assicurarsi di essere `<redirect URI>` con hello URI di reindirizzamento di immesso al momento della registrazione di un'applicazione hello in Azure AD.

## <a name="list-cdn-profiles-and-endpoints"></a>Elencare i profili e gli endpoint della rete CDN
Si è pronti tooperform operazioni di rete CDN.  Hello prima cosa il metodo è l'elenco di tutti i profili di hello e gli endpoint in questo gruppo di risorse e se viene trovata una corrispondenza per i nomi di endpoint e profilo di hello specificato nel nostro costanti, annota che per un momento successivo, in modo non si eseguono tentativi toocreate duplicati.

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Creare profili ed endpoint della rete CDN
Ora si creerà un profilo.

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

Una volta creato il profilo di hello, verrà creato un endpoint.

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> esempio Hello precedente assegna endpoint hello un'entità origin denominata *Contoso* con un nome host `www.contoso.com`.  È necessario modificare questo toopoint tooyour personalizzate del nome host dell'origine.
> 
> 

## <a name="purge-an-endpoint"></a>Ripulire un endpoint
Supponendo che l'endpoint di hello è stato creato, un'attività comune che si voglia tooperform in questo programma è eliminazione contenuto hello in questo endpoint.

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> Nell'esempio hello sopra, hello stringa `/*` indica che desidera toopurge tutti gli elementi nella directory radice del percorso dell'endpoint hello hello.  Questo è l'equivalente toochecking **ripulire tutti** in hello Azure portal "Elimina" finestra di dialogo. In hello `CreateCdnProfile` metodo, creato il profilo come un **rete CDN di Azure da Verizon** profilo mediante il codice hello `Sku = new Sku(SkuName.StandardVerizon)`, in modo che sia corretta.  Tuttavia, **rete CDN di Azure da Akamai** non supportano i profili **ripulire tutti**, pertanto se si è dato dal fatto utilizzando un profilo di Akamai per questa esercitazione, è necessario tooinclude percorsi specifici toopurge.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>Eliminare profili ed endpoint della rete CDN
metodi ultimo Hello eliminerà l'endpoint e un profilo.

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a>Programma hello in esecuzione
Ora possiamo compilare ed eseguire il programma di hello facendo hello **avviare** pulsante in Visual Studio.

![Il programma in esecuzione](./media/cdn-app-dev-net/cdn-program-running-1.png)

Quando il programma hello raggiunge hello sopra prompt dei comandi, dovrebbero essere in grado di tooreturn tooyour risorse gruppo hello portale di Azure e che sia stato creato il profilo di hello.

![Completamento della procedura](./media/cdn-app-dev-net/cdn-success.png)

È quindi possibile verificare hello richieste toorun hello resto del programma hello.

![Il completamento del programma](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Passaggi successivi
il progetto completato hello toosee da questa procedura dettagliata, [scaricare l'esempio hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

documentazione aggiuntiva toofind su hello libreria di gestione della rete CDN di Azure per .NET, hello vista [reference sul sito MSDN](https://msdn.microsoft.com/library/mt657769.aspx).

Gestire le risorse della rete CDN con [PowerShell](cdn-manage-powershell.md).

