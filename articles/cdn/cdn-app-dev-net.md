---
title: Introduzione ad Azure CDN Library per .NET | Microsoft Docs
description: Informazioni su come scrivere applicazioni .NET per la gestione della rete CDN di Azure tramite Visual Studio.
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
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="23e46-103">Introduzione allo sviluppo della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="23e46-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23e46-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="23e46-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="23e46-105">.NET</span><span class="sxs-lookup"><span data-stu-id="23e46-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="23e46-106">È possibile usare la [libreria CDN di Azure per .NET](https://msdn.microsoft.com/library/mt657769.aspx) per automatizzare la creazione e la gestione di profili ed endpoint di una rete CDN.</span><span class="sxs-lookup"><span data-stu-id="23e46-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="23e46-107">Questa esercitazione illustra in dettaglio la creazione di una semplice applicazione console .NET che dimostra varie operazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="23e46-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="23e46-108">Lo scopo di questa esercitazione non è descrivere dettagliatamente tutti gli aspetti della libreria CDN di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="23e46-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="23e46-109">Per completare questa esercitazione, è necessario Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="23e46-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="23e46-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) è disponibile gratuitamente per il download.</span><span class="sxs-lookup"><span data-stu-id="23e46-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="23e46-111">Il [progetto completato di questa esercitazione](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) è disponibile per il download in MSDN.</span><span class="sxs-lookup"><span data-stu-id="23e46-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="23e46-112">Creare il progetto e aggiungere i pacchetti Nuget</span><span class="sxs-lookup"><span data-stu-id="23e46-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="23e46-113">Ora che abbiamo creato un gruppo di risorse per i profili di rete CDN e assegnato all'applicazione Azure AD l'autorizzazione per gestire i profili e gli endpoint della rete CDN all'interno del gruppo, è possibile iniziare a creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="23e46-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="23e46-114">Da Visual Studio 2015 fare clic su **File**, **Nuovo**, **Progetto** per aprire la finestra di dialogo del nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="23e46-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="23e46-115">Espandere **Visual C#** e selezionare **Windows** nel riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="23e46-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="23e46-116">Fare clic su **Applicazione console** nel riquadro centrale.</span><span class="sxs-lookup"><span data-stu-id="23e46-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="23e46-117">Assegnare un nome al progetto e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="23e46-117">Name your project, then click **OK**.</span></span>  

![Nuovo progetto](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="23e46-119">Il progetto userà alcune librerie di Azure contenute nei pacchetti Nuget.</span><span class="sxs-lookup"><span data-stu-id="23e46-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="23e46-120">Ora si aggiungeranno al progetto.</span><span class="sxs-lookup"><span data-stu-id="23e46-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="23e46-121">Scegliere **Gestione pacchetti NuGet** dal menu **Strumenti** e fare clic su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="23e46-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Gestisci pacchetti NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="23e46-123">Nella Console di Gestione pacchetti eseguire il comando seguente per installare **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="23e46-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="23e46-124">Eseguire il codice seguente per installare **Azure CDN Management Library**:</span><span class="sxs-lookup"><span data-stu-id="23e46-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="23e46-125">Direttive, costanti, metodo main e metodi helper</span><span class="sxs-lookup"><span data-stu-id="23e46-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="23e46-126">Ora si scriverà la struttura di base del programma.</span><span class="sxs-lookup"><span data-stu-id="23e46-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="23e46-127">Nella scheda Program.cs sostituire la direttiva `using` all'inizio con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="23e46-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
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
2. <span data-ttu-id="23e46-128">È necessario definire alcune costanti che i metodi useranno.</span><span class="sxs-lookup"><span data-stu-id="23e46-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="23e46-129">Nella classe `Program`, ma prima del metodo `Main`, aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="23e46-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="23e46-130">Sostituire i segnaposto, incluse le **&lt;parentesi acute&gt;**, con i valori necessari.</span><span class="sxs-lookup"><span data-stu-id="23e46-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="23e46-131">Sempre a livello della classe, definire queste due variabili.</span><span class="sxs-lookup"><span data-stu-id="23e46-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="23e46-132">Saranno usate in un secondo momento per determinare se il profilo e l'endpoint esistono già.</span><span class="sxs-lookup"><span data-stu-id="23e46-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="23e46-133">Sostituire il metodo `Main` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="23e46-133">Replace the `Main` method as follows:</span></span>
   
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
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="23e46-134">Altri metodi che si useranno presenteranno all'utente domande "Sì/No".</span><span class="sxs-lookup"><span data-stu-id="23e46-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="23e46-135">Aggiungere il metodo seguente per facilitare l'operazione:</span><span class="sxs-lookup"><span data-stu-id="23e46-135">Add the following method to make that a little easier:</span></span>
   
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

<span data-ttu-id="23e46-136">Ora che la struttura di base del programma è stata scritta, è necessario creare i metodi chiamati dal metodo `Main` .</span><span class="sxs-lookup"><span data-stu-id="23e46-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="23e46-137">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="23e46-137">Authentication</span></span>
<span data-ttu-id="23e46-138">Per poter usare Azure CDN Management Library, è necessario autenticare l'entità servizio e ottenere un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="23e46-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="23e46-139">Questo metodo usa ADAL per recuperare il token.</span><span class="sxs-lookup"><span data-stu-id="23e46-139">This method uses ADAL to retrieve the token.</span></span>

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

<span data-ttu-id="23e46-140">Se si usa l'autenticazione del singolo utente, il metodo `GetAccessToken` avrà un aspetto leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="23e46-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23e46-141">Usare questo esempio di codice solo se si sceglie l'autenticazione interattiva del singolo utente anziché un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="23e46-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="23e46-142">Assicurarsi di sostituire `<redirect URI>` con l'URI di reindirizzamento inserito al momento della registrazione dell'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23e46-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="23e46-143">Elencare i profili e gli endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="23e46-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="23e46-144">Ora tutto è pronto per eseguire le operazioni della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="23e46-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="23e46-145">La prima cosa che il metodo fa è elencare tutti i profili e gli endpoint nel gruppo di risorse e, se trova una corrispondenza per i nomi di profilo e di endpoint specificati nelle costanti, ne tiene conto per un momento successivo in modo da evitare tentativi di creazione di duplicati.</span><span class="sxs-lookup"><span data-stu-id="23e46-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="23e46-146">Creare profili ed endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="23e46-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="23e46-147">Ora si creerà un profilo.</span><span class="sxs-lookup"><span data-stu-id="23e46-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="23e46-148">Dopo il profilo, verrà creato un endpoint.</span><span class="sxs-lookup"><span data-stu-id="23e46-148">Once the profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="23e46-149">L'esempio precedente assegna all'endpoint un'origine denominata *Contoso* con il nome host `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="23e46-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="23e46-150">È necessario modificarlo in modo che punti al nome host dell'origine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="23e46-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="23e46-151">Ripulire un endpoint</span><span class="sxs-lookup"><span data-stu-id="23e46-151">Purge an endpoint</span></span>
<span data-ttu-id="23e46-152">Supponendo che l'endpoint sia stato creato, un'attività comune che potrebbe essere necessario eseguire nel programma è ripulire il contenuto dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="23e46-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

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
> <span data-ttu-id="23e46-153">Nell'esempio precedente la stringa `/*` indica che si vuole ripulire tutto il contenuto della radice del percorso dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="23e46-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="23e46-154">Ciò equivale a selezionare **Elimina tutti** nella finestra di dialogo "Elimina" del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="23e46-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="23e46-155">Nel metodo `CreateCdnProfile` è stato creato il profilo come profilo **Rete CDN di Azure da Verizon** usando il codice `Sku = new Sku(SkuName.StandardVerizon)`, perciò l'operazione avrà esito positivo.</span><span class="sxs-lookup"><span data-stu-id="23e46-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="23e46-156">I profili **Rete CDN Azure da Akamai** tuttavia non supportano **Elimina tutti**, perciò se si usasse un profilo Akamai per questa esercitazione si dovrebbero includere percorsi specifici da ripulire.</span><span class="sxs-lookup"><span data-stu-id="23e46-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="23e46-157">Eliminare profili ed endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="23e46-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="23e46-158">Gli ultimi metodi consentiranno di eliminare l'endpoint e il profilo.</span><span class="sxs-lookup"><span data-stu-id="23e46-158">The last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="23e46-159">Esecuzione del programma</span><span class="sxs-lookup"><span data-stu-id="23e46-159">Running the program</span></span>
<span data-ttu-id="23e46-160">È ora possibile compilare ed eseguire il programma facendo clic sul pulsante **Avvia** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23e46-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![Il programma in esecuzione](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="23e46-162">Quando il programma raggiunge la richiesta precedente, sarà possibile ritornare al gruppo di risorse nel portale di Azure e verificare che il profilo sia stato creato.</span><span class="sxs-lookup"><span data-stu-id="23e46-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![Completamento della procedura](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="23e46-164">È quindi possibile confermare le richieste per eseguire il resto del programma.</span><span class="sxs-lookup"><span data-stu-id="23e46-164">We can then confirm the prompts to run the rest of the program.</span></span>

![Il completamento del programma](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="23e46-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23e46-166">Next Steps</span></span>
<span data-ttu-id="23e46-167">Per vedere il progetto completato di questa procedura dettagliata, [scaricare l'esempio](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="23e46-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="23e46-168">Per altra documentazione su Azure CDN Management Library per .NET, vedere i [riferimenti su MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="23e46-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="23e46-169">Gestire le risorse della rete CDN con [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="23e46-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

