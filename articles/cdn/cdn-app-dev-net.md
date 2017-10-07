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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="35adf-103">Introduzione allo sviluppo della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="35adf-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35adf-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="35adf-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="35adf-105">.NET</span><span class="sxs-lookup"><span data-stu-id="35adf-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="35adf-106">È possibile utilizzare hello [libreria rete CDN di Azure per .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creazione e la gestione dei profili di rete CDN e gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="35adf-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="35adf-107">In questa esercitazione vengono illustrati la creazione di hello di una semplice applicazione console .NET che illustra diverse operazioni hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="35adf-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="35adf-108">In questa esercitazione è non è adatto toodescribe tutti gli aspetti di hello libreria rete CDN di Azure per .NET in modo dettagliato.</span><span class="sxs-lookup"><span data-stu-id="35adf-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="35adf-109">È necessario Visual Studio 2015 toocomplete questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="35adf-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="35adf-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) è disponibile gratuitamente per il download.</span><span class="sxs-lookup"><span data-stu-id="35adf-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="35adf-111">Hello [progetto completato questa esercitazione](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) è disponibile per il download su MSDN.</span><span class="sxs-lookup"><span data-stu-id="35adf-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="35adf-112">Creare il progetto e aggiungere i pacchetti Nuget</span><span class="sxs-lookup"><span data-stu-id="35adf-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="35adf-113">Ora che è stato creato un gruppo di risorse per i profili di rete CDN e specificati i profili di rete CDN di Azure AD applicazione autorizzazione toomanage e gli endpoint all'interno del gruppo, è possibile iniziare a creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35adf-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="35adf-114">All'interno di Visual Studio 2015, scegliere **File**, **New**, **progetto...**  finestra Nuovo progetto di tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="35adf-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="35adf-115">Espandere **Visual c#**, quindi selezionare **Windows** nel riquadro a sinistra di hello hello.</span><span class="sxs-lookup"><span data-stu-id="35adf-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="35adf-116">Fare clic su **applicazione Console** nel riquadro centrale hello.</span><span class="sxs-lookup"><span data-stu-id="35adf-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="35adf-117">Assegnare un nome al progetto e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="35adf-117">Name your project, then click **OK**.</span></span>  

![Nuovo progetto](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="35adf-119">Il progetto verrà toouse alcune librerie di Azure contenuti nei pacchetti di Nuget.</span><span class="sxs-lookup"><span data-stu-id="35adf-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="35adf-120">Aggiungere tali progetto toohello.</span><span class="sxs-lookup"><span data-stu-id="35adf-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="35adf-121">Fare clic su hello **strumenti** menu **Gestione pacchetti Nuget**, quindi **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="35adf-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Gestisci pacchetti NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="35adf-123">Nella Console di gestione pacchetti hello, eseguire hello successivo comando tooinstall hello **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="35adf-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="35adf-124">Eseguire hello seguente hello tooinstall **libreria di gestione della rete CDN di Azure**:</span><span class="sxs-lookup"><span data-stu-id="35adf-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="35adf-125">Direttive, costanti, metodo main e metodi helper</span><span class="sxs-lookup"><span data-stu-id="35adf-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="35adf-126">Possiamo procedere alla struttura di base di questo programma scritto hello.</span><span class="sxs-lookup"><span data-stu-id="35adf-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="35adf-127">Nella scheda Program.cs hello, sostituire hello `using` direttive all'inizio di hello con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="35adf-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
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
2. <span data-ttu-id="35adf-128">È necessario toodefine alcune costanti che utilizzeranno i metodi.</span><span class="sxs-lookup"><span data-stu-id="35adf-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="35adf-129">In hello `Program` (classe), ma prima dell'esecuzione hello `Main` metodo, aggiungere il seguente hello.</span><span class="sxs-lookup"><span data-stu-id="35adf-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="35adf-130">Essere tooreplace che segnaposto hello, tra cui hello  **&lt;angolari&gt;**, con valori personalizzati in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="35adf-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="35adf-131">Anche a livello di classe hello, definire queste due variabili.</span><span class="sxs-lookup"><span data-stu-id="35adf-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="35adf-132">Useremo queste toodetermine successive se il profilo e l'endpoint esiste già.</span><span class="sxs-lookup"><span data-stu-id="35adf-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="35adf-133">Sostituire hello `Main` metodo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="35adf-133">Replace hello `Main` method as follows:</span></span>
   
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
5. <span data-ttu-id="35adf-134">Alcuni dei nostri altri metodi sta utente hello tooprompt con domande "Sì/No".</span><span class="sxs-lookup"><span data-stu-id="35adf-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="35adf-135">Aggiungere hello toomake metodo dopo che un po' più semplice:</span><span class="sxs-lookup"><span data-stu-id="35adf-135">Add hello following method toomake that a little easier:</span></span>
   
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

<span data-ttu-id="35adf-136">Struttura di base hello di questo programma è stato scritto, si dovrebbe creare metodi hello chiamati da hello `Main` metodo.</span><span class="sxs-lookup"><span data-stu-id="35adf-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="35adf-137">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="35adf-137">Authentication</span></span>
<span data-ttu-id="35adf-138">Prima di utilizzare hello libreria di gestione della rete CDN di Azure, è necessario dell'entità servizio tooauthenticate e ottenere un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="35adf-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="35adf-139">Questo metodo Usa token hello tooretrieve ADAL.</span><span class="sxs-lookup"><span data-stu-id="35adf-139">This method uses ADAL tooretrieve hello token.</span></span>

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

<span data-ttu-id="35adf-140">Se si utilizza l'autenticazione utente, hello `GetAccessToken` metodo avrà un aspetto leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="35adf-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="35adf-141">Usare questo esempio di codice solo se si sceglie l'autenticazione utente toohave anziché un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="35adf-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="35adf-142">Tooreplace assicurarsi di essere `<redirect URI>` con hello URI di reindirizzamento di immesso al momento della registrazione di un'applicazione hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35adf-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="35adf-143">Elencare i profili e gli endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="35adf-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="35adf-144">Si è pronti tooperform operazioni di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="35adf-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="35adf-145">Hello prima cosa il metodo è l'elenco di tutti i profili di hello e gli endpoint in questo gruppo di risorse e se viene trovata una corrispondenza per i nomi di endpoint e profilo di hello specificato nel nostro costanti, annota che per un momento successivo, in modo non si eseguono tentativi toocreate duplicati.</span><span class="sxs-lookup"><span data-stu-id="35adf-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="35adf-146">Creare profili ed endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="35adf-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="35adf-147">Ora si creerà un profilo.</span><span class="sxs-lookup"><span data-stu-id="35adf-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="35adf-148">Una volta creato il profilo di hello, verrà creato un endpoint.</span><span class="sxs-lookup"><span data-stu-id="35adf-148">Once hello profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="35adf-149">esempio Hello precedente assegna endpoint hello un'entità origin denominata *Contoso* con un nome host `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="35adf-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="35adf-150">È necessario modificare questo toopoint tooyour personalizzate del nome host dell'origine.</span><span class="sxs-lookup"><span data-stu-id="35adf-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="35adf-151">Ripulire un endpoint</span><span class="sxs-lookup"><span data-stu-id="35adf-151">Purge an endpoint</span></span>
<span data-ttu-id="35adf-152">Supponendo che l'endpoint di hello è stato creato, un'attività comune che si voglia tooperform in questo programma è eliminazione contenuto hello in questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="35adf-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

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
> <span data-ttu-id="35adf-153">Nell'esempio hello sopra, hello stringa `/*` indica che desidera toopurge tutti gli elementi nella directory radice del percorso dell'endpoint hello hello.</span><span class="sxs-lookup"><span data-stu-id="35adf-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="35adf-154">Questo è l'equivalente toochecking **ripulire tutti** in hello Azure portal "Elimina" finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="35adf-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="35adf-155">In hello `CreateCdnProfile` metodo, creato il profilo come un **rete CDN di Azure da Verizon** profilo mediante il codice hello `Sku = new Sku(SkuName.StandardVerizon)`, in modo che sia corretta.</span><span class="sxs-lookup"><span data-stu-id="35adf-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="35adf-156">Tuttavia, **rete CDN di Azure da Akamai** non supportano i profili **ripulire tutti**, pertanto se si è dato dal fatto utilizzando un profilo di Akamai per questa esercitazione, è necessario tooinclude percorsi specifici toopurge.</span><span class="sxs-lookup"><span data-stu-id="35adf-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="35adf-157">Eliminare profili ed endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="35adf-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="35adf-158">metodi ultimo Hello eliminerà l'endpoint e un profilo.</span><span class="sxs-lookup"><span data-stu-id="35adf-158">hello last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="35adf-159">Programma hello in esecuzione</span><span class="sxs-lookup"><span data-stu-id="35adf-159">Running hello program</span></span>
<span data-ttu-id="35adf-160">Ora possiamo compilare ed eseguire il programma di hello facendo hello **avviare** pulsante in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35adf-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![Il programma in esecuzione](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="35adf-162">Quando il programma hello raggiunge hello sopra prompt dei comandi, dovrebbero essere in grado di tooreturn tooyour risorse gruppo hello portale di Azure e che sia stato creato il profilo di hello.</span><span class="sxs-lookup"><span data-stu-id="35adf-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![Completamento della procedura](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="35adf-164">È quindi possibile verificare hello richieste toorun hello resto del programma hello.</span><span class="sxs-lookup"><span data-stu-id="35adf-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![Il completamento del programma](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="35adf-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35adf-166">Next Steps</span></span>
<span data-ttu-id="35adf-167">il progetto completato hello toosee da questa procedura dettagliata, [scaricare l'esempio hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="35adf-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="35adf-168">documentazione aggiuntiva toofind su hello libreria di gestione della rete CDN di Azure per .NET, hello vista [reference sul sito MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="35adf-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="35adf-169">Gestire le risorse della rete CDN con [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="35adf-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

