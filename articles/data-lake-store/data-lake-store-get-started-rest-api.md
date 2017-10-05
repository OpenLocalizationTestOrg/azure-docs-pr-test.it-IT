---
title: Usare l'API REST per iniziare a usare Data Lake Store | Documentazione Microsoft
description: Usare API REST WebHDFS per eseguire operazioni su Archivio Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: dc2c8f58e0a2faf1b00f4903148328a5141a8637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="55b18-103">Introduzione ad Archivio Azure Data Lake con API REST</span><span class="sxs-lookup"><span data-stu-id="55b18-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55b18-104">Portale</span><span class="sxs-lookup"><span data-stu-id="55b18-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="55b18-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55b18-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="55b18-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="55b18-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="55b18-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="55b18-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="55b18-108">API REST</span><span class="sxs-lookup"><span data-stu-id="55b18-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="55b18-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="55b18-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="55b18-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="55b18-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="55b18-111">Python</span><span class="sxs-lookup"><span data-stu-id="55b18-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="55b18-112">Questo articolo descrive come usare le API REST WebHDFS e le API REST di Archivio Data Lake per eseguire la gestione dell'account e le operazioni del file system su Archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="55b18-112">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="55b18-113">Archivio Azure Data Lake espone le proprie API REST per operazioni di gestione account.</span><span class="sxs-lookup"><span data-stu-id="55b18-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="55b18-114">Tuttavia, dal momento che Archivio Data Lake è compatibile con l'ecosistema Hadoop e HDFS, supporta le operazioni del file system tramite le API REST WebHDFS.</span><span class="sxs-lookup"><span data-stu-id="55b18-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="55b18-115">Per informazioni dettagliate sul supporto delle API REST per Archivio Data Lake, vedere [Informazioni di riferimento sulle API REST di Archivio Azure Data Lake](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="55b18-115">For detailed information on the REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="55b18-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="55b18-116">Prerequisites</span></span>
* <span data-ttu-id="55b18-117">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="55b18-117">**An Azure subscription**.</span></span> <span data-ttu-id="55b18-118">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55b18-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="55b18-119">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55b18-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="55b18-120">Usare l'applicazione Azure AD per autenticare l'applicazione Data Lake Store con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55b18-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="55b18-121">Per l'autenticazione con Azure AD è possibile usare l'**autenticazione dell'utente finale** o l'**autenticazione da servizio a servizio**.</span><span class="sxs-lookup"><span data-stu-id="55b18-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="55b18-122">Per altre informazioni e istruzioni su come eseguire l'autenticazione, vedere [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticazione da servizio a servizio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="55b18-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="55b18-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="55b18-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="55b18-124">Questo articolo usa cURL per illustrare come effettuare chiamate API REST con un account Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="55b18-124">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="55b18-125">Come si esegue l'autenticazione tramite Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55b18-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="55b18-126">È possibile adottare due approcci per l'autenticazione tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="55b18-126">You can use two approaches to authenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="55b18-127">Autenticazione dell'utente finale (interattiva)</span><span class="sxs-lookup"><span data-stu-id="55b18-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="55b18-128">In questo scenario, l'applicazione richiede all'utente di accedere e tutte le operazioni vengono eseguite nel contesto utente.</span><span class="sxs-lookup"><span data-stu-id="55b18-128">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="55b18-129">Eseguire la procedura seguente per l'autenticazione interattiva.</span><span class="sxs-lookup"><span data-stu-id="55b18-129">Perform the following steps for interactive authentication.</span></span>

1. <span data-ttu-id="55b18-130">Tramite l'applicazione, reindirizzare l'utente all'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-130">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="55b18-131">\<REDIRECT-URI> deve essere codificato per essere usato in un URL.</span><span class="sxs-lookup"><span data-stu-id="55b18-131">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="55b18-132">Per https://localhost, usare quindi `https%3A%2F%2Flocalhost`</span><span class="sxs-lookup"><span data-stu-id="55b18-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="55b18-133">Per questa esercitazione, è possibile sostituire i valori segnaposto nell'URL precedente e incollare quest'ultimo nella barra degli indirizzi di un web browser.</span><span class="sxs-lookup"><span data-stu-id="55b18-133">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="55b18-134">Si verrà reindirizzati per l'autenticazione tramite l'accesso ad Azure.</span><span class="sxs-lookup"><span data-stu-id="55b18-134">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="55b18-135">Dopo aver eseguito correttamente l'accesso, la risposta verrà visualizzata nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="55b18-135">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="55b18-136">La risposta sarà nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-136">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="55b18-137">Acquisire il codice di autorizzazione dalla risposta.</span><span class="sxs-lookup"><span data-stu-id="55b18-137">Capture the authorization code from the response.</span></span> <span data-ttu-id="55b18-138">Per questa esercitazione, è possibile copiare il codice di autorizzazione dalla barra degli indirizzi del web browser e passarla nella richiesta POST all'endpoint di token come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="55b18-138">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="55b18-139">In questo caso non è necessario codificare \<REDIRECT-URI>.</span><span class="sxs-lookup"><span data-stu-id="55b18-139">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="55b18-140">La risposta è un oggetto JSON che contiene un token di accesso (ad esempio, `"access_token": "<ACCESS_TOKEN>"`) e un token di aggiornamento (ad esempio, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="55b18-140">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="55b18-141">L'applicazione usa il token di accesso quando si accede all'Archivio Azure Data Lake e il token di aggiornamento quando un token di accesso scade per ottenerne un altro.</span><span class="sxs-lookup"><span data-stu-id="55b18-141">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="55b18-142">Quando il token di accesso scade, è possibile richiederne uno nuovo tramite il token di aggiornamento come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="55b18-142">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="55b18-143">Per altre informazioni sull'autenticazione utente interattiva, vedere [Flusso di concessione del codice di autorizzazione](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="55b18-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="55b18-144">Autenticazione da servizio a servizio (non interattiva)</span><span class="sxs-lookup"><span data-stu-id="55b18-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="55b18-145">In questo scenario, l'applicazione fornisce le proprie credenziali per eseguire le operazioni.</span><span class="sxs-lookup"><span data-stu-id="55b18-145">In this scenario, the the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="55b18-146">A tale scopo, è necessario inviare una richiesta POST come quella riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="55b18-146">For this, you must issue a POST request like the one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="55b18-147">L'output della richiesta include un token di autorizzazione (indicato da `access-token` nell'output riportato di seguito) che verrà passato successivamente con le chiamate API REST.</span><span class="sxs-lookup"><span data-stu-id="55b18-147">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="55b18-148">Salvare questo token di autenticazione in un file di testo, che sarà necessario più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="55b18-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="55b18-149">Questo articolo usa l'approccio **non interattivo** .</span><span class="sxs-lookup"><span data-stu-id="55b18-149">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="55b18-150">Per altre informazioni sull'autenticazione non interattiva (chiamate da servizio a servizio), vedere [Chiamate da servizio a servizio tramite le credenziali](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="55b18-150">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="55b18-151">Creare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="55b18-152">Questa operazione si basa sulla chiamata API REST definita [qui](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="55b18-152">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="55b18-153">Usare il comando cURL seguente.</span><span class="sxs-lookup"><span data-stu-id="55b18-153">Use the following cURL command.</span></span> <span data-ttu-id="55b18-154">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="55b18-155">Nel comando sopra sostituire \<`REDACTED`\> con il token di autorizzazione recuperato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="55b18-155">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="55b18-156">Il payload della richiesta per questo comando è contenuto nel file **input.json** fornito per il parametro `-d` precedente.</span><span class="sxs-lookup"><span data-stu-id="55b18-156">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="55b18-157">Il contenuto del file input.json è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-157">The contents of the input.json file resemble the following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="55b18-158">Creare delle cartelle in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="55b18-159">Questa operazione si basa sulla chiamata API REST WebHDFS definita [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="55b18-159">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="55b18-160">Usare il comando cURL seguente.</span><span class="sxs-lookup"><span data-stu-id="55b18-160">Use the following cURL command.</span></span> <span data-ttu-id="55b18-161">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="55b18-162">Nel comando sopra sostituire \<`REDACTED`\> con il token di autorizzazione recuperato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="55b18-162">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="55b18-163">Questo comando crea una directory denominata **mytempdir** nella cartella radice del proprio account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-163">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="55b18-164">Se l'operazione viene completata correttamente, verrà visualizzata una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-164">You should see a response like this if the operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="55b18-165">Elencare le cartelle in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="55b18-166">Questa operazione si basa sulla chiamata API REST WebHDFS definita [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="55b18-166">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="55b18-167">Usare il comando cURL seguente.</span><span class="sxs-lookup"><span data-stu-id="55b18-167">Use the following cURL command.</span></span> <span data-ttu-id="55b18-168">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="55b18-169">Nel comando sopra sostituire \<`REDACTED`\> con il token di autorizzazione recuperato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="55b18-169">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="55b18-170">Se l'operazione viene completata correttamente, verrà visualizzata una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-170">You should see a response like this if the operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="55b18-171">Caricare dati in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="55b18-172">Questa operazione si basa sulla chiamata API REST WebHDFS definita [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="55b18-172">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="55b18-173">Usare il comando cURL seguente.</span><span class="sxs-lookup"><span data-stu-id="55b18-173">Use the following cURL command.</span></span> <span data-ttu-id="55b18-174">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="55b18-175">Nella sintassi precedente il parametro **-T** indica la posizione del file da caricare.</span><span class="sxs-lookup"><span data-stu-id="55b18-175">In the above syntax **-T** parameter is the location of the file you are uploading.</span></span>

<span data-ttu-id="55b18-176">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-176">The output is similar to the following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="55b18-177">Leggere i dati da un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="55b18-178">Questa operazione si basa sulla chiamata API REST WebHDFS definita [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="55b18-178">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="55b18-179">La lettura dei dati da un account Archivio Data Lake è un processo in due fasi.</span><span class="sxs-lookup"><span data-stu-id="55b18-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="55b18-180">È prima necessario inviare una richiesta GET all'endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="55b18-180">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="55b18-181">Verrà restituito un percorso a cui inviare la richiesta GET successiva.</span><span class="sxs-lookup"><span data-stu-id="55b18-181">This will return a location to submit the next GET request to.</span></span>
* <span data-ttu-id="55b18-182">È quindi necessario inviare la richiesta GET all'endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="55b18-182">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="55b18-183">Verrà visualizzato il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="55b18-183">This will display the contents of the file.</span></span>

<span data-ttu-id="55b18-184">Tuttavia, dal momento che non esiste alcuna differenza nei parametri di input tra il primo e il secondo passaggio, è possibile usare il parametro `-L` per inviare la prima richiesta.</span><span class="sxs-lookup"><span data-stu-id="55b18-184">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="55b18-185">`-L` combina essenzialmente due richieste in una e fa ripetere a cURL la richiesta nel nuovo percorso.</span><span class="sxs-lookup"><span data-stu-id="55b18-185">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span></span> <span data-ttu-id="55b18-186">Infine, viene visualizzato l'output di tutte le chiamate di richiesta, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="55b18-186">Finally, the output from all the request calls is displayed, like shown below.</span></span> <span data-ttu-id="55b18-187">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="55b18-188">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-188">You should see an output similar to the following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="55b18-189">Rinominare un file in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="55b18-190">Questa operazione si basa sulla chiamata API REST WebHDFS definita [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="55b18-190">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="55b18-191">Per rinominare un file, usare il comando cURL seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-191">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="55b18-192">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="55b18-193">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-193">You should see an output similar to the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="55b18-194">Eliminare un file da un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="55b18-195">Questa operazione si basa sulla chiamata API REST WebHDFS definita [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="55b18-195">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="55b18-196">Utilizzare il comando cURL seguente per eliminare un file.</span><span class="sxs-lookup"><span data-stu-id="55b18-196">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="55b18-197">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="55b18-198">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-198">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="55b18-199">Eliminare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="55b18-200">Questa operazione si basa sulla chiamata API REST definita [qui](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="55b18-200">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="55b18-201">Usare il comando cURL seguente per eliminare un account Archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="55b18-201">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="55b18-202">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55b18-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="55b18-203">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="55b18-203">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="55b18-204">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="55b18-204">See also</span></span>
* [<span data-ttu-id="55b18-205">Aprire le applicazioni Big Data di origine che funzionano con Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="55b18-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

