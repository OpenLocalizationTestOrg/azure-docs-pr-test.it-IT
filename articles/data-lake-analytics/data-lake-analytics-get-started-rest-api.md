---
title: Introduzione a Data Lake Analytics con API REST| Documentazione Microsoft
description: Usare API REST WebHDFS per eseguire operazioni su Data Lake Analytics
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
ms.openlocfilehash: 332d7af2539eea8890745005104ac5b0921c2b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="83042-103">Introduzione ad Azure Data Lake Analytics con API REST</span><span class="sxs-lookup"><span data-stu-id="83042-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="83042-104">Informazioni sull'uso delle API REST WebHDFS e delle API REST di Data Lake Analytics per gestire gli account, i processi e il catalogo di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="83042-104">Learn how to use WebHDFS REST APIs and Data Lake Analytics REST APIs to manage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="83042-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="83042-105">Prerequisites</span></span>
* <span data-ttu-id="83042-106">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="83042-106">**An Azure subscription**.</span></span> <span data-ttu-id="83042-107">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83042-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="83042-108">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83042-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="83042-109">Usare l'applicazione Azure AD per autenticare l'applicazione Data Lake Analytics con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83042-109">You use the Azure AD application to authenticate the Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="83042-110">Per l'autenticazione con Azure AD è possibile usare l'**autenticazione dell'utente finale** o l'**autenticazione da servizio a servizio**.</span><span class="sxs-lookup"><span data-stu-id="83042-110">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="83042-111">Per altre informazioni e istruzioni su come eseguire l'autenticazione, vedere [Eseguire l'autenticazione con Data Lake Analytics usando Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="83042-111">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="83042-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="83042-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="83042-113">Questo articolo usa cURL per illustrare come eseguire chiamate API REST su un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="83042-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="83042-114">Eseguire l'autenticazione con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83042-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="83042-115">Per l'autenticazione con Azure Active Directory è possibile procedere in due modi.</span><span class="sxs-lookup"><span data-stu-id="83042-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="83042-116">Autenticazione dell'utente finale (interattiva)</span><span class="sxs-lookup"><span data-stu-id="83042-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="83042-117">Con questo metodo, l'applicazione richiede all'utente di accedere e tutte le operazioni vengono eseguite nel contesto utente.</span><span class="sxs-lookup"><span data-stu-id="83042-117">Using this method, application prompts the user to log in and all the operations are performed in the context of the user.</span></span> 

<span data-ttu-id="83042-118">Eseguire questa procedura per l'autenticazione interattiva:</span><span class="sxs-lookup"><span data-stu-id="83042-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="83042-119">Tramite l'applicazione, reindirizzare l'utente all'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="83042-119">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="83042-120">\<REDIRECT-URI> deve essere codificato per essere usato in un URL.</span><span class="sxs-lookup"><span data-stu-id="83042-120">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="83042-121">Per https://localhost, usare quindi `https%3A%2F%2Flocalhost`</span><span class="sxs-lookup"><span data-stu-id="83042-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="83042-122">Per questa esercitazione, è possibile sostituire i valori segnaposto nell'URL precedente e incollare quest'ultimo nella barra degli indirizzi di un web browser.</span><span class="sxs-lookup"><span data-stu-id="83042-122">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="83042-123">Si verrà reindirizzati per l'autenticazione tramite l'accesso ad Azure.</span><span class="sxs-lookup"><span data-stu-id="83042-123">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="83042-124">Dopo aver eseguito correttamente l'accesso, la risposta verrà visualizzata nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="83042-124">Once you succesfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="83042-125">La risposta sarà nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="83042-125">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="83042-126">Acquisire il codice di autorizzazione dalla risposta.</span><span class="sxs-lookup"><span data-stu-id="83042-126">Capture the authorization code from the response.</span></span> <span data-ttu-id="83042-127">Per questa esercitazione, è possibile copiare il codice di autorizzazione dalla barra degli indirizzi del web browser e passarla nella richiesta POST all'endpoint di token come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="83042-127">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="83042-128">In questo caso non è necessario codificare \<REDIRECT-URI>.</span><span class="sxs-lookup"><span data-stu-id="83042-128">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="83042-129">La risposta è un oggetto JSON che contiene un token di accesso (ad esempio, `"access_token": "<ACCESS_TOKEN>"`) e un token di aggiornamento (ad esempio, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="83042-129">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="83042-130">L'applicazione usa il token di accesso quando si accede all'Archivio Azure Data Lake e il token di aggiornamento quando un token di accesso scade per ottenerne un altro.</span><span class="sxs-lookup"><span data-stu-id="83042-130">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="83042-131">Quando il token di accesso scade, è possibile richiederne uno nuovo tramite il token di aggiornamento come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="83042-131">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="83042-132">Per altre informazioni sull'autenticazione utente interattiva, vedere [Flusso di concessione del codice di autorizzazione](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="83042-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="83042-133">Autenticazione da servizio a servizio (non interattiva)</span><span class="sxs-lookup"><span data-stu-id="83042-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="83042-134">Con questo metodo, l'applicazione fornisce le proprie credenziali per eseguire le operazioni.</span><span class="sxs-lookup"><span data-stu-id="83042-134">Using this method, application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="83042-135">A tale scopo è necessario inviare una richiesta POST come la seguente:</span><span class="sxs-lookup"><span data-stu-id="83042-135">For this, you must issue a POST request like the one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="83042-136">L'output della richiesta include un token di autorizzazione (indicato da `access-token` nell'output riportato di seguito) che verrà passato successivamente con le chiamate API REST.</span><span class="sxs-lookup"><span data-stu-id="83042-136">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="83042-137">Salvare questo token di autenticazione in un file di testo, che sarà necessario più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="83042-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="83042-138">Questo articolo usa l'approccio **non interattivo** .</span><span class="sxs-lookup"><span data-stu-id="83042-138">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="83042-139">Per altre informazioni sull'autenticazione non interattiva (chiamate da servizio a servizio), vedere [Chiamate da servizio a servizio tramite le credenziali](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="83042-139">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="83042-140">Creare un account di Analisi Data Lake</span><span class="sxs-lookup"><span data-stu-id="83042-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="83042-141">È necessario creare un gruppo di risorse di Azure e un account Data Lake Store prima di poter creare un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="83042-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="83042-142">Vedere [Creare un account Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="83042-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="83042-143">Il comando Curl seguente illustra come creare un account:</span><span class="sxs-lookup"><span data-stu-id="83042-143">The following Curl command shows how to create an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="83042-144">Sostituire \<`REDACTED`\> con il token di autorizzazione, \<`AzureSubscriptionID`\> con l'ID sottoscrizione, \<`AzureResourceGroupName`\> con il nome di un gruppo di risorse di Azure esistente e \<`NewAzureDataLakeAnalyticsAccountName`\> con il nome di un nuovo account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="83042-144">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="83042-145">Il payload della richiesta per questo comando è contenuto nel file **CreateDatalakeAnalyticsAccountRequest.json** specificato per il parametro `-d` precedente.</span><span class="sxs-lookup"><span data-stu-id="83042-145">The request payload for this command is contained in the **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="83042-146">Il contenuto del file input.json è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="83042-146">The contents of the input.json file resemble the following:</span></span>

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="83042-147">Elencare gli account di Data Lake Analytics in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="83042-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="83042-148">Il comando Curl seguente illustra come elencare gli account in una sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="83042-148">The following Curl command shows how to list accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="83042-149">Sostituire \<`REDACTED`\> con il token di autorizzazione e \<`AzureSubscriptionID`\> con l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="83042-149">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="83042-150">L'output è simile a:</span><span class="sxs-lookup"><span data-stu-id="83042-150">The output is similar to:</span></span>

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

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="83042-151">Ottenere informazioni su un account Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="83042-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="83042-152">Il comando Curl seguente illustra come ottenere informazioni su un account:</span><span class="sxs-lookup"><span data-stu-id="83042-152">The following Curl command shows how to get an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="83042-153">Sostituire \<`REDACTED`\> con il token di autorizzazione, \<`AzureSubscriptionID`\> con l'ID sottoscrizione, \<`AzureResourceGroupName`\> con il nome di un gruppo di risorse di Azure esistente e \<`DataLakeAnalyticsAccountName`\> con il nome di un account Data Lake Analytics esistente.</span><span class="sxs-lookup"><span data-stu-id="83042-153">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="83042-154">L'output è simile a:</span><span class="sxs-lookup"><span data-stu-id="83042-154">The output is similar to:</span></span>

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="83042-155">Elencare gli archivi Data Lake di account Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="83042-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="83042-156">Il comando Curl seguente illustra come elencare gli archivi Data Lake di un account:</span><span class="sxs-lookup"><span data-stu-id="83042-156">The following Curl command shows how to list Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="83042-157">Sostituire \<`REDACTED`\> con il token di autorizzazione, \<`AzureSubscriptionID`\> con l'ID sottoscrizione, \<`AzureResourceGroupName`\> con il nome di un gruppo di risorse di Azure esistente e \<`DataLakeAnalyticsAccountName`\> con il nome di un account Data Lake Analytics esistente.</span><span class="sxs-lookup"><span data-stu-id="83042-157">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="83042-158">L'output è simile a:</span><span class="sxs-lookup"><span data-stu-id="83042-158">The output is similar to:</span></span>

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

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="83042-159">Inviare processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="83042-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="83042-160">Il comando Curl seguente illustra come inviare un processo U-SQL:</span><span class="sxs-lookup"><span data-stu-id="83042-160">The following Curl command shows how to submit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="83042-161">Sostituire \<`REDACTED`\> con il token di autorizzazione e \<`DataLakeAnalyticsAccountName`\> con il nome di un account Data Lake Analytics esistente.</span><span class="sxs-lookup"><span data-stu-id="83042-161">Replace \<`REDACTED`\> with the authorization token, \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="83042-162">Il payload della richiesta per questo comando è contenuto nel file **SubmitADLAJob.json** fornito per il parametro `-d` indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="83042-162">The request payload for this command is contained in the **SubmitADLAJob.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="83042-163">Il contenuto del file input.json è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="83042-163">The contents of the input.json file resemble the following:</span></span>

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
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    TO \"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="83042-164">L'output è simile a:</span><span class="sxs-lookup"><span data-stu-id="83042-164">The output is similar to:</span></span>

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


## <a name="list-u-sql-jobs"></a><span data-ttu-id="83042-165">Elencare i processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="83042-165">List U-SQL jobs</span></span>
<span data-ttu-id="83042-166">Il comando Curl seguente illustra come elencare i processi U-SQL:</span><span class="sxs-lookup"><span data-stu-id="83042-166">The following Curl command shows how to list U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="83042-167">Sostituire \<`REDACTED`\> con il token di autorizzazione e \<`DataLakeAnalyticsAccountName`\> con il nome di un account Data Lake Analytics esistente.</span><span class="sxs-lookup"><span data-stu-id="83042-167">Replace \<`REDACTED`\> with the authorization token, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="83042-168">L'output è simile a:</span><span class="sxs-lookup"><span data-stu-id="83042-168">The output is similar to:</span></span>

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


## <a name="get-catalog-items"></a><span data-ttu-id="83042-169">Ottenere gli elementi del catalogo</span><span class="sxs-lookup"><span data-stu-id="83042-169">Get catalog items</span></span>
<span data-ttu-id="83042-170">Il comando Curl seguente illustra come ottenere i database dal catalogo:</span><span class="sxs-lookup"><span data-stu-id="83042-170">The following Curl command shows how to get the databases from the catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="83042-171">L'output è simile a:</span><span class="sxs-lookup"><span data-stu-id="83042-171">The output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="83042-172">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="83042-172">See also</span></span>
* <span data-ttu-id="83042-173">Per visualizzare una query più complessa, vedere [Analizzare i log del sito Web mediante Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="83042-173">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="83042-174">Per iniziare a sviluppare applicazioni U-SQL, vedere [Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83042-174">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="83042-175">Per informazioni su U-SQL, vedere [Introduzione al linguaggio U-SQL di Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83042-175">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="83042-176">Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="83042-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="83042-177">Per una panoramica su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83042-177">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="83042-178">Per visualizzare la stessa esercitazione usando altri strumenti, scegliere i selettori di scheda nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="83042-178">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>

