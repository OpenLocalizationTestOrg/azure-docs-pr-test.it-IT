---
title: aaaGet avviato con Data Lake Analitica tramite l'API REST | Documenti Microsoft
description: Utilizzare le API REST WebHDFS tooperform operazioni su Data Lake Analitica
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="0c6e2-103">Introduzione ad Azure Data Lake Analytics con API REST</span><span class="sxs-lookup"><span data-stu-id="0c6e2-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="0c6e2-104">Informazioni su come toouse WebHDFS REST API e le API REST di Data Lake Analitica toomanage Data Lake Analitica account, i processi e del catalogo.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0c6e2-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0c6e2-105">Prerequisites</span></span>
* <span data-ttu-id="0c6e2-106">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-106">**An Azure subscription**.</span></span> <span data-ttu-id="0c6e2-107">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0c6e2-108">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="0c6e2-109">Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello Data Lake Analitica con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="0c6e2-110">Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="0c6e2-111">Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autentica con Data Lake Analitica tramite Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="0c6e2-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="0c6e2-113">In questo articolo Usa toodemonstrate cURL come toomake API REST chiama rispetto a un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="0c6e2-114">Eseguire l'autenticazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c6e2-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="0c6e2-115">Per l'autenticazione con Azure Active Directory è possibile procedere in due modi.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="0c6e2-116">Autenticazione dell'utente finale (interattiva)</span><span class="sxs-lookup"><span data-stu-id="0c6e2-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="0c6e2-117">Utilizzando questo metodo, l'applicazione chiede toolog utente hello in e tutte le operazioni hello vengono eseguite nel contesto di hello dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="0c6e2-118">Eseguire questa procedura per l'autenticazione interattiva:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="0c6e2-119">Tramite l'applicazione, il reindirizzamento hello utente toohello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="0c6e2-120">\<URI di reindirizzamento > deve toobe codificati per l'uso in un URL.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="0c6e2-121">Per https://localhost, usare quindi `https%3A%2F%2Flocalhost`</span><span class="sxs-lookup"><span data-stu-id="0c6e2-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="0c6e2-122">A scopo di hello di questa esercitazione, è possibile sostituire i valori segnaposto hello nell'URL hello in precedenza e incollarlo nella barra degli indirizzi del web browser.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="0c6e2-123">Sarà reindirizzato tooauthenticate utilizzando l'account di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="0c6e2-124">Al termine si correttamente l'accesso, la risposta hello viene visualizzata nella barra degli indirizzi del browser hello.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="0c6e2-125">risposta Hello sarà in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="0c6e2-126">Acquisire il codice di autorizzazione hello dalla risposta hello.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="0c6e2-127">Per questa esercitazione, è possibile copiare il codice di autorizzazione hello dalla barra degli indirizzi del browser web hello hello e passarlo in hello POST richiesta toohello endpoint token, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="0c6e2-128">In questo caso, hello \<URI di reindirizzamento > non devono essere codificati.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="0c6e2-129">risposta Hello è un oggetto JSON che contiene un token di accesso (ad esempio, `"access_token": "<ACCESS_TOKEN>"`) e un token di aggiornamento (ad esempio, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="0c6e2-130">L'applicazione utilizza il token di accesso di hello quando si accede a un archivio Azure Data Lake e hello aggiornamento token tooget un altro token di accesso quando scade un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="0c6e2-131">Quando il token di accesso hello scade, è possibile richiedere un nuovo token di accesso usando il token di aggiornamento di hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="0c6e2-132">Per altre informazioni sull'autenticazione utente interattiva, vedere [Flusso di concessione del codice di autorizzazione](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="0c6e2-133">Autenticazione da servizio a servizio (non interattiva)</span><span class="sxs-lookup"><span data-stu-id="0c6e2-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="0c6e2-134">In questo modo, il applicazione fornisce le proprie credenziali tooperform hello operazioni.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="0c6e2-135">A tale scopo, è necessario inviare una richiesta POST come hello illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="0c6e2-136">output di Hello della richiesta includerà un token di autorizzazione (indicato da `access-token` nell'output di hello riportato di seguito) che verranno successivamente passati con le chiamate API REST.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="0c6e2-137">Salvare questo token di autenticazione in un file di testo, che sarà necessario più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="0c6e2-138">Questo articolo Usa hello **interattivo** approccio.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="0c6e2-139">Per ulteriori informazioni sulle modalità interattiva (chiamate service to service), vedere [tooservice chiamate utilizzando le credenziali del servizio](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="0c6e2-140">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="0c6e2-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="0c6e2-141">È necessario creare un gruppo di risorse di Azure e un account Data Lake Store prima di poter creare un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="0c6e2-142">Vedere [Creare un account Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="0c6e2-143">Hello seguente Curl comando Mostra come toocreate un account:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="0c6e2-144">Sostituire \< `REDACTED` \> con token di autorizzazione, hello \< `AzureSubscriptionID` \> con l'ID sottoscrizione, \< `AzureResourceGroupName` \> con una risorsa di Azure esistente Nome del gruppo, e \< `NewAzureDataLakeAnalyticsAccountName` \> con un nuovo nome Account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="0c6e2-145">payload della richiesta Hello per questo comando è contenuto in hello **CreateDatalakeAnalyticsAccountRequest.json** file fornito per hello `-d` parametro precedente.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="0c6e2-146">il contenuto di Hello del file input.json hello nella figura seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-146">hello contents of hello input.json file resemble hello following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="0c6e2-147">Elencare gli account di Data Lake Analytics in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="0c6e2-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="0c6e2-148">Hello Curl comando seguente viene illustrato come toolist account in una sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="0c6e2-149">Sostituire \< `REDACTED` \> con token di autorizzazione, hello \< `AzureSubscriptionID` \> con l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="0c6e2-150">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-150">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="0c6e2-151">Ottenere informazioni su un account Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="0c6e2-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="0c6e2-152">Hello seguente Curl comando Mostra come tooget informazioni account:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="0c6e2-153">Sostituire \< `REDACTED` \> con token di autorizzazione, hello \< `AzureSubscriptionID` \> con l'ID sottoscrizione, \< `AzureResourceGroupName` \> con una risorsa di Azure esistente Nome del gruppo, e \< `DataLakeAnalyticsAccountName` \> con nome hello di un Account esistente di Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="0c6e2-154">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-154">hello output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="0c6e2-155">Elencare gli archivi Data Lake di account Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0c6e2-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="0c6e2-156">Hello Curl comando seguente viene illustrato come gli archivi di un account toolist Data Lake:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="0c6e2-157">Sostituire \< `REDACTED` \> con token di autorizzazione, hello \< `AzureSubscriptionID` \> con l'ID sottoscrizione, \< `AzureResourceGroupName` \> con una risorsa di Azure esistente Nome del gruppo, e \< `DataLakeAnalyticsAccountName` \> con nome hello di un Account esistente di Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="0c6e2-158">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-158">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="0c6e2-159">Inviare processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="0c6e2-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="0c6e2-160">Hello seguente Curl comando Mostra come processo toosubmit U-SQL:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="0c6e2-161">Sostituire \< `REDACTED` \> con token di autorizzazione, hello \< `DataLakeAnalyticsAccountName` \> con nome hello di un Account esistente di Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="0c6e2-162">payload della richiesta Hello per questo comando è contenuto in hello **SubmitADLAJob.json** file fornito per hello `-d` parametro precedente.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="0c6e2-163">il contenuto di Hello del file input.json hello nella figura seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-163">hello contents of hello input.json file resemble hello following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="0c6e2-164">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-164">hello output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="0c6e2-165">Elencare i processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="0c6e2-165">List U-SQL jobs</span></span>
<span data-ttu-id="0c6e2-166">Hello seguente Curl comando Mostra come processi toolist U-SQL:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="0c6e2-167">Sostituire \< `REDACTED` \> con token di autorizzazione, hello e \< `DataLakeAnalyticsAccountName` \> con nome hello di un Account esistente di Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="0c6e2-168">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-168">hello output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="0c6e2-169">Ottenere gli elementi del catalogo</span><span class="sxs-lookup"><span data-stu-id="0c6e2-169">Get catalog items</span></span>
<span data-ttu-id="0c6e2-170">Hello Curl comando seguente viene illustrato come i database di hello tooget da hello catalogo:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="0c6e2-171">output di Hello è simile a:</span><span class="sxs-lookup"><span data-stu-id="0c6e2-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="0c6e2-172">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0c6e2-172">See also</span></span>
* <span data-ttu-id="0c6e2-173">toosee una query più complessa, vedere [sito Web di analizzare i log di Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="0c6e2-174">tooget iniziare a sviluppare applicazioni U-SQL, vedere [script U-SQL sviluppare utilizzando Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="0c6e2-175">toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="0c6e2-176">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="0c6e2-177">tooget una panoramica del Data Lake Analitica, vedere [Panoramica di Azure Data Lake Analitica](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c6e2-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="0c6e2-178">toosee hello stesso esercitazione con altri strumenti, fare clic sui selettori di hello scheda nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="0c6e2-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

