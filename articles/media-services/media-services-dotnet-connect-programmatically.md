---
title: Connessione a un account di Servizi multimediali mediante .NET
description: Questo argomento illustra come connettersi a Servizi multimediali mediante .NET.
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 892932116934952265a21ab17aac3434b5760136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="6446a-103">Connessione a un account di Servizi multimediali mediante l'SDK di Servizi multimediali per .NET</span><span class="sxs-lookup"><span data-stu-id="6446a-103">Connecting to Media Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6446a-104">REST</span><span class="sxs-lookup"><span data-stu-id="6446a-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="6446a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="6446a-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="6446a-106">Questo argomento descrive come ottenere una connessione a Servizi multimediali di Microsoft Azure a livello di codice quando si programma con Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="6446a-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span></span>

## <a name="connecting-to-media-services"></a><span data-ttu-id="6446a-107">Connessione a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="6446a-107">Connecting to Media Services</span></span>
<span data-ttu-id="6446a-108">Prima di connettersi a Servizi multimediali a livello di codice, è necessario impostare un account Azure, configurare Servizi multimediali su tale account e quindi definire un progetto di Visual Studio per lo sviluppo con l'SDK di Servizi multimediali per .NET.</span><span class="sxs-lookup"><span data-stu-id="6446a-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span></span> <span data-ttu-id="6446a-109">Per altre informazioni, vedere Configurazione per lo sviluppo con l'SDK di Servizi multimediali per .NET.</span><span class="sxs-lookup"><span data-stu-id="6446a-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span></span>

<span data-ttu-id="6446a-110">Al termine del processo di configurazione dell'account di Servizi multimediali, l'utente ottiene i seguenti valori di connessione obbligatori,</span><span class="sxs-lookup"><span data-stu-id="6446a-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span></span> <span data-ttu-id="6446a-111">che può usare per configurare connessioni a Servizi multimediali a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="6446a-111">Use these to make programmatic connections to Media Services.</span></span>

* <span data-ttu-id="6446a-112">Nome dell'account di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="6446a-112">Your Media Services account name.</span></span>
* <span data-ttu-id="6446a-113">Chiave dell'account di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="6446a-113">Your Media Services account key.</span></span>

<span data-ttu-id="6446a-114">Per trovare questi valori, passare al portale di gestione di Azure, selezionare l'account di Servizi multimediali e fare clic sull'icona "**GESTISCI CHIAVI**" nella parte inferiore della finestra del portale.</span><span class="sxs-lookup"><span data-stu-id="6446a-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span></span> <span data-ttu-id="6446a-115">Facendo clic sull'icona accanto a ciascuna casella di testo, il valore viene copiato negli Appunti di sistema.</span><span class="sxs-lookup"><span data-stu-id="6446a-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="6446a-116">Creazione di un'istanza di CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="6446a-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="6446a-117">Prima di iniziare la programmazione basata su Servizi multimediali, è necessario creare un'istanza di **CloudMediaContext** che rappresenta il contesto del server.</span><span class="sxs-lookup"><span data-stu-id="6446a-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="6446a-118">**CloudMediaContext** contiene riferimenti a raccolte importanti composte da processi, asset, file, criteri di accesso e localizzatori.</span><span class="sxs-lookup"><span data-stu-id="6446a-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="6446a-119">La classe **CloudMediaContext** non è di tipo thread-safe.</span><span class="sxs-lookup"><span data-stu-id="6446a-119">The **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="6446a-120">È quindi necessario creare una nuova istanza di CloudMediaContext per ogni thread o set di operazioni.</span><span class="sxs-lookup"><span data-stu-id="6446a-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="6446a-121">CloudMediaContext include cinque overload del costruttore.</span><span class="sxs-lookup"><span data-stu-id="6446a-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="6446a-122">Si consiglia di usare costruttori che accettano **MediaServicesCredentials** come parametro.</span><span class="sxs-lookup"><span data-stu-id="6446a-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="6446a-123">Per altre informazioni, vedere la sezione **Riutilizzo dei token del Servizio di controllo di accesso** seguente.</span><span class="sxs-lookup"><span data-stu-id="6446a-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="6446a-124">Nel seguente esempio viene usato il costruttore pubblico CloudMediaContext(MediaServicesCredentials credentials):</span><span class="sxs-lookup"><span data-stu-id="6446a-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="6446a-125">Riutilizzo dei token del Servizio di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="6446a-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="6446a-126">Questa sezione mostra come riutilizzare i token del Servizio di controllo di accesso mediante i costruttori CloudMediaContext che accettano MediaServicesCredentials come parametro.</span><span class="sxs-lookup"><span data-stu-id="6446a-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="6446a-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (noto anche come Servizio di controllo di accesso o ACS) è un servizio basato sul cloud che offre un modo semplice per autenticare e autorizzare gli utenti, in modo che possano accedere alle applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="6446a-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span></span> <span data-ttu-id="6446a-128">Servizi multimediali di Microsoft Azure controlla l'accesso ai servizi tramite il protocollo OAuth che richiede un token ACS.</span><span class="sxs-lookup"><span data-stu-id="6446a-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="6446a-129">Servizi multimediali riceve i token ACS da un server di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="6446a-129">Media Services receives the ACS tokens from an authorization server.</span></span>

<span data-ttu-id="6446a-130">Quando si sviluppa usando l'SDK di Servizi multimediali, è possibile scegliere di non gestire i token, poiché questi vengono gestiti automaticamente dal codice dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="6446a-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span></span> <span data-ttu-id="6446a-131">Tuttavia, se si lascia all'SDK la gestione completa dei token ACS, possono verificarsi richieste di token non necessarie.</span><span class="sxs-lookup"><span data-stu-id="6446a-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span></span> <span data-ttu-id="6446a-132">Le richieste di token richiedono tempo e utilizzano le risorse di client e server.</span><span class="sxs-lookup"><span data-stu-id="6446a-132">Requesting tokens takes time and consumes the client and server resources.</span></span> <span data-ttu-id="6446a-133">Inoltre, il server ACS limita le richieste in caso di velocità eccessiva.</span><span class="sxs-lookup"><span data-stu-id="6446a-133">Also, the ACS server throttles the requests if the rate is too high.</span></span> <span data-ttu-id="6446a-134">Il limite è di 30 richieste al secondo. Per informazioni dettagliate, vedere [Limitazioni del servizio ACS](https://msdn.microsoft.com/library/gg185909.aspx).</span><span class="sxs-lookup"><span data-stu-id="6446a-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="6446a-135">A partire dalla versione 3.0.0.0 dell'SDK di Servizi multimediali, è possibile riutilizzare i token ACS.</span><span class="sxs-lookup"><span data-stu-id="6446a-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span></span> <span data-ttu-id="6446a-136">I costruttori **CloudMediaContext**, che accettano **MediaServicesCredentials** come parametro, consentono di condividere i token ACS tra più contesti.</span><span class="sxs-lookup"><span data-stu-id="6446a-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span></span> <span data-ttu-id="6446a-137">La classe MediaServicesCredentials incapsula le credenziali di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="6446a-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span></span> <span data-ttu-id="6446a-138">Se è disponibile un token e la data di scadenza è nota, è possibile creare una nuova istanza di MediaServicesCredentials con il token e passarla al costruttore di CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="6446a-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span></span> <span data-ttu-id="6446a-139">Si noti che l'SDK di Servizi multimediali aggiorna automaticamente i token ogni volta che scadono.</span><span class="sxs-lookup"><span data-stu-id="6446a-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="6446a-140">Per riutilizzare i token ACS sono disponibili i due modi illustrati nei seguenti esempi.</span><span class="sxs-lookup"><span data-stu-id="6446a-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span></span>

* <span data-ttu-id="6446a-141">È possibile memorizzare l'oggetto **MediaServicesCredentials** nella cache, ad esempio in una variabile di classe statica,</span><span class="sxs-lookup"><span data-stu-id="6446a-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="6446a-142">e quindi passare l'oggetto memorizzato nella cache al costruttore CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="6446a-142">Then, pass the cached object to the CloudMediaContext constructor.</span></span> <span data-ttu-id="6446a-143">L'oggetto MediaServicesCredentials contiene un token ACS che, se ancora valido, può essere riutilizzato.</span><span class="sxs-lookup"><span data-stu-id="6446a-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="6446a-144">Se il token non è più valido, verrà aggiornato dall'SDK di Servizi multimediali usando le credenziali fornite al costruttore MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="6446a-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="6446a-145">Si noti che l'oggetto **MediaServicesCredentials** ottiene un token valido dopo la chiamata a RefreshToken.</span><span class="sxs-lookup"><span data-stu-id="6446a-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span></span> <span data-ttu-id="6446a-146">**CloudMediaContext** chiama il metodo **RefreshToken** nel costruttore.</span><span class="sxs-lookup"><span data-stu-id="6446a-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span></span> <span data-ttu-id="6446a-147">Se si prevede di salvare i valori dei token in una risorsa di archiviazione esterna, assicurarsi che il valore di TokenExpiration sia ancora valido prima di salvare i dati del token.</span><span class="sxs-lookup"><span data-stu-id="6446a-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span></span> <span data-ttu-id="6446a-148">Se non è valido, chiamare RefreshToken prima di procedere alla memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="6446a-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="6446a-149">È anche possibile memorizzare nella cache la stringa AccessToken e i valori TokenExpiration.</span><span class="sxs-lookup"><span data-stu-id="6446a-149">You can also cache the AccessToken string and the TokenExpiration values.</span></span> <span data-ttu-id="6446a-150">I valori possono essere usati successivamente per creare un nuovo oggetto MediaServicesCredentials con i dati del token memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="6446a-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span></span>  <span data-ttu-id="6446a-151">Ciò è particolarmente utile in scenari in cui il token può essere condiviso in modo sicuro tra più processi o computer.</span><span class="sxs-lookup"><span data-stu-id="6446a-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="6446a-152">I seguenti frammenti di codice chiamano i metodi SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage e UpdateTokenDataInExternalStorageIfNeeded che non sono definiti in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="6446a-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="6446a-153">È possibile definire questi metodi per archiviare, recuperare e aggiornare i dati del token in una risorsa di archiviazione esterna.</span><span class="sxs-lookup"><span data-stu-id="6446a-153">You could define these methods to store, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="6446a-154">Usare i valori del token per creare MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="6446a-154">Use the saved token values to create MediaServicesCredentials.</span></span>

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    <span data-ttu-id="6446a-155">Aggiornare la copia del token, nel caso in cui il token sia stato aggiornato dall'SDK di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="6446a-155">Update the token copy in case the token was updated by the Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="6446a-156">Se sono presenti più account di Servizi multimediali, ad esempio per la condivisione del carico o la distribuzione geografica, è possibile memorizzare nella cache gli oggetti MediaServicesCredentials tramite la raccolta System.Collections.Concurrent.ConcurrentDictionary, una raccolta thread-safe di coppie chiave/valore a cui possono accedere simultaneamente più thread.</span><span class="sxs-lookup"><span data-stu-id="6446a-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="6446a-157">È quindi possibile usare il metodo GetOrAdd per ottenere le credenziali memorizzate nella cache.</span><span class="sxs-lookup"><span data-stu-id="6446a-157">You can then use the GetOrAdd method to get the cached credentials.</span></span> 
  
        // Declare a static class variable of the ConcurrentDictionary type in which the Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials to create a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a><span data-ttu-id="6446a-158">Connessione a un account di Servizi multimediali in Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="6446a-158">Connecting to a Media Services account located in the North China region</span></span>
<span data-ttu-id="6446a-159">Se il proprio account si trova in Cine settentrionale, usare il seguente costruttore:</span><span class="sxs-lookup"><span data-stu-id="6446a-159">If your account is located in the North China region, use the following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="6446a-160">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6446a-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="6446a-161">Archiviazione dei valori di connessione nella configurazione</span><span class="sxs-lookup"><span data-stu-id="6446a-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="6446a-162">È consigliabile archiviare i valori di connessione, in particolare quelli sensibili come nome account e password, all'interno della configurazione,</span><span class="sxs-lookup"><span data-stu-id="6446a-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="6446a-163">e anche crittografare i dati di configurazione sensibili.</span><span class="sxs-lookup"><span data-stu-id="6446a-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span></span> <span data-ttu-id="6446a-164">È possibile crittografare l'intero file di configurazione tramite il sistema EFS (Encrypting File System) di Windows.</span><span class="sxs-lookup"><span data-stu-id="6446a-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="6446a-165">Per abilitare il sistema EFS per un file, fare clic con il pulsante destro del mouse sul file, scegliere **Proprietà** e abilitare la crittografia nella scheda delle impostazioni **Avanzate**.</span><span class="sxs-lookup"><span data-stu-id="6446a-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab.</span></span> <span data-ttu-id="6446a-166">In alternativa, è possibile creare una soluzione personalizzata per crittografare parti selezionate di un file di configurazione tramite la configurazione protetta.</span><span class="sxs-lookup"><span data-stu-id="6446a-166">Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="6446a-167">Vedere l'argomento relativo alla [crittografia delle informazioni di configurazione usando la configurazione protetta](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="6446a-167">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="6446a-168">Il file App.config contiene i valori di configurazione necessari.</span><span class="sxs-lookup"><span data-stu-id="6446a-168">The following App.config file contains the required connection values.</span></span> <span data-ttu-id="6446a-169">I valori nell'elemento <appSettings> sono i valori necessari ottenuti durante il processo di configurazione dell'account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="6446a-169">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="6446a-170">Per recuperare i valori di connessione dalla configurazione, è possibile usare la classe **ConfigurationManager** e quindi assegnare i valori ai campi nel codice:</span><span class="sxs-lookup"><span data-stu-id="6446a-170">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="6446a-171">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="6446a-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6446a-172">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="6446a-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

