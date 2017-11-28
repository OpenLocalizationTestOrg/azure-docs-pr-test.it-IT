---
title: Autenticazione basata su aaaToken di (HTTP/2) per il servizio APN nell'hub di notifica di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come tooleverage hello nuova autenticazione del token per il servizio APN
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="8c2f0-103">Autenticazione basata su token (HTTP/2) per il servizio APN</span><span class="sxs-lookup"><span data-stu-id="8c2f0-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="8c2f0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8c2f0-104">Overview</span></span>
<span data-ttu-id="8c2f0-105">In questo articolo illustra in dettaglio come l'autenticazione basata su protocollo nuovo APN HTTP/2 toouse hello con token.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="8c2f0-106">vantaggi principali di Hello dell'utilizzo di nuovo protocollo di hello includono:</span><span class="sxs-lookup"><span data-stu-id="8c2f0-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="8c2f0-107">Generazione dei token è relativamente semplice disponibile (confrontati toocertificates)</span><span class="sxs-lookup"><span data-stu-id="8c2f0-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="8c2f0-108">Non sono previste scadenze: l'utente ha il controllo completo dei token di autenticazione e della rispettiva revoca.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="8c2f0-109">È ora possibile payload too4 KB</span><span class="sxs-lookup"><span data-stu-id="8c2f0-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="8c2f0-110">Commenti e suggerimenti sincroni</span><span class="sxs-lookup"><span data-stu-id="8c2f0-110">Synchronous feedback</span></span>
-   <span data-ttu-id="8c2f0-111">Si è sul protocollo più recente di Apple – i certificati utilizzano ancora protocollo binario hello, che è contrassegnato per l'eliminazione</span><span class="sxs-lookup"><span data-stu-id="8c2f0-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="8c2f0-112">Per usare questo nuovo meccanismo sono sufficienti due passaggi che richiedono pochi minuti:</span><span class="sxs-lookup"><span data-stu-id="8c2f0-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="8c2f0-113">Ottenere le informazioni necessarie hello dal portale di Account per sviluppatori Apple hello</span><span class="sxs-lookup"><span data-stu-id="8c2f0-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="8c2f0-114">Configurare l'hub di notifica con le nuove informazioni hello</span><span class="sxs-lookup"><span data-stu-id="8c2f0-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="8c2f0-115">Gli hub di notifica è ora tutti i set toouse hello nuovo sistema di autenticazione con il servizio APN.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="8c2f0-116">Se è stata eseguita la migrazione dall'uso delle credenziali del certificato per il servizio APN, si noti quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8c2f0-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="8c2f0-117">proprietà token Hello sovrascrivere il certificato nel sistema,</span><span class="sxs-lookup"><span data-stu-id="8c2f0-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="8c2f0-118">ma l'applicazione continua tooreceive notifiche senza problemi.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="8c2f0-119">Recupero delle informazioni di autenticazione da Apple</span><span class="sxs-lookup"><span data-stu-id="8c2f0-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="8c2f0-120">l'autenticazione basata su token tooenable, è necessario hello le proprietà seguenti dal tuo Account sviluppatore Apple:</span><span class="sxs-lookup"><span data-stu-id="8c2f0-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="8c2f0-121">Identificatore di chiave</span><span class="sxs-lookup"><span data-stu-id="8c2f0-121">Key Identifier</span></span>
<span data-ttu-id="8c2f0-122">Identificatore di chiave Hello può essere ottenuti dalla pagina "Chiavi" hello nell'Account per sviluppatori di Apple</span><span class="sxs-lookup"><span data-stu-id="8c2f0-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="8c2f0-123">Identificatore dell'applicazione e nome dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c2f0-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="8c2f0-124">nome dell'applicazione Hello è disponibile nella pagina di ID App hello in hello Account sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="8c2f0-125">Identificatore dell'applicazione Hello è disponibile nella pagina dettagli di appartenenza hello in hello Account sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="8c2f0-126">Token di autenticazione</span><span class="sxs-lookup"><span data-stu-id="8c2f0-126">Authentication token</span></span>
<span data-ttu-id="8c2f0-127">è possibile scaricare il token di autenticazione Hello dopo la generazione di un token per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="8c2f0-128">Per informazioni dettagliate su come toogenerate questo token, vedere troppo[documentazione per sviluppatori di Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="8c2f0-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="8c2f0-129">Configurazione dell'autenticazione basata su token toouse la notifica hub</span><span class="sxs-lookup"><span data-stu-id="8c2f0-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="8c2f0-130">Configurare tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8c2f0-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="8c2f0-131">token tooenable in base l'autenticazione nel portale di hello, accedi toohello portale di Azure e passare tooyour Hub di notifica > Notification Services > Pannello APN.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="8c2f0-132">È disponibile una nuova proprietà, ovvero *Modalità di autenticazione*.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="8c2f0-133">Se si seleziona Token sarà tooupdate l'hub con tutte hello token le proprietà rilevanti.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="8c2f0-134">Immettere proprietà hello recuperato dal tuo account sviluppatore di Apple,</span><span class="sxs-lookup"><span data-stu-id="8c2f0-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="8c2f0-135">Scegliere la modalità dell'applicazione (produzione o sandbox).</span><span class="sxs-lookup"><span data-stu-id="8c2f0-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="8c2f0-136">Fare clic su Salva tooupdate le credenziali APNS.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="8c2f0-137">Configurazione tramite API Gestione (REST)</span><span class="sxs-lookup"><span data-stu-id="8c2f0-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="8c2f0-138">È possibile utilizzare il nostro [le API di gestione](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate l'autenticazione basata su token di notifica hub toouse.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="8c2f0-139">A seconda se si sta configurando un'applicazione hello è un'applicazione di produzione o Sandbox (specificata nell'Account per sviluppatori di Apple), utilizzare uno degli endpoint corrispondente hello:</span><span class="sxs-lookup"><span data-stu-id="8c2f0-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="8c2f0-140">Endpoint sandbox: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="8c2f0-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="8c2f0-141">Endpoint di produzione: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="8c2f0-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c2f0-142">L'autenticazione basata su token richiede una versione **2017-04 o successiva** dell'API.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="8c2f0-143">Di seguito è riportato un esempio di un tooupdate richiesta PUT un hub con l'autenticazione basata su token:</span><span class="sxs-lookup"><span data-stu-id="8c2f0-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="8c2f0-144">Configurare tramite hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8c2f0-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="8c2f0-145">È possibile configurare l'autenticazione basata su token toouse hub utilizzando il nostro [client più recente SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="8c2f0-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="8c2f0-146">Di seguito è riportato un esempio di codice che descrive l'utilizzo corretto di hello:</span><span class="sxs-lookup"><span data-stu-id="8c2f0-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="8c2f0-147">Autenticazione basata su certificato toousing ripristino</span><span class="sxs-lookup"><span data-stu-id="8c2f0-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="8c2f0-148">È possibile ripristinare in qualsiasi autenticazione basata sui certificati di tempo toousing utilizzando qualsiasi certificato di hello (metodo) e il passaggio precedente anziché le proprietà token hello.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="8c2f0-149">Le credenziali che l'azione sovrascrive hello precedentemente archiviate.</span><span class="sxs-lookup"><span data-stu-id="8c2f0-149">That action overwrites hello previously stored credentials.</span></span>
