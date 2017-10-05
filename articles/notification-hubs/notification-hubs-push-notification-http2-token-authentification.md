---
title: Autenticazione basata su token (HTTP/2) per il servizio APN negli hub di notifica di Azure | Microsoft Docs
description: Questo argomento spiega come sfruttare i vantaggi della nuova autenticazione basata su token per il servizio APN
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
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="3e4db-103">Autenticazione basata su token (HTTP/2) per il servizio APN</span><span class="sxs-lookup"><span data-stu-id="3e4db-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="3e4db-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3e4db-104">Overview</span></span>
<span data-ttu-id="3e4db-105">Questo articolo illustra come usare il nuovo protocollo HTTP/2 del servizio APN con l'autenticazione basata su token.</span><span class="sxs-lookup"><span data-stu-id="3e4db-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="3e4db-106">Ecco i vantaggi principali dell'uso del nuovo protocollo:</span><span class="sxs-lookup"><span data-stu-id="3e4db-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="3e4db-107">La generazione di token è relativamente semplice rispetto ai certificati.</span><span class="sxs-lookup"><span data-stu-id="3e4db-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="3e4db-108">Non sono previste scadenze: l'utente ha il controllo completo dei token di autenticazione e della rispettiva revoca.</span><span class="sxs-lookup"><span data-stu-id="3e4db-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="3e4db-109">Sono consentiti payload fino a 4 KB.</span><span class="sxs-lookup"><span data-stu-id="3e4db-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="3e4db-110">Commenti e suggerimenti sincroni</span><span class="sxs-lookup"><span data-stu-id="3e4db-110">Synchronous feedback</span></span>
-   <span data-ttu-id="3e4db-111">Viene usato il protocollo più recente di Apple, mentre i certificati usano ancora il protocollo binario, contrassegnato per l'eliminazione</span><span class="sxs-lookup"><span data-stu-id="3e4db-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="3e4db-112">Per usare questo nuovo meccanismo sono sufficienti due passaggi che richiedono pochi minuti:</span><span class="sxs-lookup"><span data-stu-id="3e4db-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="3e4db-113">Ottenere le informazioni necessarie dal portale per account sviluppatore Apple</span><span class="sxs-lookup"><span data-stu-id="3e4db-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="3e4db-114">Configurare l'hub di notifica con le nuove informazioni</span><span class="sxs-lookup"><span data-stu-id="3e4db-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="3e4db-115">Hub di notifica è ora configurato per l'uso del nuovo sistema di autenticazione con il servizio APN.</span><span class="sxs-lookup"><span data-stu-id="3e4db-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="3e4db-116">Se è stata eseguita la migrazione dall'uso delle credenziali del certificato per il servizio APN, si noti quanto segue:</span><span class="sxs-lookup"><span data-stu-id="3e4db-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="3e4db-117">Le proprietà del token sovrascrivono il certificato nel sistema.</span><span class="sxs-lookup"><span data-stu-id="3e4db-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="3e4db-118">L'applicazione continua tuttavia a ricevere le notifiche senza problemi.</span><span class="sxs-lookup"><span data-stu-id="3e4db-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="3e4db-119">Recupero delle informazioni di autenticazione da Apple</span><span class="sxs-lookup"><span data-stu-id="3e4db-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="3e4db-120">Per abilitare l'autenticazione basata su token, sono necessarie le proprietà seguenti dell'account sviluppatore Apple:</span><span class="sxs-lookup"><span data-stu-id="3e4db-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="3e4db-121">Identificatore di chiave</span><span class="sxs-lookup"><span data-stu-id="3e4db-121">Key Identifier</span></span>
<span data-ttu-id="3e4db-122">L'identificatore di chiave può esser ottenuto dalla pagina "Keys" (Chiavi) dell'account sviluppatore Apple.</span><span class="sxs-lookup"><span data-stu-id="3e4db-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="3e4db-123">Identificatore dell'applicazione e nome dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="3e4db-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="3e4db-124">Il nome dell'applicazione è disponibile nella pagina relativa agli ID dell'app dell'account sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="3e4db-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="3e4db-125">L'identificatore dell'applicazione è disponibile tramite la pagina relativa ai dettagli dell'appartenenza dell'account sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="3e4db-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="3e4db-126">Token di autenticazione</span><span class="sxs-lookup"><span data-stu-id="3e4db-126">Authentication token</span></span>
<span data-ttu-id="3e4db-127">Il token di autenticazione può essere scaricato dopo la generazione di un token per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e4db-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="3e4db-128">Per informazioni dettagliate su come generare questo token, vedere la [documentazione per sviluppatori di Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="3e4db-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="3e4db-129">Configurazione dell'hub di notifica per l'uso dell'autenticazione basata su token</span><span class="sxs-lookup"><span data-stu-id="3e4db-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="3e4db-130">Eseguire la configurazione tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3e4db-130">Configure via the Azure portal</span></span>
<span data-ttu-id="3e4db-131">Per abilitare l'autenticazione basata su token nel portale, accedere a portale di Azure e passare al pannello Hub di notifica > Servizi di notifica > Servizio APN.</span><span class="sxs-lookup"><span data-stu-id="3e4db-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="3e4db-132">È disponibile una nuova proprietà, ovvero *Modalità di autenticazione*.</span><span class="sxs-lookup"><span data-stu-id="3e4db-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="3e4db-133">La selezione del token consente di aggiornare l'hub con tutte le proprietà rilevanti del token.</span><span class="sxs-lookup"><span data-stu-id="3e4db-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="3e4db-134">Immettere le proprietà recuperate dall'account sviluppatore Apple.</span><span class="sxs-lookup"><span data-stu-id="3e4db-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="3e4db-135">Scegliere la modalità dell'applicazione (produzione o sandbox).</span><span class="sxs-lookup"><span data-stu-id="3e4db-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="3e4db-136">Fare clic su Salva per aggiornare le credenziali del servizio APN.</span><span class="sxs-lookup"><span data-stu-id="3e4db-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="3e4db-137">Configurazione tramite API Gestione (REST)</span><span class="sxs-lookup"><span data-stu-id="3e4db-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="3e4db-138">È possibile usare le [API di gestione](https://msdn.microsoft.com/library/azure/dn495827.aspx) per aggiornare l'hub di notifica per l'uso dell'autenticazione basata su token.</span><span class="sxs-lookup"><span data-stu-id="3e4db-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="3e4db-139">In base alla modalità usata per l'app da configurare, ovvero sandbox o produzione, come indicato nell'account sviluppatore Apple, usare uno degli endpoint corrispondenti:</span><span class="sxs-lookup"><span data-stu-id="3e4db-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="3e4db-140">Endpoint sandbox: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="3e4db-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="3e4db-141">Endpoint di produzione: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="3e4db-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e4db-142">L'autenticazione basata su token richiede una versione **2017-04 o successiva** dell'API.</span><span class="sxs-lookup"><span data-stu-id="3e4db-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="3e4db-143">Ecco un esempio di richiesta PUT per l'aggiornamento di un hub con l'autenticazione basata su token:</span><span class="sxs-lookup"><span data-stu-id="3e4db-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="3e4db-144">Configurazione tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3e4db-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="3e4db-145">È possibile configurare l'hub per l'uso dell'autenticazione basata su token tramite la [versione più recente dell'SDK client](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="3e4db-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="3e4db-146">Ecco un esempio di codice che illustra l'utilizzo corretto:</span><span class="sxs-lookup"><span data-stu-id="3e4db-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="3e4db-147">Ripristino dell'uso dell'autenticazione basata su certificati</span><span class="sxs-lookup"><span data-stu-id="3e4db-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="3e4db-148">È possibile ripristinare in qualsiasi momento l'uso dell'autenticazione basata su certificati usando uno dei metodi precedenti e passando il certificato invece delle proprietà dei token.</span><span class="sxs-lookup"><span data-stu-id="3e4db-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="3e4db-149">Questa azione sovrascrive le credenziali archiviate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3e4db-149">That action overwrites the previously stored credentials.</span></span>
