---
title: Aggiungere altri account di Archiviazione di Azure a HDInsight | Documentazione Microsoft
description: Informazioni su come aggiungere altri account di Archiviazione di Azure a un cluster HDInsight esistente.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="611b1-103">Aggiungere altri account di archiviazione a HDInsight</span><span class="sxs-lookup"><span data-stu-id="611b1-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="611b1-104">Informazioni su come usare le azioni script per aggiungere altri account di archiviazione di Azure in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="611b1-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="611b1-105">Nella procedura descritta in questo documento viene aggiunto un account di archiviazione a un cluster HDInsight basato su Linux esistente.</span><span class="sxs-lookup"><span data-stu-id="611b1-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="611b1-106">Le informazioni in questo documento illustrano come aggiungere altre risorse di archiviazione a un cluster dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="611b1-107">Per informazioni sull'aggiunta di account di archiviazione durante la creazione del cluster, vedere [Configurare cluster in HDInsight con Hadoop, Spark, Kafka e altro](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="611b1-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="611b1-108">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="611b1-108">How it works</span></span>

<span data-ttu-id="611b1-109">Lo script accetta i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="611b1-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="611b1-110">__Nome dell'account di archiviazione di Azure__: nome dell'account di archiviazione da aggiungere al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="611b1-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="611b1-111">Dopo l'esecuzione dello script, HDInsight è in grado di leggere e scrivere i dati archiviati in questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="611b1-112">__Chiave dell'account di archiviazione di Azure__: chiave che concede l'accesso all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="611b1-113">__-p__ (facoltativo): se questo parametro è specificato, la chiave non viene crittografata e viene archiviata nel file core-site.xml come testo normale.</span><span class="sxs-lookup"><span data-stu-id="611b1-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="611b1-114">Durante l'elaborazione, lo script esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="611b1-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="611b1-115">Se la chiave dell'account di archiviazione esiste già nella configurazione del file core-site.xml per il cluster, lo script viene chiuso e non vengono eseguite altre azioni.</span><span class="sxs-lookup"><span data-stu-id="611b1-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="611b1-116">Verifica che l'account di archiviazione esista e sia accessibile tramite la chiave.</span><span class="sxs-lookup"><span data-stu-id="611b1-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="611b1-117">Crittografa la chiave mediante le credenziali del cluster,</span><span class="sxs-lookup"><span data-stu-id="611b1-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="611b1-118">Aggiunge l'account di archiviazione al file core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="611b1-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="611b1-119">Arresta e riavvia i servizi Oozie, YARN, MapReduce2 e Hadoop Distributed File System.</span><span class="sxs-lookup"><span data-stu-id="611b1-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="611b1-120">L'arresto e l'avvio di questi servizi consente di usare il nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="611b1-121">L'uso di un account di archiviazione in una località diversa rispetto al cluster HDInsight non è supportato.</span><span class="sxs-lookup"><span data-stu-id="611b1-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="611b1-122">Lo script</span><span class="sxs-lookup"><span data-stu-id="611b1-122">The script</span></span>

<span data-ttu-id="611b1-123">__Percorso dello script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="611b1-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="611b1-124">__Requisiti__:</span><span class="sxs-lookup"><span data-stu-id="611b1-124">__Requirements__:</span></span>

* <span data-ttu-id="611b1-125">Lo script deve essere applicato ai __nodi head__.</span><span class="sxs-lookup"><span data-stu-id="611b1-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="611b1-126">Per usare lo script</span><span class="sxs-lookup"><span data-stu-id="611b1-126">To use the script</span></span>

<span data-ttu-id="611b1-127">È possibile usare lo script tramite il portale di Azure, Azure PowerShell o l'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="611b1-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="611b1-128">Per altre informazioni, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster).</span><span class="sxs-lookup"><span data-stu-id="611b1-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="611b1-129">Nella procedura descritta nel documento di personalizzazione usare le informazioni seguenti per applicare questo script:</span><span class="sxs-lookup"><span data-stu-id="611b1-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="611b1-130">Sostituire l'URI di esempio dell'azione script con l'URI per questo script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="611b1-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="611b1-131">Sostituire eventuali parametri di esempio con il nome dell'account di archiviazione di Azure e la chiave dell'account di archiviazione da aggiungere al cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="611b1-132">Se si usa il portale di Azure, questi parametri devono essere separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="611b1-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="611b1-133">Non è necessario contrassegnare lo script come __Persistente__, perché aggiorna direttamente la configurazione Ambari per il cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="611b1-134">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="611b1-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="611b1-135">Account di archiviazione non visualizzati nel portale di Azure o negli strumenti</span><span class="sxs-lookup"><span data-stu-id="611b1-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="611b1-136">Quando si visualizza il cluster HDInsight nel Portale di Azure, selezionando la voce __Account di archiviazione__ in __Proprietà__ non vengono mostrati gli account di archiviazione aggiunti tramite questa azione script.</span><span class="sxs-lookup"><span data-stu-id="611b1-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="611b1-137">L'account di archiviazione aggiuntivo non viene inoltre visualizzato in Azure PowerShell e nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="611b1-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="611b1-138">Le informazioni di archiviazione non vengono mostrate perché lo script modifica solo la configurazione di core-site.xml per il cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="611b1-139">Queste informazioni non vengono usate durante il recupero delle informazioni del cluster tramite le API di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="611b1-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="611b1-140">Per visualizzare le informazioni sull'account di archiviazione aggiunte al cluster tramite lo script, usare l'API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="611b1-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="611b1-141">Usare i comandi seguenti per recuperare queste informazioni per il cluster:</span><span class="sxs-lookup"><span data-stu-id="611b1-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="611b1-142">Impostare `$clusterName` sul nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="611b1-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="611b1-143">Impostare `$storageAccountName` sul nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="611b1-144">Quando richiesto, immettere (admin) e password di accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="611b1-145">Impostare `$PASSWORD` sulla password dell'account (admin) di accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="611b1-146">Impostare `$CLUSTERNAME` sul nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="611b1-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="611b1-147">Impostare `$STORAGEACCOUNTNAME` sul nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="611b1-148">Queste esempio usa [curl (http://curl.haxx.se/)](http://curl.haxx.se/) e [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) per recuperare e analizzare i dati JSON.</span><span class="sxs-lookup"><span data-stu-id="611b1-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="611b1-149">Quando si usa questo comando, sostituire __CLUSTERNAME__ con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="611b1-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="611b1-150">Sostituire __PASSWORD__ con la password di accesso HTTP per il cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="611b1-151">Sostituire __STORAGEACCOUNT__ con il nome dell'account di archiviazione aggiunto usando l'azione script.</span><span class="sxs-lookup"><span data-stu-id="611b1-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="611b1-152">Le informazioni restituite da questo comando sono simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="611b1-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="611b1-153">Questo testo è un esempio di chiave crittografata, usata per accedere all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="611b1-154">Non è possibile accedere alla risorsa di archiviazione dopo la modifica della chiave</span><span class="sxs-lookup"><span data-stu-id="611b1-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="611b1-155">Se si modifica la chiave per un account di archiviazione, HDInsight non potrà più accedere all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="611b1-156">HDInsight usa una copia memorizzata nella cache della chiave in core-site.xml per il cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="611b1-157">Questa copia memorizzata nella cache deve essere aggiornata in modo che corrisponda alla nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="611b1-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="611b1-158">La ripetizione dell'esecuzione dell'azione script __non__ aggiorna la chiave, perché lo script verifica se esiste già una voce per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="611b1-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="611b1-159">Se esiste già una voce, non viene apportata alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="611b1-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="611b1-160">Per risolvere il problema, è necessario rimuovere la voce esistente per l'account di archiviazione,</span><span class="sxs-lookup"><span data-stu-id="611b1-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="611b1-161">Eseguire i seguenti passaggi per rimuovere la voce esistente:</span><span class="sxs-lookup"><span data-stu-id="611b1-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="611b1-162">In un Web browser aprire l'interfaccia utente Web di Ambari per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="611b1-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="611b1-163">L'URI è https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="611b1-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="611b1-164">Sostituire __CLUSTERNAME__ con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="611b1-165">Quando richiesto, immettere l'utente e la password di accesso HTTP per il cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="611b1-166">Dall'elenco di servizi nella parte sinistra della pagina selezionare __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="611b1-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="611b1-167">Selezionare quindi la scheda __Configs__ (Configurazioni) al centro della pagina.</span><span class="sxs-lookup"><span data-stu-id="611b1-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="611b1-168">Nel campo __Filter__ (Filtro) immettere il valore __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="611b1-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="611b1-169">Vengono restituite le voci per eventuali account di archiviazione aggiunti al cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="611b1-170">Sono disponibili due tipi di voci, ovvero __keyprovider__ e __key__.</span><span class="sxs-lookup"><span data-stu-id="611b1-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="611b1-171">Entrambi i tipi contengono il nome dell'account di archiviazione come parte del nome della chiave.</span><span class="sxs-lookup"><span data-stu-id="611b1-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="611b1-172">Le voci di esempio seguenti sono relative a un account di archiviazione denominato __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="611b1-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="611b1-173">Dopo avere identificato le chiavi per l'account di archiviazione da rimuovere, usare l'icona '-' rossa a destra della voce per eliminarla.</span><span class="sxs-lookup"><span data-stu-id="611b1-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="611b1-174">Usare quindi il pulsante __Salva__ per salvare le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="611b1-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="611b1-175">Dopo il salvataggio delle modifiche, usare l'azione script per aggiungere l'account di archiviazione e il nuovo valore della chiave al cluster.</span><span class="sxs-lookup"><span data-stu-id="611b1-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="611b1-176">Prestazioni non ottimali</span><span class="sxs-lookup"><span data-stu-id="611b1-176">Poor performance</span></span>

<span data-ttu-id="611b1-177">Se l'account di archiviazione si trova in un'area diversa rispetto al cluster HDInsight, è possibile che le prestazioni non siano ottimali.</span><span class="sxs-lookup"><span data-stu-id="611b1-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="611b1-178">L'accesso ai dati in un'area diversa comporta l'invio di traffico di rete all'esterno del data center di Azure di un'area specifica e la trasmissione tramite Internet pubblico e ciò può introdurre latenza.</span><span class="sxs-lookup"><span data-stu-id="611b1-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="611b1-179">L'uso di un account di archiviazione in un'area diversa rispetto al cluster HDInsight non è supportato.</span><span class="sxs-lookup"><span data-stu-id="611b1-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="611b1-180">Costi aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="611b1-180">Additional charges</span></span>

<span data-ttu-id="611b1-181">Se l'account di archiviazione si trova in un'area diversa rispetto al cluster HDInsight, è possibile che la fatturazione di Azure includa addebiti di uscita aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="611b1-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="611b1-182">Viene applicato un addebito di uscita quando i dati escono dal data center di un'area,</span><span class="sxs-lookup"><span data-stu-id="611b1-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="611b1-183">anche se il traffico è destinato a un altro data center di Azure in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="611b1-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="611b1-184">L'uso di un account di archiviazione in un'area diversa rispetto al cluster HDInsight non è supportato.</span><span class="sxs-lookup"><span data-stu-id="611b1-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="611b1-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="611b1-185">Next steps</span></span>

<span data-ttu-id="611b1-186">Fino a ora sono state date le informazioni su come aggiungere altri account di archiviazione a un cluster HDInsight esistente.</span><span class="sxs-lookup"><span data-stu-id="611b1-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="611b1-187">Per altre informazioni sulle azioni script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="611b1-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
