---
title: aaaUse hello API REST tooget avviato con l'archivio Data Lake | Documenti Microsoft
description: Utilizzare le API REST WebHDFS tooperform operazioni in archivio Data Lake
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
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="8b149-103">Introduzione ad Archivio Azure Data Lake con API REST</span><span class="sxs-lookup"><span data-stu-id="8b149-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b149-104">Portale</span><span class="sxs-lookup"><span data-stu-id="8b149-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="8b149-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b149-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="8b149-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="8b149-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="8b149-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="8b149-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="8b149-108">API REST</span><span class="sxs-lookup"><span data-stu-id="8b149-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="8b149-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8b149-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="8b149-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="8b149-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="8b149-111">Python</span><span class="sxs-lookup"><span data-stu-id="8b149-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="8b149-112">In questo articolo si apprenderà come account toouse WebHDFS REST API e le API REST di Data Lake archivio tooperform gestione nonché operazioni di file System in archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b149-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="8b149-113">Archivio Azure Data Lake espone le proprie API REST per operazioni di gestione account.</span><span class="sxs-lookup"><span data-stu-id="8b149-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="8b149-114">Tuttavia, dal momento che Archivio Data Lake è compatibile con l'ecosistema Hadoop e HDFS, supporta le operazioni del file system tramite le API REST WebHDFS.</span><span class="sxs-lookup"><span data-stu-id="8b149-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="8b149-115">Per informazioni dettagliate sul supporto di API REST hello per archivio Data Lake, vedere [Azure Data Lake archivio REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b149-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8b149-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b149-116">Prerequisites</span></span>
* <span data-ttu-id="8b149-117">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8b149-117">**An Azure subscription**.</span></span> <span data-ttu-id="8b149-118">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b149-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8b149-119">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b149-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="8b149-120">Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello archivio Data Lake con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b149-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="8b149-121">Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**.</span><span class="sxs-lookup"><span data-stu-id="8b149-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="8b149-122">Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8b149-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="8b149-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="8b149-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="8b149-124">In questo articolo Usa toodemonstrate cURL come toomake API REST chiama rispetto a un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b149-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="8b149-125">Come si esegue l'autenticazione tramite Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b149-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="8b149-126">È possibile utilizzare due approcci tooauthenticate, tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8b149-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="8b149-127">Autenticazione dell'utente finale (interattiva)</span><span class="sxs-lookup"><span data-stu-id="8b149-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="8b149-128">In questo scenario, l'applicazione hello chiede toolog utente hello in e tutte le operazioni hello vengono eseguite nel contesto di hello dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="8b149-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="8b149-129">Eseguire hello alla procedura seguente per l'autenticazione interattiva.</span><span class="sxs-lookup"><span data-stu-id="8b149-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="8b149-130">Tramite l'applicazione, il reindirizzamento hello utente toohello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="8b149-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="8b149-131">\<URI di reindirizzamento > deve toobe codificati per l'uso in un URL.</span><span class="sxs-lookup"><span data-stu-id="8b149-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="8b149-132">Per https://localhost, usare quindi `https%3A%2F%2Flocalhost`</span><span class="sxs-lookup"><span data-stu-id="8b149-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="8b149-133">A scopo di hello di questa esercitazione, è possibile sostituire i valori segnaposto hello nell'URL hello in precedenza e incollarlo nella barra degli indirizzi del web browser.</span><span class="sxs-lookup"><span data-stu-id="8b149-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="8b149-134">Sarà reindirizzato tooauthenticate utilizzando l'account di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b149-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="8b149-135">Una volta che riesce ad accedere, risposta hello viene visualizzato nella barra degli indirizzi del browser hello.</span><span class="sxs-lookup"><span data-stu-id="8b149-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="8b149-136">risposta Hello sarà in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="8b149-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="8b149-137">Acquisire il codice di autorizzazione hello dalla risposta hello.</span><span class="sxs-lookup"><span data-stu-id="8b149-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="8b149-138">Per questa esercitazione, è possibile copiare il codice di autorizzazione hello dalla barra degli indirizzi del browser web hello hello e passarlo in hello POST richiesta toohello endpoint token, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8b149-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="8b149-139">In questo caso, hello \<URI di reindirizzamento > non devono essere codificati.</span><span class="sxs-lookup"><span data-stu-id="8b149-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="8b149-140">risposta Hello è un oggetto JSON che contiene un token di accesso (ad esempio, `"access_token": "<ACCESS_TOKEN>"`) e un token di aggiornamento (ad esempio, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="8b149-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="8b149-141">L'applicazione utilizza il token di accesso di hello quando si accede a un archivio Azure Data Lake e hello aggiornamento token tooget un altro token di accesso quando scade un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="8b149-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="8b149-142">Quando il token di accesso hello scade, è possibile richiedere un nuovo token di accesso usando il token di aggiornamento di hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8b149-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="8b149-143">Per altre informazioni sull'autenticazione utente interattiva, vedere [Flusso di concessione del codice di autorizzazione](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b149-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="8b149-144">Autenticazione da servizio a servizio (non interattiva)</span><span class="sxs-lookup"><span data-stu-id="8b149-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="8b149-145">In questo scenario, un'applicazione hello hello fornisce operazioni hello tooperform le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="8b149-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="8b149-146">A tale scopo, è necessario inviare una richiesta POST come hello illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8b149-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="8b149-147">output di Hello della richiesta includerà un token di autorizzazione (indicato da `access-token` nell'output di hello riportato di seguito) che verranno successivamente passati con le chiamate API REST.</span><span class="sxs-lookup"><span data-stu-id="8b149-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="8b149-148">Salvare questo token di autenticazione in un file di testo, che sarà necessario più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8b149-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="8b149-149">Questo articolo Usa hello **interattivo** approccio.</span><span class="sxs-lookup"><span data-stu-id="8b149-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="8b149-150">Per ulteriori informazioni sulle modalità interattiva (chiamate service to service), vedere [tooservice chiamate utilizzando le credenziali del servizio](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b149-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="8b149-151">Creare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="8b149-152">Questa operazione è basata su chiamata API REST hello definito [qui](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b149-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="8b149-153">Utilizzare hello cURL comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8b149-153">Use hello following cURL command.</span></span> <span data-ttu-id="8b149-154">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b149-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="8b149-155">In hello in precedenza di comando, sostituire \< `REDACTED` \> con token di autorizzazione hello recuperati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8b149-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="8b149-156">payload della richiesta Hello per questo comando è contenuto in hello **input.json** file fornito per hello `-d` parametro precedente.</span><span class="sxs-lookup"><span data-stu-id="8b149-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="8b149-157">il contenuto di Hello del file input.json hello nella figura seguente hello:</span><span class="sxs-lookup"><span data-stu-id="8b149-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="8b149-158">Creare delle cartelle in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="8b149-159">Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="8b149-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="8b149-160">Utilizzare hello cURL comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8b149-160">Use hello following cURL command.</span></span> <span data-ttu-id="8b149-161">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b149-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="8b149-162">In hello in precedenza di comando, sostituire \< `REDACTED` \> con token di autorizzazione hello recuperati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8b149-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="8b149-163">Questo comando crea una directory denominata **mytempdir** nella cartella radice hello del tuo account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b149-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="8b149-164">Se il completamento dell'operazione hello dovrebbe essere una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="8b149-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="8b149-165">Elencare le cartelle in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="8b149-166">Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="8b149-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="8b149-167">Utilizzare hello cURL comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8b149-167">Use hello following cURL command.</span></span> <span data-ttu-id="8b149-168">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b149-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="8b149-169">In hello in precedenza di comando, sostituire \< `REDACTED` \> con token di autorizzazione hello recuperati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8b149-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="8b149-170">Se il completamento dell'operazione hello dovrebbe essere una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="8b149-170">You should see a response like this if hello operation completes successfully:</span></span>

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

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="8b149-171">Caricare dati in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="8b149-172">Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="8b149-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="8b149-173">Utilizzare hello cURL comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8b149-173">Use hello following cURL command.</span></span> <span data-ttu-id="8b149-174">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b149-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="8b149-175">In hello sopra sintassi **-T** parametro è il percorso di hello si sta caricando file hello.</span><span class="sxs-lookup"><span data-stu-id="8b149-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="8b149-176">output di Hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b149-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="8b149-177">Leggere i dati da un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="8b149-178">Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="8b149-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="8b149-179">La lettura dei dati da un account Archivio Data Lake è un processo in due fasi.</span><span class="sxs-lookup"><span data-stu-id="8b149-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="8b149-180">È prima di inviare una richiesta GET endpoint hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="8b149-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="8b149-181">Verrà restituito una percorso toosubmit hello GET richiesta successiva.</span><span class="sxs-lookup"><span data-stu-id="8b149-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="8b149-182">È quindi inviare la richiesta di recupero hello endpoint hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="8b149-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="8b149-183">Verrà visualizzato il contenuto di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="8b149-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="8b149-184">Tuttavia, poiché non esiste alcuna differenza hello parametri di input tra hello hello e innanzitutto secondo passaggio, è possibile utilizzare hello `-L` parametro toosubmit hello della prima richiesta.</span><span class="sxs-lookup"><span data-stu-id="8b149-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="8b149-185">`-L`opzione essenzialmente combina due richieste in un e renderà cURL Ripeti richiesta hello nella nuova posizione hello.</span><span class="sxs-lookup"><span data-stu-id="8b149-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="8b149-186">Infine, hello output di tutte le chiamate richiesta hello viene visualizzato, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8b149-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="8b149-187">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b149-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="8b149-188">Verrà visualizzato un segue toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="8b149-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="8b149-189">Rinominare un file in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="8b149-190">Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="8b149-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="8b149-191">Seguente hello usare cURL comando toorename un file.</span><span class="sxs-lookup"><span data-stu-id="8b149-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="8b149-192">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b149-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="8b149-193">Verrà visualizzato un segue toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="8b149-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="8b149-194">Eliminare un file da un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="8b149-195">Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="8b149-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="8b149-196">Seguente hello usare cURL comando toodelete un file.</span><span class="sxs-lookup"><span data-stu-id="8b149-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="8b149-197">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b149-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="8b149-198">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="8b149-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="8b149-199">Eliminare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="8b149-200">Questa operazione è basata su chiamata API REST hello definito [qui](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b149-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="8b149-201">Seguente hello usare cURL comando toodelete un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b149-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="8b149-202">Sostituire **\<yourstorename>** con il nome di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b149-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="8b149-203">Verrà visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="8b149-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="8b149-204">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8b149-204">See also</span></span>
* [<span data-ttu-id="8b149-205">Aprire le applicazioni Big Data di origine che funzionano con Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b149-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

