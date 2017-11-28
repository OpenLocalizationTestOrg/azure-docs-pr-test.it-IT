---
title: tooget interfaccia aaaUse Azure 2.0 da riga di comando avviato con l'archivio Azure Data Lake | Documenti Microsoft
description: Utilizzare una riga di comando multipiattaforma di Azure 2.0 toocreate un account archivio Data Lake ed eseguire operazioni di base
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="918ef-103">Introduzione ad Azure Data Lake Store con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="918ef-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="918ef-104">Portale</span><span class="sxs-lookup"><span data-stu-id="918ef-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="918ef-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="918ef-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="918ef-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="918ef-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="918ef-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="918ef-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="918ef-108">API REST</span><span class="sxs-lookup"><span data-stu-id="918ef-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="918ef-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="918ef-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="918ef-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="918ef-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="918ef-111">Python</span><span class="sxs-lookup"><span data-stu-id="918ef-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="918ef-112">Informazioni sulla modalità di memorizzazione una Data Lake di Azure di toocreate toouse CLI di Azure 2.0 account e di eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati, eliminare l'account, e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="918ef-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="918ef-113">Hello Azure CLI 2.0 è una nuova esperienza della riga di comando di Azure per la gestione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="918ef-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="918ef-114">Può essere usata in macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="918ef-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="918ef-115">Per altre informazioni, vedere [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Panoramica dell'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="918ef-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="918ef-116">È anche possibile esaminare hello [riferimento di Azure Data Lake archivio CLI 2.0](https://docs.microsoft.com/cli/azure/dls) per un elenco completo di comandi e sintassi.</span><span class="sxs-lookup"><span data-stu-id="918ef-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="918ef-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="918ef-117">Prerequisites</span></span>
<span data-ttu-id="918ef-118">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="918ef-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="918ef-119">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="918ef-119">**An Azure subscription**.</span></span> <span data-ttu-id="918ef-120">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="918ef-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="918ef-121">**Interfaccia della riga di comando di Azure 2.0**: per istruzioni, vedere [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="918ef-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="918ef-122">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="918ef-122">Authentication</span></span>

<span data-ttu-id="918ef-123">Questo articolo usa un approccio di autenticazione più semplice con Data Lake Store in cui si accede come utente finale.</span><span class="sxs-lookup"><span data-stu-id="918ef-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="918ef-124">Hello accesso livello tooData Lake archivio account file system e quindi è disciplinato dal livello di accesso hello di hello utente connesso.</span><span class="sxs-lookup"><span data-stu-id="918ef-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="918ef-125">Tuttavia, esistono altri approcci come ben tooauthenticate con archivio Data Lake, che sono **autenticazione dell'utente finale** o **authentication service to service**.</span><span class="sxs-lookup"><span data-stu-id="918ef-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="918ef-126">Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="918ef-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="918ef-127">Accedi tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="918ef-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="918ef-128">Accedere alla propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="918ef-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="918ef-129">Si ottiene un codice toouse nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="918ef-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="918ef-130">Utilizzare un web browser tooopen hello pagina https://aka.ms/devicelogin e immettere tooauthenticate codice hello.</span><span class="sxs-lookup"><span data-stu-id="918ef-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="918ef-131">Si è toolog richiesta utilizzando le credenziali.</span><span class="sxs-lookup"><span data-stu-id="918ef-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="918ef-132">Quando si accede, tutti gli elenchi di finestra hello hello sottoscrizioni Azure in cui sono associate all'account.</span><span class="sxs-lookup"><span data-stu-id="918ef-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="918ef-133">Utilizzare hello successivo comando toouse una sottoscrizione specifica.</span><span class="sxs-lookup"><span data-stu-id="918ef-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="918ef-134">Creare un account di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="918ef-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="918ef-135">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="918ef-135">Create a new resource group.</span></span> <span data-ttu-id="918ef-136">Nel comando seguente di hello, fornire hello valori di parametro che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="918ef-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="918ef-137">Se il nome di percorso hello contiene spazi, è necessario inserirlo tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="918ef-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="918ef-138">Ad esempio "Stati Uniti orientali 2".</span><span class="sxs-lookup"><span data-stu-id="918ef-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="918ef-139">Creare account archivio Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="918ef-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="918ef-140">Creare delle cartelle in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="918ef-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="918ef-141">È possibile creare cartelle sotto la toomanage account archivio Azure Data Lake e archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="918ef-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="918ef-142">Hello utilizzo successivo comando toocreate una cartella denominata **mynewfolder** radice hello hello archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="918ef-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="918ef-143">Hello `--folder` parametro assicura che il comando hello crea una cartella.</span><span class="sxs-lookup"><span data-stu-id="918ef-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="918ef-144">Se questo parametro non è presente, il comando di hello crea un file vuoto denominato mynewfolder radice hello hello account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="918ef-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="918ef-145">Caricamento account archivio Data Lake tooa di dati</span><span class="sxs-lookup"><span data-stu-id="918ef-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="918ef-146">È possibile caricare l'archivio del data Lake tooData direttamente in hello livello o tooa cartella radice che è stato creato all'interno di account hello.</span><span class="sxs-lookup"><span data-stu-id="918ef-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="918ef-147">Hello i frammenti di codice riportato di seguito viene illustrato come tooupload cartella toohello alcuni dati di esempio (**mynewfolder**) creata nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="918ef-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="918ef-148">Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="918ef-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="918ef-149">Scaricare il file hello e archiviarlo in una directory locale nel computer in uso, ad esempio C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="918ef-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="918ef-150">Per la destinazione di hello, è necessario specificare percorso completo di hello compreso il nome del file hello.</span><span class="sxs-lookup"><span data-stu-id="918ef-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="918ef-151">Elencare i file in un account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="918ef-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="918ef-152">Utilizzare i seguenti comandi toolist hello file in un account archivio Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="918ef-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="918ef-153">output di Hello di questo oggetto deve essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="918ef-153">hello output of this should be similar toohello following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="918ef-154">Rinominare, scaricare ed eliminare i dati da un account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="918ef-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="918ef-155">**un file toorename**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="918ef-156">**un file toodownload**, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="918ef-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="918ef-157">Verificare che il percorso di destinazione hello specificato già esiste.</span><span class="sxs-lookup"><span data-stu-id="918ef-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="918ef-158">comando Hello Crea cartella di destinazione hello se non esiste.</span><span class="sxs-lookup"><span data-stu-id="918ef-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="918ef-159">**un file toodelete**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="918ef-160">Se si desidera toodelete hello cartella **mynewfolder** e file hello **vehicle1_09142014_copy.csv** insieme in un comando, utilizzare hello - recurse parametro</span><span class="sxs-lookup"><span data-stu-id="918ef-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="918ef-161">Utilizzare autorizzazioni ed elenchi di controllo di accesso per un account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="918ef-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="918ef-162">In questa sezione informazioni su come toomanage ACL e autorizzazioni mediante Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="918ef-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="918ef-163">Per una spiegazione dettagliata di come vengono implementati gli elenchi di controllo di accesso in Azure Data Lake Store, vedere [Controllo di accesso in Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="918ef-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="918ef-164">**proprietario hello tooupdate di una file o alla cartella**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="918ef-165">**le autorizzazioni di hello tooupdate per una file o alla cartella**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="918ef-166">**tooget hello ACL per un determinato percorso**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="918ef-167">output di Hello deve essere simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="918ef-167">hello output should be similar toohello following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="918ef-168">**una voce per un ACL tooset**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="918ef-169">**una voce per un ACL tooremove**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="918ef-170">**un ACL predefinito intero tooremove**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="918ef-171">**un ACL non predefinito intero tooremove**, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="918ef-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="918ef-172">Eliminare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="918ef-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="918ef-173">Utilizzare hello successivo comando toodelete un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="918ef-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="918ef-174">Quando richiesto, immettere **Y** account hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="918ef-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="918ef-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="918ef-175">Next steps</span></span>

* <span data-ttu-id="918ef-176">[Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) (Informazioni di riferimento sull'interfaccia della riga di comando di Azure Data Lake Store 2.0)</span><span class="sxs-lookup"><span data-stu-id="918ef-176">[Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls)</span></span>
* [<span data-ttu-id="918ef-177">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="918ef-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="918ef-178">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="918ef-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="918ef-179">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="918ef-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
