---
title: Eseguire l'autenticazione con le API REST di Mobile Engagement
description: Descrive come eseguire l'autenticazione con le API REST di Azure Mobile Engagement
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
ms.openlocfilehash: b05181d9252c0a804648e01b4058019278ae5abe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="0788a-103">Eseguire l'autenticazione con le API REST di Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="0788a-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="0788a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0788a-104">Overview</span></span>
<span data-ttu-id="0788a-105">Il presente documento descrive come ottenere un token Oauth AAD per eseguire l'autenticazione con le API REST di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="0788a-105">This document describes how to get a valid AAD Oauth token to authenticate with the Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="0788a-106">Si presuppone che l'utente abbia una sottoscrizione di Azure valida e che abbia creato un'app Mobile Engagement usando una delle [Esercitazioni per sviluppatori](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0788a-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="0788a-107">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="0788a-107">Authentication</span></span>
<span data-ttu-id="0788a-108">È necessario usare per l'autenticazione un token OAuth basato su Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0788a-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="0788a-109">Per autenticare richieste API, è necessario aggiungere un'intestazione di autorizzazione a ciascuna richiesta della seguente forma:</span><span class="sxs-lookup"><span data-stu-id="0788a-109">In order to authentication an API request, an authorization header must be added to every request which is of the following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="0788a-110">I token di Azure Active Directory scadono in un'ora.</span><span class="sxs-lookup"><span data-stu-id="0788a-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="0788a-111">È possibile ottenere un token in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="0788a-111">There are several ways to get a token.</span></span> <span data-ttu-id="0788a-112">Dal momento che le API vengono in genere chiamate da un servizio cloud, si vorrà usare una chiave API.</span><span class="sxs-lookup"><span data-stu-id="0788a-112">Since the APIs are generally called from a cloud service, you want to use an API key.</span></span> <span data-ttu-id="0788a-113">Nella terminologia di Azure una chiave API è una password dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="0788a-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="0788a-114">La procedura seguente descrive come impostarla in modo manuale.</span><span class="sxs-lookup"><span data-stu-id="0788a-114">The following procedure describes one way to setting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="0788a-115">Installazione singola (mediante script)</span><span class="sxs-lookup"><span data-stu-id="0788a-115">One-time setup (using script)</span></span>
<span data-ttu-id="0788a-116">È necessario osservare le istruzioni seguenti per eseguire l'installazione tramite uno script di PowerShell che richiede il minor tempo ma che utilizza le impostazioni predefinite più ammissibili.</span><span class="sxs-lookup"><span data-stu-id="0788a-116">You should follow the set of instructions below to perform the setup using a PowerShell script which takes the minimum time for setup but uses the most permissible defaults.</span></span> <span data-ttu-id="0788a-117">Facoltativamente, è anche possibile seguire le istruzioni per [l'installazione manuale](mobile-engagement-api-authentication-manual.md) per eseguire questa operazione direttamente dal portale di Azure con una configurazione più precisa.</span><span class="sxs-lookup"><span data-stu-id="0788a-117">Optionally, you can also follow the instructions in the [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from the Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="0788a-118">Usare la versione più recente di Azure PowerShell che può essere scaricata [qui](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="0788a-118">Get the latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="0788a-119">Per ulteriori informazioni sulle istruzioni di download, è possibile visualizzare questo [collegamento](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0788a-119">For more information on the download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="0788a-120">Dopo aver installato Azure PowerShell, usare i comandi seguenti per assicurarsi che il **modulo Azure** sia installato:</span><span class="sxs-lookup"><span data-stu-id="0788a-120">Once Azure PowerShell is installed, use the following commands to ensure that you have the **Azure module** installed:</span></span>
   
    <span data-ttu-id="0788a-121">a.</span><span class="sxs-lookup"><span data-stu-id="0788a-121">a.</span></span> <span data-ttu-id="0788a-122">Assicurarsi che il modulo Azure PowerShell sia presente nell'elenco dei moduli disponibili.</span><span class="sxs-lookup"><span data-stu-id="0788a-122">Make sure the Azure PowerShell module is available in the list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Moduli di Azure disponibili][1]
   
    <span data-ttu-id="0788a-124">b.</span><span class="sxs-lookup"><span data-stu-id="0788a-124">b.</span></span> <span data-ttu-id="0788a-125">Se il modulo Azure PowerShell non è presente nell'elenco precedente, è necessario procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="0788a-125">If you do not find the Azure PowerShell module in the above list then you need to run the following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="0788a-126">Accedere ad Azure Resource Manager da PowerShell eseguendo il comando seguente e fornendo nome utente e password dell'account Azure:</span><span class="sxs-lookup"><span data-stu-id="0788a-126">Login to the Azure Resource Manager from PowerShell by running the following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="0788a-127">In caso di più sottoscrizioni, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="0788a-127">If you have multiple subscriptions then you should run the following:</span></span>
   
    <span data-ttu-id="0788a-128">a.</span><span class="sxs-lookup"><span data-stu-id="0788a-128">a.</span></span> <span data-ttu-id="0788a-129">Ottenere un elenco di tutte le sottoscrizioni e copiare il SubscriptionId della sottoscrizione che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="0788a-129">Get a list of all your subscriptions and copy the SubscriptionId of the subscription you want to use.</span></span> <span data-ttu-id="0788a-130">Assicurarsi che la sottoscrizione corrisponda a quella dell'app Mobile Engagement con cui si andrà a interagire tramite le API.</span><span class="sxs-lookup"><span data-stu-id="0788a-130">Make sure this subscription is the same one which has the Mobile Engagement App which you are going to interact with using the APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="0788a-131">b.</span><span class="sxs-lookup"><span data-stu-id="0788a-131">b.</span></span> <span data-ttu-id="0788a-132">Eseguire il comando seguente specificando il SubscriptionId per configurare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="0788a-132">Run the following command providing the SubscriptionId to configure the subscription to be used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="0788a-133">Copiare il testo per lo script [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) nel computer locale, salvarlo come cmdlet PowerShell (ad esempio `APIAuth.ps1`) ed eseguirlo `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="0788a-133">Copy the text for the [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script to your local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="0788a-134">Lo script richiederà di immettere un **principalName**.</span><span class="sxs-lookup"><span data-stu-id="0788a-134">The script will ask you to provide an input for **principalName**.</span></span> <span data-ttu-id="0788a-135">Fornire un nome adeguato da utilizzare per creare l'applicazione Active Directory (ad esempio APIAuth).</span><span class="sxs-lookup"><span data-stu-id="0788a-135">Provide a suitable name here that you want to use to create your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="0788a-136">Dopo il completamento dello script, accertarsi di copiare i quattro valori seguenti che verranno visualizzati, necessari per un'autenticazione a livello di codice con AD </span><span class="sxs-lookup"><span data-stu-id="0788a-136">After the script completes, it will display the following four values that you will need to authenticate programmatically with AD so make sure to copy them.</span></span> 
   
    <span data-ttu-id="0788a-137">**TenantId**, **SubscriptionId**, **ApplicationId** e **Secret**.</span><span class="sxs-lookup"><span data-stu-id="0788a-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="0788a-138">TenantId sarà usato come `{TENANT_ID}`, ApplicationId come `{CLIENT_ID}` e Secret come `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="0788a-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0788a-139">I criteri di sicurezza predefiniti possono bloccare l'esecuzione degli script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0788a-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="0788a-140">In questo caso, configurare temporaneamente i criteri di esecuzione in modo da consentire l'esecuzione degli script usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0788a-140">If so, you temporarily configure your execution policy to allow script execution using the following command:</span></span>
   > 
   > <span data-ttu-id="0788a-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="0788a-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="0788a-142">L'insieme di cmdlet PS sarà simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="0788a-142">Here is how the set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="0788a-143">Controllare nel portale di gestione di Azure che sia stata creata una nuova applicazione AD con il nome specificato per lo script denominato **principalName** in **Mostra Applicazioni di proprietà dell'azienda**.</span><span class="sxs-lookup"><span data-stu-id="0788a-143">Check in the Azure Management portal that a new AD application was created with the name you provided to the script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-to-get-a-valid-token"></a><span data-ttu-id="0788a-144">Procedura per ottenere un token valido</span><span class="sxs-lookup"><span data-stu-id="0788a-144">Steps to get a valid token</span></span>
1. <span data-ttu-id="0788a-145">Chiamare l'API con i parametri seguenti e assicurarsi di sostituire TENANT\_ID, CLIENT\_ID e CLIENT\_SECRET:</span><span class="sxs-lookup"><span data-stu-id="0788a-145">Call the API with the following parameters and make sure to replace the TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="0788a-146">**URL richiesta** come *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="0788a-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="0788a-147">**Intestazione Content-Type HTTP** come *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="0788a-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="0788a-148">**Corpo richiesta HTTP** come *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="0788a-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="0788a-149">Di seguito è riportata una richiesta di esempio:</span><span class="sxs-lookup"><span data-stu-id="0788a-149">The following is an example request:</span></span>
     
       <span data-ttu-id="0788a-150">POST / {TENANT_ID} / oauth2/token Host HTTP/1.1: login.microsoftonline.com Content-Type: grant_type application/x-www-form-urlencoded = client_credentials & client_id = {CLIENT_ID} & client_secret = {CLIENT_SECRET} & reso urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="0788a-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="0788a-151">Di seguito è riportata una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="0788a-151">Here is an example response:</span></span>
     
       <span data-ttu-id="0788a-152">HTTP/1.1 200 OK Content-Type: application/json; charset = utf-8. Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="0788a-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="0788a-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="0788a-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="0788a-154">Questo esempio include la codifica URL dei parametri POST. Il valore `resource` effettivo è `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="0788a-154">This example included URL encoding of the POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="0788a-155">Prestare attenzione anche alla codifica URL di `{CLIENT_SECRET}` perché può contenere caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="0788a-155">Be careful to also URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="0788a-156">Per i test, è possibile usare uno strumento client HTTP come [Fiddler](http://www.telerik.com/fiddler) o [l'estensione Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="0788a-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="0788a-157">Ora in ogni chiamata all'API includere l'intestazione della richiesta di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="0788a-157">Now in every API call, include the authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="0788a-158">Se viene restituito il codice di stato 401, rivedere il corpo della risposta e controllare che il token non sia scaduto.</span><span class="sxs-lookup"><span data-stu-id="0788a-158">If you get a 401 status code returned, check the response body, it might tell you the token is expired.</span></span> <span data-ttu-id="0788a-159">In caso affermativo, ottenere un nuovo token.</span><span class="sxs-lookup"><span data-stu-id="0788a-159">In that case, get a new token.</span></span>

## <a name="using-the-apis"></a><span data-ttu-id="0788a-160">Uso delle API</span><span class="sxs-lookup"><span data-stu-id="0788a-160">Using the APIs</span></span>
<span data-ttu-id="0788a-161">Ora che si dispone di un token valido, è possibile eseguire chiamate API.</span><span class="sxs-lookup"><span data-stu-id="0788a-161">Now that you have a valid token, you are ready to make the API calls.</span></span>

1. <span data-ttu-id="0788a-162">È necessario passare in ciascuna richiesta API un token valido e non scaduto, ottenuto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="0788a-162">In each API request, you will need to pass a valid, unexpired token which you obtained in the previous section.</span></span>
2. <span data-ttu-id="0788a-163">È necessario inserire alcuni parametri nella richiesta URI che identifica l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0788a-163">You will need to plug in some parameters into the request URI which identifies your application.</span></span> <span data-ttu-id="0788a-164">L'URI di richiesta è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0788a-164">The request URI looks like the following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="0788a-165">Per ottenere i parametri, fare clic sul nome dell'applicazione e quindi su Dashboard. Verrà visualizzata una pagina simile a quella riportata di seguito, con tutti e tre i parametri.</span><span class="sxs-lookup"><span data-stu-id="0788a-165">To get the parameters, click on your application name and click Dashboard and you will see a page like the following with all the 3 parameters.</span></span>
   
   * <span data-ttu-id="0788a-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="0788a-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="0788a-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="0788a-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="0788a-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="0788a-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="0788a-169">**4**Il nome del gruppo di risorse sarà **MobileEngagement** a meno che non ne sia stato creato uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="0788a-169">**4** Your Resource Group name is going to be **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Parametri URI API di Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="0788a-171">Ignorare l'indirizzo radice dell'API perché riferito alle API precedenti.</span><span class="sxs-lookup"><span data-stu-id="0788a-171">Ignore the API Root Address as this was for the previous APIs.</span></span><br/>
> 2. <span data-ttu-id="0788a-172">Se l'app è stata creata tramite il portale di Azure classico, è necessario usare il nome della Risorsa applicazione, che è diverso dal nome dell'applicazione stessa.</span><span class="sxs-lookup"><span data-stu-id="0788a-172">If you created the app using Azure Classic portal then you need to use the Application Resource name which is different than the Application name itself.</span></span> <span data-ttu-id="0788a-173">Se l'app è stata creata nel portale di Azure, è necessario usare il nome dell'applicazione stessa. In questo caso, il nome della Risorsa applicazione non differisce dal nome dell'app per le applicazioni create nel nuovo portale.</span><span class="sxs-lookup"><span data-stu-id="0788a-173">If you created the app in the Azure Portal then you should use the App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in the new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



