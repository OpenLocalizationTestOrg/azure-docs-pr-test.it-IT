---
title: aaaConnecting tooMedia servizi Account usando .NET
description: Questo argomento viene illustrato come tooconnect tooMedia servizi abbonamento .NET.
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
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="1c6bc-103">Connessione tooMedia Account Services con Media Services SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="1c6bc-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c6bc-104">REST</span><span class="sxs-lookup"><span data-stu-id="1c6bc-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="1c6bc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1c6bc-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="1c6bc-106">In questo argomento viene descritto come tooobtain tooMicrosoft una connessione a livello di codice servizi multimediali di Azure quando si programma con hello Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="1c6bc-107">La connessione di servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="1c6bc-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="1c6bc-108">tooconnect tooMedia servizi a livello di codice, è necessario avere già configurato un account Azure, configurato servizi multimediali nell'account e quindi configurare un progetto di Visual Studio per lo sviluppo con hello Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="1c6bc-109">Per ulteriori informazioni, vedere il programma di installazione per lo sviluppo con hello Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="1c6bc-110">Alla fine di hello del processo di installazione di account servizi multimediali hello, ottenuto seguente hello necessari valori di connessione.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="1c6bc-111">Utilizzare queste connessioni a livello di codice toomake tooMedia servizi.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="1c6bc-112">Nome dell'account di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1c6bc-112">Your Media Services account name.</span></span>
* <span data-ttu-id="1c6bc-113">Chiave dell'account di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1c6bc-113">Your Media Services account key.</span></span>

<span data-ttu-id="1c6bc-114">toofind questi valori, visitare il portale di gestione di Azure toohello, selezionare l'account del servizio di supporto e fare clic su hello "**GESTISCI CHIAVI**" sull'icona nella parte inferiore di hello della finestra portale hello.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="1c6bc-115">Facendo clic su hello icona Avanti tooeach testo casella copie hello valore toohello Appunti di sistema.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="1c6bc-116">Creazione di un'istanza di CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="1c6bc-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="1c6bc-117">programmazione con Media Services è necessario toocreate toostart un **CloudMediaContext** istanza che rappresenta il contesto di server hello.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="1c6bc-118">Hello **CloudMediaContext** include riferimenti tooimportant insiemi inclusi i processi, asset, file, i criteri di accesso e localizzatori.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="1c6bc-119">Hello **CloudMediaContext** classe non è thread-safe.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="1c6bc-120">È quindi necessario creare una nuova istanza di CloudMediaContext per ogni thread o set di operazioni.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="1c6bc-121">CloudMediaContext include cinque overload del costruttore.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="1c6bc-122">È consigliato toouse costruttori che accettano **MediaServicesCredentials** come parametro.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="1c6bc-123">Per ulteriori informazioni, vedere hello **riutilizzo dei token del servizio controllo di accesso** che segue.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="1c6bc-124">Hello esempio seguente viene utilizzato un costruttore pubblico CloudMediaContext(MediaServicesCredentials credentials) hello:</span><span class="sxs-lookup"><span data-stu-id="1c6bc-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="1c6bc-125">Riutilizzo dei token del Servizio di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="1c6bc-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="1c6bc-126">In questa sezione viene illustrato come tooreuse Access Control Service token usando CloudMediaContext costruttori che accettano MediaServicesCredentials come parametro.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="1c6bc-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (noto anche come servizio di controllo di accesso o ACS) è un servizio basato su cloud che fornisce un modo semplice di autenticazione e autorizzazione accesso toogain utenti tootheir le applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="1c6bc-128">Servizi multimediali di Microsoft Azure controlla l'accesso tooits servizi tramite il protocollo OAuth che richiede un token ACS.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="1c6bc-129">Servizi multimediali riceve i token ACS hello da un server di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="1c6bc-130">Quando si sviluppa con hello Media Services SDK, è possibile scegliere gestiscono toonot token hello perché hello Gestioni codice SDK per è.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="1c6bc-131">Tuttavia, consentendo agli sviluppatori di hello SDK gestire completamente le richieste di token ACS hello token lead toounnecessary.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="1c6bc-132">Le richieste di token richiede tempo e utilizza risorse di hello client e server.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="1c6bc-133">Inoltre, server ACS hello limita le richieste di hello se frequenza hello è troppo alto.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="1c6bc-134">limite di Hello è di 30 richieste al secondo, vedere [limitazioni del servizio ACS](https://msdn.microsoft.com/library/gg185909.aspx) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="1c6bc-135">A partire da Media Services SDK versione 3.0.0.0 hello, è possibile riutilizzare i token ACS hello.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="1c6bc-136">Hello **CloudMediaContext** costruttori che accettano **MediaServicesCredentials** come parametro consentono di token ACS hello condivisione tra più contesti.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="1c6bc-137">Hello MediaServicesCredentials classe incapsula le credenziali di servizi multimediali di hello.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="1c6bc-138">Se è disponibile un token ACS e l'ora di scadenza è noto, è possibile creare una nuova istanza di MediaServicesCredentials con token hello e passarlo come costruttore toohello di CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="1c6bc-139">Si noti che hello Media Services SDK Aggiorna automaticamente i token ogni volta che scadono.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="1c6bc-140">Esistono due modi i token ACS tooreuse, come illustrato nell'esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="1c6bc-141">È possibile memorizzare nella cache di hello **MediaServicesCredentials** oggetto in memoria (ad esempio, una variabile di classe statici).</span><span class="sxs-lookup"><span data-stu-id="1c6bc-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="1c6bc-142">Quindi, passare costruttore CloudMediaContext toohello dell'oggetto memorizzato nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="1c6bc-143">oggetto MediaServicesCredentials Hello contiene un token ACS che può essere riutilizzato se è ancora valido.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="1c6bc-144">Se il token di hello non è valido, che verrà aggiornato da hello toohello MediaServicesCredentials costruttore utilizzando le credenziali di hello Media Services SDK.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="1c6bc-145">Si noti che hello **MediaServicesCredentials** oggetto Ottiene un token valido dopo hello RefreshToken viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="1c6bc-146">Hello **CloudMediaContext** hello chiamate **RefreshToken** metodo hello costruttore.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="1c6bc-147">Se si prevede di archiviazione esterna tooan toosave hello i valori del token, prendere toocheck che hello TokenExpiration valore sia valido prima di salvare i dati del token hello.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="1c6bc-148">Se non è valido, chiamare RefreshToken prima di procedere alla memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="1c6bc-149">È inoltre possibile memorizzare nella cache hello AccessToken valori stringa e hello TokenExpiration.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="1c6bc-150">i valori Hello in un secondo momento potrebbe essere utilizzato toocreate MediaServicesCredentials un nuovo oggetto con i dati memorizzati nella cache di hello del token.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="1c6bc-151">Ciò è particolarmente utile per scenari in cui il token hello può essere condiviso in modo sicuro tra più processi o computer.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="1c6bc-152">Hello frammenti di codice seguente chiamano hello metodi SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage e UpdateTokenDataInExternalStorageIfNeeded non definiti in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="1c6bc-153">È possibile definire questi metodi toostore, recuperare e aggiornare i dati token in un archivio esterno.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="1c6bc-154">Utilizzare hello salvata token valori toocreate MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="1c6bc-155">Aggiornare copia token hello nel caso in cui il token hello è stato aggiornato da Media Services SDK hello.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="1c6bc-156">Se si hanno più account di servizi multimediali (ad esempio, per la condivisione del carico o Geo-distribuzione) è possibile memorizzare nella cache oggetti MediaServicesCredentials utilizzo hello System.Collections.Concurrent.ConcurrentDictionary insieme (Buongiorno Raccolta di ConcurrentDictionary rappresenta una raccolta thread-safe di coppie chiave/valore che è possibile accedere contemporaneamente da più thread).</span><span class="sxs-lookup"><span data-stu-id="1c6bc-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="1c6bc-157">È quindi possibile utilizzare le credenziali memorizzate nella cache di hello tooget di hello GetOrAdd (metodo).</span><span class="sxs-lookup"><span data-stu-id="1c6bc-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="1c6bc-158">La connessione di account di servizi multimediali tooa si trova nell'area di hello Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="1c6bc-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="1c6bc-159">Se l'account si trova nell'area di hello Cina settentrionale, usare hello costruttore seguente:</span><span class="sxs-lookup"><span data-stu-id="1c6bc-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="1c6bc-160">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1c6bc-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="1c6bc-161">Archiviazione dei valori di connessione nella configurazione</span><span class="sxs-lookup"><span data-stu-id="1c6bc-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="1c6bc-162">È un consigliabile toostore connessione valori, particolarmente sensibili, ad esempio il nome dell'account e la password, nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="1c6bc-163">Inoltre, si tratta di dati di configurazione sensibili tooencrypt una procedura consigliata.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="1c6bc-164">È possibile crittografare hello intero file di configurazione utilizzando hello Windows Encrypting File System (EFS).</span><span class="sxs-lookup"><span data-stu-id="1c6bc-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="1c6bc-165">Selezionare tooenable EFS in un file, il pulsante destro del mouse hello file **proprietà**e abilitare la crittografia in hello **avanzate** scheda Impostazioni. In alternativa, è possibile creare una soluzione personalizzata per crittografare parti selezionate di un file di configurazione tramite la configurazione protetta.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="1c6bc-166">Vedere l'argomento relativo alla [crittografia delle informazioni di configurazione usando la configurazione protetta](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c6bc-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="1c6bc-167">Hello seguenti il file app. config contiene valori di connessione hello necessario.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="1c6bc-168">Hello valori hello <appSettings> elemento sono valori hello necessario ottenuti nel processo di installazione di account servizi multimediali hello.</span><span class="sxs-lookup"><span data-stu-id="1c6bc-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="1c6bc-169">tooretrieve i valori di connessione della configurazione, è possibile utilizzare hello **ConfigurationManager** e quindi assegnare toofields valori hello nel codice:</span><span class="sxs-lookup"><span data-stu-id="1c6bc-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="1c6bc-170">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1c6bc-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1c6bc-171">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1c6bc-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

