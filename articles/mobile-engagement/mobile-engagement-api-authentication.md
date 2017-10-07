---
title: aaaAuthenticate con le API REST di Engagement Mobile
description: Viene descritto come tooauthenticate con le API REST di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="572a9-103">Eseguire l'autenticazione con le API REST di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="572a9-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="572a9-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="572a9-104">Overview</span></span>
<span data-ttu-id="572a9-105">Questo documento descrive come un Oauth di AAD valido di tooget token tooauthenticate con hello API REST di Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="572a9-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="572a9-106">Si presuppone che l'utente abbia una sottoscrizione di Azure valida e che abbia creato un'app Mobile Engagement usando una delle [Esercitazioni per sviluppatori](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="572a9-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="572a9-107">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="572a9-107">Authentication</span></span>
<span data-ttu-id="572a9-108">È necessario usare per l'autenticazione un token OAuth basato su Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="572a9-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="572a9-109">Nella richiesta di ordine tooauthentication un'API, un'intestazione di autorizzazione deve essere aggiunto richiesta tooevery di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="572a9-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="572a9-110">I token di Azure Active Directory scadono in un'ora.</span><span class="sxs-lookup"><span data-stu-id="572a9-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="572a9-111">Esistono diversi modi tooget un token.</span><span class="sxs-lookup"><span data-stu-id="572a9-111">There are several ways tooget a token.</span></span> <span data-ttu-id="572a9-112">Poiché hello che API vengono in genere chiamate da un servizio cloud, si desidera toouse una chiave API.</span><span class="sxs-lookup"><span data-stu-id="572a9-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="572a9-113">Nella terminologia di Azure una chiave API è una password dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="572a9-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="572a9-114">Hello procedura seguente viene illustrato un modo toosetting il backup manualmente.</span><span class="sxs-lookup"><span data-stu-id="572a9-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="572a9-115">Installazione singola (mediante script)</span><span class="sxs-lookup"><span data-stu-id="572a9-115">One-time setup (using script)</span></span>
<span data-ttu-id="572a9-116">È consigliabile seguire il set di hello di istruzioni che seguono il programma di installazione di tooperform hello tramite uno script di PowerShell che richiede hello tempo minimo per l'installazione, ma vengono utilizzati valori predefiniti più ammissibili hello.</span><span class="sxs-lookup"><span data-stu-id="572a9-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="572a9-117">Facoltativamente, è possibile inoltre seguire le istruzioni hello hello [installazione manuale](mobile-engagement-api-authentication-manual.md) per eseguire questa operazione da hello direttamente portale di Azure e configurazione di eseguire più preciso.</span><span class="sxs-lookup"><span data-stu-id="572a9-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="572a9-118">Ottenere la versione più recente di hello di Azure PowerShell da [qui](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="572a9-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="572a9-119">Per ulteriori informazioni sulle istruzioni di download di hello, è possibile visualizzare questo [collegamento](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="572a9-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="572a9-120">Una volta installato Azure PowerShell, seguito hello utilizzare comandi tooensure di aver hello **modulo Azure** installato:</span><span class="sxs-lookup"><span data-stu-id="572a9-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="572a9-121">a.</span><span class="sxs-lookup"><span data-stu-id="572a9-121">a.</span></span> <span data-ttu-id="572a9-122">Verificare che il modulo di Azure PowerShell hello è disponibile nell'elenco di hello dei moduli disponibili.</span><span class="sxs-lookup"><span data-stu-id="572a9-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Moduli di Azure disponibili][1]
   
    <span data-ttu-id="572a9-124">b.</span><span class="sxs-lookup"><span data-stu-id="572a9-124">b.</span></span> <span data-ttu-id="572a9-125">Se non si trova il modulo di Azure PowerShell hello in hello sopra l'elenco è necessario seguente hello toorun:</span><span class="sxs-lookup"><span data-stu-id="572a9-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="572a9-126">Account di accesso toohello, Gestione risorse di Azure da PowerShell eseguendo hello comando seguente e di fornire il nome utente e la password per l'account di Azure:</span><span class="sxs-lookup"><span data-stu-id="572a9-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="572a9-127">Se sono presenti più sottoscrizioni, è consigliabile eseguire l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="572a9-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="572a9-128">a.</span><span class="sxs-lookup"><span data-stu-id="572a9-128">a.</span></span> <span data-ttu-id="572a9-129">Ottenere un elenco di tutte le sottoscrizioni e hello copia SubscriptionId della sottoscrizione hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="572a9-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="572a9-130">Verificare che la sottoscrizione è quello che ha hello App Engagement Mobile che si prevede di hello toointeract con hello API.</span><span class="sxs-lookup"><span data-stu-id="572a9-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="572a9-131">b.</span><span class="sxs-lookup"><span data-stu-id="572a9-131">b.</span></span> <span data-ttu-id="572a9-132">Comando che segue di hello esecuzione fornendo hello SubscriptionId tooconfigure hello sottoscrizione toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="572a9-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="572a9-133">Copiare il testo hello per hello [New AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour locali e salvarlo come un cmdlet di PowerShell (ad esempio `APIAuth.ps1`) ed eseguirlo `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="572a9-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="572a9-134">Hello script chiederà tooprovide un input per **nome dell'entità**.</span><span class="sxs-lookup"><span data-stu-id="572a9-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="572a9-135">Fornire un nome appropriato che si desidera toouse toocreate l'applicazione di Active Directory (ad esempio APIAuth).</span><span class="sxs-lookup"><span data-stu-id="572a9-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="572a9-136">Al termine dell'esecuzione dello script hello, verrà visualizzato hello seguenti quattro valori che è necessario tooauthenticate a livello di programmazione con Active Directory per rendere toocopy che li.</span><span class="sxs-lookup"><span data-stu-id="572a9-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="572a9-137">**TenantId**, **SubscriptionId**, **ApplicationId** e **Secret**.</span><span class="sxs-lookup"><span data-stu-id="572a9-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="572a9-138">TenantId sarà usato come `{TENANT_ID}`, ApplicationId come `{CLIENT_ID}` e Secret come `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="572a9-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="572a9-139">I criteri di sicurezza predefiniti possono bloccare l'esecuzione degli script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="572a9-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="572a9-140">In questo caso, configurare temporaneamente l'esecuzione di script tooallow dei criteri di esecuzione utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="572a9-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="572a9-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="572a9-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="572a9-142">Ecco come set di hello di cmdlet di PS avrà un aspetto analogo.</span><span class="sxs-lookup"><span data-stu-id="572a9-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="572a9-143">Controllare nel portale di gestione di Azure hello che una nuova applicazione di Active Directory è stata creata con il nome di hello è fornito toohello script chiamato **nome dell'entità** in **applicazioni Mostra proprietà dell'azienda**.</span><span class="sxs-lookup"><span data-stu-id="572a9-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="572a9-144">Passaggi tooget un token valido</span><span class="sxs-lookup"><span data-stu-id="572a9-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="572a9-145">Chiamata API hello con hello seguenti parametri e verificare che tooreplace hello TENANT\_ID, i CLIENT\_ID e CLIENT\_segreto:</span><span class="sxs-lookup"><span data-stu-id="572a9-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="572a9-146">**URL richiesta** come *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="572a9-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="572a9-147">**Intestazione Content-Type HTTP** come *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="572a9-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="572a9-148">**Corpo richiesta HTTP** come *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="572a9-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="572a9-149">di seguito Hello è un esempio di richiesta:</span><span class="sxs-lookup"><span data-stu-id="572a9-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="572a9-150">POST / {TENANT_ID} / oauth2/token Host HTTP/1.1: login.microsoftonline.com Content-Type: grant_type application/x-www-form-urlencoded = client_credentials & client_id = {CLIENT_ID} & client_secret = {CLIENT_SECRET} & reso urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="572a9-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="572a9-151">Di seguito è riportata una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="572a9-151">Here is an example response:</span></span>
     
       <span data-ttu-id="572a9-152">HTTP/1.1 200 OK Content-Type: application/json; charset = utf-8. Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="572a9-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="572a9-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="572a9-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="572a9-154">In questo esempio è inclusa la codifica URL dei parametri POST hello, `resource` valore sia effettivamente `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="572a9-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="572a9-155">Assicurarsi che la codifica URL tooalso `{CLIENT_SECRET}` , che potrebbe contenere caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="572a9-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="572a9-156">Per i test, è possibile usare uno strumento client HTTP come [Fiddler](http://www.telerik.com/fiddler) o [l'estensione Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="572a9-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="572a9-157">In ogni chiamata API, includono ora intestazione di richiesta di autorizzazione hello:</span><span class="sxs-lookup"><span data-stu-id="572a9-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="572a9-158">Se viene visualizzato un codice di 401 stato restituito, corpo della risposta hello controllo, potrebbe indicare hello token è scaduto.</span><span class="sxs-lookup"><span data-stu-id="572a9-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="572a9-159">In caso affermativo, ottenere un nuovo token.</span><span class="sxs-lookup"><span data-stu-id="572a9-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="572a9-160">Utilizzando le API di hello</span><span class="sxs-lookup"><span data-stu-id="572a9-160">Using hello APIs</span></span>
<span data-ttu-id="572a9-161">Dopo aver creato un token valido, si è pronti toomake hello API chiamate.</span><span class="sxs-lookup"><span data-stu-id="572a9-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="572a9-162">In ogni richiesta di API, è necessario un token valido e non scaduto è ottenuto nella sezione precedente di hello toopass.</span><span class="sxs-lookup"><span data-stu-id="572a9-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="572a9-163">È necessario tooplug alcuni parametri nella richiesta di hello URI che identifica l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="572a9-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="572a9-164">URI della richiesta Hello è simile a hello seguente</span><span class="sxs-lookup"><span data-stu-id="572a9-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="572a9-165">parametri di hello tooget, fare clic sul nome dell'applicazione e fare clic su Dashboard per visualizzare una pagina come segue hello con tutte hello 3 parametri.</span><span class="sxs-lookup"><span data-stu-id="572a9-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="572a9-166">**1**`{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="572a9-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="572a9-167">**2**`{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="572a9-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="572a9-168">**3**`{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="572a9-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="572a9-169">**4** nome del gruppo di risorse sta toobe **MobileEngagement** a meno che non è stato creato uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="572a9-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Parametri URI API di Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="572a9-171">Ignorare hello indirizzo radice API perché questo era per hello API precedente.</span><span class="sxs-lookup"><span data-stu-id="572a9-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="572a9-172">Se si hello app creata usando il portale di Azure classico è necessario nome di risorsa dell'applicazione hello toouse che è diverso dal nome dell'applicazione hello stesso.</span><span class="sxs-lookup"><span data-stu-id="572a9-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="572a9-173">Se si crea l'applicazione hello in hello portale di Azure è necessario utilizzare hello Nome App stesso (non vi è alcuna differenza tra il nome di risorsa dell'applicazione e il nome dell'App per le app create nel nuovo portale di hello).</span><span class="sxs-lookup"><span data-stu-id="572a9-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



