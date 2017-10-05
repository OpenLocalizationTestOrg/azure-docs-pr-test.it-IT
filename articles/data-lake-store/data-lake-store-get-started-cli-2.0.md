---
title: Usare l'interfaccia della riga di comando di Azure 2.0 per iniziare a usare Azure Data Lake Store | Microsoft Docs
description: Usare la riga di comando multipiattaforma di Azure 2.0 per creare un account di Data Lake Store ed eseguire operazioni di base
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
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="4bd32-103">Introduzione ad Azure Data Lake Store con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4bd32-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4bd32-104">Portale</span><span class="sxs-lookup"><span data-stu-id="4bd32-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="4bd32-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bd32-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="4bd32-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="4bd32-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="4bd32-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="4bd32-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="4bd32-108">API REST</span><span class="sxs-lookup"><span data-stu-id="4bd32-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="4bd32-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4bd32-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="4bd32-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="4bd32-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="4bd32-111">Python</span><span class="sxs-lookup"><span data-stu-id="4bd32-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="4bd32-112">Informazioni su come usare l'interfaccia della riga di comando di Azure 2.0 per creare un account di Azure Data Lake Store ed eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare i file di dati, eliminare l'account e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4bd32-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="4bd32-113">L'interfaccia della riga di comando di Azure 2.0 è la nuova esperienza della riga di comando di Azure per gestire le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd32-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="4bd32-114">Può essere usata in macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="4bd32-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="4bd32-115">Per altre informazioni, vedere [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Panoramica dell'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="4bd32-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="4bd32-116">Per un elenco completo di comandi e per la sintassi, è anche possibile vedere le [informazioni di riferimento sull'interfaccia della riga di comando di Azure Data Lake Store 2.0](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="4bd32-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4bd32-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4bd32-117">Prerequisites</span></span>
<span data-ttu-id="4bd32-118">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="4bd32-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="4bd32-119">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="4bd32-119">**An Azure subscription**.</span></span> <span data-ttu-id="4bd32-120">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4bd32-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="4bd32-121">**Interfaccia della riga di comando di Azure 2.0**: per istruzioni, vedere [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="4bd32-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="4bd32-122">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="4bd32-122">Authentication</span></span>

<span data-ttu-id="4bd32-123">Questo articolo usa un approccio di autenticazione più semplice con Data Lake Store in cui si accede come utente finale.</span><span class="sxs-lookup"><span data-stu-id="4bd32-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="4bd32-124">Il livello di accesso al file system e all'account Data Lake Store viene quindi regolato dal livello di accesso dell'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="4bd32-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="4bd32-125">Esistono tuttavia altri approcci oltre all'autenticazione con Data Lake Store, ad esempio l'**autenticazione dell'utente finale** o l'**autenticazione da servizio a servizio**.</span><span class="sxs-lookup"><span data-stu-id="4bd32-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="4bd32-126">Per altre informazioni e istruzioni su come eseguire l'autenticazione, vedere [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticazione da servizio a servizio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="4bd32-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="4bd32-127">Accedere alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="4bd32-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="4bd32-128">Accedere alla propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd32-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="4bd32-129">Si ottiene un codice da usare nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="4bd32-129">You get a code to use in the next step.</span></span> <span data-ttu-id="4bd32-130">Usare un Web browser per aprire la pagina https://aka.ms/devicelogin e immettere il codice per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4bd32-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="4bd32-131">Verrà chiesto di accedere usando le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="4bd32-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="4bd32-132">Dopo l'accesso, la finestra elenca tutte le sottoscrizioni di Azure associate all'account.</span><span class="sxs-lookup"><span data-stu-id="4bd32-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="4bd32-133">Usare il comando seguente per usare una sottoscrizione specifica.</span><span class="sxs-lookup"><span data-stu-id="4bd32-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="4bd32-134">Creare un account di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4bd32-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="4bd32-135">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="4bd32-135">Create a new resource group.</span></span> <span data-ttu-id="4bd32-136">Nel comando seguente, fornire i valori dei parametri da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="4bd32-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="4bd32-137">Se il nome del percorso contiene spazi, racchiuderlo tra virgolette doppie,</span><span class="sxs-lookup"><span data-stu-id="4bd32-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="4bd32-138">Ad esempio "Stati Uniti orientali 2".</span><span class="sxs-lookup"><span data-stu-id="4bd32-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="4bd32-139">Creare un account Data Lake Store di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd32-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="4bd32-140">Creare delle cartelle in un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="4bd32-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="4bd32-141">È possibile creare delle cartelle con il proprio account di Azure Data Lake Store per gestire e archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="4bd32-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="4bd32-142">Usare il comando seguente per creare una cartella denominata **mynewfolder** nella directory radice di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4bd32-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="4bd32-143">Il parametro `--folder` assicura che il comando crei una cartella.</span><span class="sxs-lookup"><span data-stu-id="4bd32-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="4bd32-144">Se questo parametro non è presente, il comando crea un file vuoto denominato mynewfolder nella radice dell'account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4bd32-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="4bd32-145">Caricare dati in un account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4bd32-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="4bd32-146">È possibile caricare dati in Data Lake Store direttamente a livello di radice o in una cartella creata nell'account.</span><span class="sxs-lookup"><span data-stu-id="4bd32-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="4bd32-147">I frammenti di codice riportati di seguito illustrano come caricare alcuni dati di esempio nella cartella (**mynewdirectory**) creata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="4bd32-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="4bd32-148">Se si stanno cercando dati di esempio da caricare, è possibile ottenere la cartella **Ambulance Data** dal [Repository GitHub per Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="4bd32-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="4bd32-149">Scaricare il file e archiviarlo in una directory locale nel computer, ad esempio C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="4bd32-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="4bd32-150">Per la destinazione, è necessario specificare il percorso completo, incluso il nome file.</span><span class="sxs-lookup"><span data-stu-id="4bd32-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="4bd32-151">Elencare i file in un account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4bd32-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="4bd32-152">Usare il comando seguente per elencare i file nell'account di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4bd32-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="4bd32-153">L'output di questo comando dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-153">The output of this should be similar to the following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="4bd32-154">Rinominare, scaricare ed eliminare i dati da un account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4bd32-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="4bd32-155">**Per rinominare un file**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="4bd32-156">**Per scaricare un file**, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="4bd32-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="4bd32-157">Assicurarsi che il percorso di destinazione specificato esista già.</span><span class="sxs-lookup"><span data-stu-id="4bd32-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="4bd32-158">Il comando crea la cartella di destinazione se non esiste.</span><span class="sxs-lookup"><span data-stu-id="4bd32-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="4bd32-159">**Per eliminare un file**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="4bd32-160">Per eliminare la cartella **mynewfolder** e il file **vehicle1_09142014_copy.csv** con un unico comando, usare il parametro --recurse.</span><span class="sxs-lookup"><span data-stu-id="4bd32-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="4bd32-161">Utilizzare autorizzazioni ed elenchi di controllo di accesso per un account Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4bd32-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="4bd32-162">Questa sezione illustra come gestire elenchi di controllo di accesso e autorizzazioni usando l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="4bd32-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="4bd32-163">Per una spiegazione dettagliata di come vengono implementati gli elenchi di controllo di accesso in Azure Data Lake Store, vedere [Controllo di accesso in Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="4bd32-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="4bd32-164">**Per aggiornare il proprietario di un file o di una cartella**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="4bd32-165">**Per aggiornare le autorizzazioni per un file o per una cartella**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="4bd32-166">**Per ottenere gli elenchi di controllo di accesso per un determinato percorso**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="4bd32-167">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-167">The output should be similar to the following:</span></span>

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

* <span data-ttu-id="4bd32-168">**Per impostare una voce per un elenco di controllo di accesso**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="4bd32-169">**Per rimuovere una voce per un elenco di controllo di accesso**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="4bd32-170">**Per rimuovere un intero elenco di controllo di accesso predefinito**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="4bd32-171">**Per rimuovere un intero elenco di controllo di accesso non predefinito**, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd32-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="4bd32-172">Eliminare un account Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="4bd32-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="4bd32-173">Usare il comando seguente per eliminare l'account di Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4bd32-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="4bd32-174">Quando viene richiesto, immettere **Y** per eliminare l'account.</span><span class="sxs-lookup"><span data-stu-id="4bd32-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bd32-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4bd32-175">Next steps</span></span>

* <span data-ttu-id="4bd32-176">[Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) (Informazioni di riferimento sull'interfaccia della riga di comando di Azure Data Lake Store 2.0)</span><span class="sxs-lookup"><span data-stu-id="4bd32-176">[Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls)</span></span>
* [<span data-ttu-id="4bd32-177">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4bd32-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="4bd32-178">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4bd32-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="4bd32-179">Usare Azure HDInsight con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4bd32-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
