---
title: account di archiviazione di Azure aggiuntivi aaaAdd tooHDInsight | Documenti Microsoft
description: Informazioni su come archiviazione di Azure aggiuntivi tooadd account cluster HDInsight esistente tooan.
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
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="94ecc-103">Aggiungere ulteriore spazio di archiviazione account tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="94ecc-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="94ecc-104">Informazioni su come toouse script azioni tooadd aggiuntive Azure storage account tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="94ecc-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="94ecc-105">Hello passaggi descritti in questo documento aggiungere un cluster di HDInsight basati su Linux esistente storage account tooan.</span><span class="sxs-lookup"><span data-stu-id="94ecc-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94ecc-106">informazioni di Hello in questo documento sono informazioni sull'aggiunta di cluster tooa ulteriore spazio di archiviazione dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="94ecc-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="94ecc-107">Per informazioni sull'aggiunta di account di archiviazione durante la creazione del cluster, vedere [Configurare cluster in HDInsight con Hadoop, Spark, Kafka e altro](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="94ecc-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="94ecc-108">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="94ecc-108">How it works</span></span>

<span data-ttu-id="94ecc-109">Questo script accetta hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="94ecc-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="94ecc-110">__Nome dell'account di archiviazione Azure__: nome hello del cluster di HDInsight toohello hello storage account tooadd.</span><span class="sxs-lookup"><span data-stu-id="94ecc-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="94ecc-111">Dopo l'esecuzione di script hello, HDInsight può leggere e scrivere dati archiviati in questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="94ecc-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="94ecc-112">__Chiave dell'account di archiviazione di Azure__: una chiave che concede l'accesso toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="94ecc-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="94ecc-113">__-p__ (facoltativo): se specificato, chiave hello non è crittografato e viene archiviato nel file core-Site.XML hello come testo normale.</span><span class="sxs-lookup"><span data-stu-id="94ecc-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="94ecc-114">Durante l'elaborazione, lo script di hello esegue hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="94ecc-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="94ecc-115">Se hello account di archiviazione esiste già nella configurazione core-Site.XML hello per cluster hello, hello script viene chiuso e che non vengano eseguite ulteriori azioni.</span><span class="sxs-lookup"><span data-stu-id="94ecc-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="94ecc-116">Verifica che l'account di archiviazione hello esiste e sono accessibili mediante chiave hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="94ecc-117">Crittografa la chiave di hello utilizzando credenziali cluster hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="94ecc-118">Aggiunge il file core-Site.XML toohello di hello storage account.</span><span class="sxs-lookup"><span data-stu-id="94ecc-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="94ecc-119">Arresta e riavvia i servizi di Oozie, YARN, MapReduce2 e HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="94ecc-120">Arrestare e avviare questi servizi, tali dati toouse hello nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="94ecc-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="94ecc-121">Non è supportato l'utilizzo di un account di archiviazione in un percorso diverso da quello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="94ecc-122">script Hello</span><span class="sxs-lookup"><span data-stu-id="94ecc-122">hello script</span></span>

<span data-ttu-id="94ecc-123">__Percorso dello script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="94ecc-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="94ecc-124">__Requisiti__:</span><span class="sxs-lookup"><span data-stu-id="94ecc-124">__Requirements__:</span></span>

* <span data-ttu-id="94ecc-125">script Hello deve essere applicato a hello __nodi Head__.</span><span class="sxs-lookup"><span data-stu-id="94ecc-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="94ecc-126">script hello toouse</span><span class="sxs-lookup"><span data-stu-id="94ecc-126">toouse hello script</span></span>

<span data-ttu-id="94ecc-127">Questo script può essere utilizzato da hello portale di Azure, Azure PowerShell, o hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="94ecc-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="94ecc-128">Per ulteriori informazioni, vedere hello [ai cluster HDInsight basati su Linux personalizzare mediante l'azione di script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.</span><span class="sxs-lookup"><span data-stu-id="94ecc-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94ecc-129">Quando si utilizza la procedura hello descritta nel documento personalizzazione hello, utilizzare questo script hello tooapply le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="94ecc-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="94ecc-130">Sostituire qualsiasi azione di script di esempio URI con hello URI per questo script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="94ecc-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="94ecc-131">Sostituire i parametri di esempio con nome di account di archiviazione di Azure hello e la chiave del cluster di hello archiviazione account toobe toohello aggiunto.</span><span class="sxs-lookup"><span data-stu-id="94ecc-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="94ecc-132">Se tramite hello portale di Azure, questi parametri devono essere separati da uno spazio.</span><span class="sxs-lookup"><span data-stu-id="94ecc-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="94ecc-133">Non è necessario toomark questo script come __Persisted__, come aggiorna direttamente configurazione Ambari hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="94ecc-134">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="94ecc-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="94ecc-135">Account di archiviazione non visualizzati nel portale di Azure o negli strumenti</span><span class="sxs-lookup"><span data-stu-id="94ecc-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="94ecc-136">Quando la visualizzazione hello HDInsight cluster in hello portale di Azure, la selezione di hello __gli account di archiviazione__ voce __proprietà__ non vengono visualizzati gli account di archiviazione aggiunti tramite questa azione di script.</span><span class="sxs-lookup"><span data-stu-id="94ecc-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="94ecc-137">Azure PowerShell e CLI di Azure non visualizzano di account di archiviazione aggiuntivo hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="94ecc-138">non vengono visualizzate informazioni sull'archiviazione Hello perché script hello modifica solo una configurazione di core-Site.XML hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="94ecc-139">Queste informazioni non vengono utilizzate durante il recupero delle informazioni del cluster hello utilizzando le API di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94ecc-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="94ecc-140">informazioni sull'account di archiviazione tooview aggiunto toohello cluster tramite questo script, utilizzare hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="94ecc-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="94ecc-141">Utilizzare queste informazioni di hello tooretrieve i comandi seguenti per il cluster:</span><span class="sxs-lookup"><span data-stu-id="94ecc-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="94ecc-142">Impostare `$clusterName` toohello nome del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="94ecc-143">Impostare `$storageAccountName` toohello nome dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="94ecc-144">Quando richiesto, immettere l'account di accesso cluster hello (amministratore) e la password.</span><span class="sxs-lookup"><span data-stu-id="94ecc-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="94ecc-145">Impostare `$PASSWORD` password dell'account di accesso (amministrazione) di toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="94ecc-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="94ecc-146">Impostare `$CLUSTERNAME` toohello nome del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="94ecc-147">Impostare `$STORAGEACCOUNTNAME` toohello nome dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="94ecc-148">Questo esempio viene utilizzato [curl (http://curl.haxx.se/)](http://curl.haxx.se/) e [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve e analizzare i dati JSON.</span><span class="sxs-lookup"><span data-stu-id="94ecc-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="94ecc-149">Quando si utilizza questo comando, sostituire __CLUSTERNAME__ con nome hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="94ecc-150">Sostituire __PASSWORD__ con password di accesso hello HTTP per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="94ecc-151">Sostituire __STORAGEACCOUNT__ con nome hello hello dell'account di archiviazione aggiunti mediante l'azione di script.</span><span class="sxs-lookup"><span data-stu-id="94ecc-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="94ecc-152">Le informazioni restituite da questo comando viene visualizzata toohello simile, il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="94ecc-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="94ecc-153">Questo testo è un esempio di una chiave crittografata, che viene utilizzato tooaccess hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="94ecc-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="94ecc-154">Non è possibile tooaccess archiviazione dopo la modifica chiave</span><span class="sxs-lookup"><span data-stu-id="94ecc-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="94ecc-155">Se si modifica la chiave hello per un account di archiviazione, HDInsight non può accedere non è più account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="94ecc-156">HDInsight utilizza una copia della chiave memorizzata nella cache in core-Site.XML hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="94ecc-157">Questa copia memorizzata nella cache deve essere una nuova chiave di hello toomatch aggiornato.</span><span class="sxs-lookup"><span data-stu-id="94ecc-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="94ecc-158">Esecuzione azione di script hello nuovamente __non__ aggiornare la chiave di hello, come script hello controlla toosee se esiste già una voce per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="94ecc-159">Se esiste già una voce, non viene apportata alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="94ecc-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="94ecc-160">toowork questo problema, è necessario rimuovere una voce hello hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="94ecc-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="94ecc-161">Utilizzare hello entrata passaggi tooremove hello esistente:</span><span class="sxs-lookup"><span data-stu-id="94ecc-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="94ecc-162">In un web browser, aprire hello Ambari Web UI per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="94ecc-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="94ecc-163">Hello URI è https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="94ecc-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="94ecc-164">Sostituire __CLUSTERNAME__ con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="94ecc-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="94ecc-165">Quando richiesto, immettere l'account di accesso HTTP hello e una password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="94ecc-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="94ecc-166">Selezionare nell'elenco dei servizi a sinistra di hello della pagina hello hello __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="94ecc-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="94ecc-167">Selezionare quindi hello __configurazioni__ scheda centro hello della pagina di hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="94ecc-168">In hello __filtro...__  immettere un valore di __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="94ecc-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="94ecc-169">Restituisce le voci relative agli account di archiviazione aggiuntivi che sono stati aggiunti toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="94ecc-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="94ecc-170">Sono disponibili due tipi di voci, ovvero __keyprovider__ e __key__.</span><span class="sxs-lookup"><span data-stu-id="94ecc-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="94ecc-171">Entrambi contengono il nome di hello hello dell'account di archiviazione come parte del nome della chiave hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="94ecc-172">di seguito Hello sono voci di esempio per un account di archiviazione denominato __la risorsa mystorage__:</span><span class="sxs-lookup"><span data-stu-id="94ecc-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="94ecc-173">Dopo aver identificato le chiavi di hello hello account di archiviazione è necessario tooremove, utilizzare hello rosso '-' icona toohello diritto di hello voce toodelete è.</span><span class="sxs-lookup"><span data-stu-id="94ecc-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="94ecc-174">Utilizzare quindi hello __salvare__ pulsante toosave le modifiche.</span><span class="sxs-lookup"><span data-stu-id="94ecc-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="94ecc-175">Dopo che sono state salvate le modifiche, utilizzare account di archiviazione hello tooadd azione script hello e cluster di toohello nuovo valore della chiave.</span><span class="sxs-lookup"><span data-stu-id="94ecc-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="94ecc-176">Prestazioni non ottimali</span><span class="sxs-lookup"><span data-stu-id="94ecc-176">Poor performance</span></span>

<span data-ttu-id="94ecc-177">Se l'account di archiviazione hello è in un'area diversa rispetto al cluster HDInsight hello, si potrebbe influire negativamente sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="94ecc-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="94ecc-178">L'accesso ai dati in un'area diversa invia il traffico di rete all'esterno di hello internazionali data center di Azure e attraverso hello internet pubblico, che può provocare latenza.</span><span class="sxs-lookup"><span data-stu-id="94ecc-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="94ecc-179">Non è possibile utilizzare un account di archiviazione in un'area diversa rispetto al cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="94ecc-180">Costi aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="94ecc-180">Additional charges</span></span>

<span data-ttu-id="94ecc-181">Se l'account di archiviazione hello è in un'area diversa rispetto a hello cluster HDInsight, è possibile riscontrare costi di uscita aggiuntive sulla fatturazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94ecc-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="94ecc-182">Viene applicato un addebito di uscita quando i dati escono dal data center di un'area,</span><span class="sxs-lookup"><span data-stu-id="94ecc-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="94ecc-183">L'addebito viene applicato anche se il traffico di hello è destinato a un altro data center di Azure in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="94ecc-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="94ecc-184">Non è possibile utilizzare un account di archiviazione in un'area diversa rispetto al cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="94ecc-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94ecc-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94ecc-185">Next steps</span></span>

<span data-ttu-id="94ecc-186">Si è appreso come account del cluster HDInsight esistente tooan tooadd ulteriore spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="94ecc-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="94ecc-187">Per altre informazioni sulle azioni script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="94ecc-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
