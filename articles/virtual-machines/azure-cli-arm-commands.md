---
title: "i comandi CLI aaaAzure in modalità di gestione risorse | Documenti Microsoft"
description: Risorse toomanage nel modello di distribuzione di gestione risorse di hello i comandi di Azure interfaccia della riga di comando (CLI)
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="adfd2-103">Comandi dell’interfaccia della riga di comando Azure in modalità Resource Manager</span><span class="sxs-lookup"><span data-stu-id="adfd2-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="adfd2-104">In questo articolo fornisce una sintassi e le opzioni per i comandi di Azure interfaccia della riga di comando (CLI) avviene in genere utilizzano toocreate e gestire le risorse di Azure nel modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="adfd2-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="adfd2-105">Accedere ai comandi eseguendo hello CLI in modalità di gestione risorse (arm).</span><span class="sxs-lookup"><span data-stu-id="adfd2-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="adfd2-106">Non si tratta di un riferimento completo e la versione dell'interfaccia della riga di comando in uso potrebbe mostrare comandi o parametri leggermente diversi.</span><span class="sxs-lookup"><span data-stu-id="adfd2-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="adfd2-107">Per informazioni generali su risorse e gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="adfd2-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="adfd2-108">In questo articolo mostra i comandi di modalità di gestione risorse in hello CLI di Azure, talvolta chiamato CLI di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="adfd2-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="adfd2-109">toowork nel modello di gestione risorse di hello, è anche possibile provare hello [CLI di Azure 2.0](/cli/azure/install-az-cli2), la multi-piattaforma nuova generazione CLI.</span><span class="sxs-lookup"><span data-stu-id="adfd2-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="adfd2-110">Ulteriori informazioni su hello [CLI di Azure precedenti e nuovi](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="adfd2-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="adfd2-111">tooget avviare prima [installare hello Azure CLI](../cli-install-nodejs.md) e [tooyour sottoscrizione di Azure connettersi](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="adfd2-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="adfd2-112">Per la sintassi del comando corrente e le opzioni nella riga di comando hello in modalità di gestione delle risorse, digitare `azure help` o toodisplay della Guida per un comando specifico, `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="adfd2-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="adfd2-113">Inoltre è possibile trovare esempi CLI nella documentazione di hello per la creazione e gestione dei servizi di Azure specifici.</span><span class="sxs-lookup"><span data-stu-id="adfd2-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="adfd2-114">I parametri facoltativi sono indicati tra parentesi quadre, ad esempio `[parameter]`.</span><span class="sxs-lookup"><span data-stu-id="adfd2-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="adfd2-115">Tutti gli altri parametri sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="adfd2-115">All other parameters are required.</span></span>

<span data-ttu-id="adfd2-116">Parametri facoltativi specifici toocommand inoltre documentato, sono disponibili tre parametri facoltativi che possono essere utilizzati toodisplay l'output, ad esempio le opzioni di richiesta e codici di stato dettagliato.</span><span class="sxs-lookup"><span data-stu-id="adfd2-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="adfd2-117">Hello `-v` parametro fornisce output dettagliato e hello `-vv` parametro fornisce ancora più dettagliate output dettagliato.</span><span class="sxs-lookup"><span data-stu-id="adfd2-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="adfd2-118">Hello `--json` opzione genera risultati hello in formato json non elaborato.</span><span class="sxs-lookup"><span data-stu-id="adfd2-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="adfd2-119">Impostazione della modalità di gestione risorse di hello</span><span class="sxs-lookup"><span data-stu-id="adfd2-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="adfd2-120">Comando che segue di hello utilizzare comandi in modalità di gestione risorse di Azure CLI tooenable.</span><span class="sxs-lookup"><span data-stu-id="adfd2-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="adfd2-121">modalità di gestione risorse di Azure e gestione dei servizi Azure Hello CLI si escludono a vicenda.</span><span class="sxs-lookup"><span data-stu-id="adfd2-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="adfd2-122">Vale a dire le risorse create in una modalità non possono essere gestite da hello altra modalità.</span><span class="sxs-lookup"><span data-stu-id="adfd2-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="adfd2-123">azure account - Gestione delle informazioni relative all'account</span><span class="sxs-lookup"><span data-stu-id="adfd2-123">azure account: Manage your account information</span></span>
<span data-ttu-id="adfd2-124">Le informazioni sulla sottoscrizione di Azure viene utilizzati da hello strumento tooconnect tooyour account.</span><span class="sxs-lookup"><span data-stu-id="adfd2-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="adfd2-125">**Elencare le sottoscrizioni di hello importato**</span><span class="sxs-lookup"><span data-stu-id="adfd2-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="adfd2-126">**Visualizzare i dettagli relativi a una sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="adfd2-127">**Impostare la sottoscrizione corrente hello**</span><span class="sxs-lookup"><span data-stu-id="adfd2-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="adfd2-128">**Rimuovere una sottoscrizione o l'ambiente o Cancella tutto delle informazioni sull'account e l'ambiente di hello archiviato**</span><span class="sxs-lookup"><span data-stu-id="adfd2-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="adfd2-129">**I comandi toomanage ambiente account**</span><span class="sxs-lookup"><span data-stu-id="adfd2-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="adfd2-130">Azure Active Directory: i comandi toodisplay oggetti di Active Directory</span><span class="sxs-lookup"><span data-stu-id="adfd2-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="adfd2-131">**Applicazioni di comandi toodisplay active directory**</span><span class="sxs-lookup"><span data-stu-id="adfd2-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="adfd2-132">**Gruppi di comandi toodisplay active directory**</span><span class="sxs-lookup"><span data-stu-id="adfd2-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="adfd2-133">**Comandi tooprovide informazioni di gruppo o un membro sub sull'active directory**</span><span class="sxs-lookup"><span data-stu-id="adfd2-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="adfd2-134">**Entità servizio di comandi toodisplay active directory**</span><span class="sxs-lookup"><span data-stu-id="adfd2-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="adfd2-135">**Utenti di active directory toodisplay comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="adfd2-136">Azure availset: imposta la disponibilità di comandi toomanage</span><span class="sxs-lookup"><span data-stu-id="adfd2-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="adfd2-137">**Creare un set di disponibilità all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="adfd2-138">**Gli elenchi di hello set di disponibilità all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="adfd2-139">**Ottenere un set di disponibilità all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="adfd2-140">**Eliminare un set di disponibilità all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="adfd2-141">configurazione di Azure: i comandi toomanage le impostazioni locali</span><span class="sxs-lookup"><span data-stu-id="adfd2-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="adfd2-142">**Elencare le impostazioni di configurazione dell'interfaccia della riga di comando di Azure**</span><span class="sxs-lookup"><span data-stu-id="adfd2-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="adfd2-143">**Eliminare un'impostazione di configurazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="adfd2-144">**Aggiornare un'impostazione di configurazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="adfd2-145">**Set di hello CLI di Azure funziona in modalità tooeither `arm` o`asm`**</span><span class="sxs-lookup"><span data-stu-id="adfd2-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="adfd2-146">funzionalità di Azure: comandi funzionalità account toomanage</span><span class="sxs-lookup"><span data-stu-id="adfd2-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="adfd2-147">**Elencare tutte le funzionalità disponibili per la sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="adfd2-148">**Visualizzare una funzionalità**</span><span class="sxs-lookup"><span data-stu-id="adfd2-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="adfd2-149">**Registrare una funzionalità in anteprima di un provider di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="adfd2-150">gruppo di Azure: i comandi toomanage dei gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="adfd2-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="adfd2-151">**Crea un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="adfd2-152">**Gruppo di risorse di set di tag tooa**</span><span class="sxs-lookup"><span data-stu-id="adfd2-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="adfd2-153">**Eliminare un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="adfd2-154">**Elenca i gruppi di risorse hello per la sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="adfd2-155">**Visualizzare un gruppo di risorse per la sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="adfd2-156">**Registri del gruppo risorse toomanage comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="adfd2-157">**I comandi toomanage la distribuzione in un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="adfd2-158">**I comandi toomanage del modello di gruppo locale o di una raccolta di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="adfd2-159">Azure hdinsight: i comandi toomanage i cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="adfd2-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="adfd2-160">**I comandi toocreate o aggiungere file di configurazione del cluster tooa**</span><span class="sxs-lookup"><span data-stu-id="adfd2-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="adfd2-161">Esempio: Creare un file di configurazione che contiene un toorun azione script durante la creazione di un cluster.</span><span class="sxs-lookup"><span data-stu-id="adfd2-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="adfd2-162">**Comando toocreate un cluster in un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="adfd2-163">Esempio: creare uno Storm nel cluster Linux</span><span class="sxs-lookup"><span data-stu-id="adfd2-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="adfd2-164">Esempio: creare un cluster con un'azione script</span><span class="sxs-lookup"><span data-stu-id="adfd2-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="adfd2-165">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="adfd2-166">**Comando toodelete un cluster**</span><span class="sxs-lookup"><span data-stu-id="adfd2-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="adfd2-167">**Dettagli del comando tooshow cluster**</span><span class="sxs-lookup"><span data-stu-id="adfd2-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="adfd2-168">**Toolist comando tutti i cluster (in un gruppo di risorse specifico, se specificato)**</span><span class="sxs-lookup"><span data-stu-id="adfd2-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="adfd2-169">**Comando tooresize un cluster**</span><span class="sxs-lookup"><span data-stu-id="adfd2-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="adfd2-170">**Comando accesso tooenable HTTP per un cluster**</span><span class="sxs-lookup"><span data-stu-id="adfd2-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="adfd2-171">**Comando accesso toodisable HTTP per un cluster**</span><span class="sxs-lookup"><span data-stu-id="adfd2-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="adfd2-172">**Comando tooenable RDP accesso per un cluster**</span><span class="sxs-lookup"><span data-stu-id="adfd2-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="adfd2-173">**Comando accesso toodisable HTTP per un cluster**</span><span class="sxs-lookup"><span data-stu-id="adfd2-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="adfd2-174">informazioni di Azure: i comandi correlati Insights toomonitoring (eventi, le regole di avviso, impostazioni di scalabilità automatica, metriche)</span><span class="sxs-lookup"><span data-stu-id="adfd2-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="adfd2-175">**Recuperare i log delle operazioni per una sottoscrizione, un ID correlazione, un gruppo di risorse, una risorsa o un provider di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="adfd2-176">località di Azure: comandi i percorsi del tooget hello disponibili per tutti i tipi di risorse</span><span class="sxs-lookup"><span data-stu-id="adfd2-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="adfd2-177">**Percorsi disponibili hello elenco**</span><span class="sxs-lookup"><span data-stu-id="adfd2-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="adfd2-178">rete di Azure: i comandi di risorse di rete toomanage</span><span class="sxs-lookup"><span data-stu-id="adfd2-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="adfd2-179">**Comandi toomanage le reti virtuali**</span><span class="sxs-lookup"><span data-stu-id="adfd2-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="adfd2-180">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="adfd2-180">Creates a virtual network.</span></span> <span data-ttu-id="adfd2-181">In hello esempio seguente viene creata una rete virtuale denominato newvnet per myresourcegroup gruppo di risorse nell'area Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="adfd2-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="adfd2-182">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="adfd2-183">Aggiorna la configurazione di una rete virtuale all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="adfd2-184">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="adfd2-185">comando Hello Elenca tutte le reti virtuali in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-185">hello command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="adfd2-186">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="adfd2-187">comando Hello Mostra le proprietà di rete virtuale hello in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-187">hello command shows hello virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="adfd2-188">comando Hello rimuove una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="adfd2-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="adfd2-189">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="adfd2-190">**Comandi toomanage subnet della rete virtuale**</span><span class="sxs-lookup"><span data-stu-id="adfd2-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="adfd2-191">Aggiunge un'altra subnet tooan rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="adfd2-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="adfd2-192">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="adfd2-193">Imposta una subnet specifica della rete virtuale all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="adfd2-194">Elenca tutte le subnet di rete virtuale hello per una rete virtuale specifica all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="adfd2-195">Visualizza le proprietà della subnet della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="adfd2-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="adfd2-196">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="adfd2-197">Rimuove una subnet da una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="adfd2-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="adfd2-198">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="adfd2-199">**Servizi di bilanciamento del carico toomanage comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="adfd2-200">Crea un set di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="adfd2-201">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="adfd2-202">Elenca le risorse di bilanciamento del carico all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="adfd2-203">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="adfd2-204">Visualizza le informazioni di un servizio/dispositivo di bilanciamento del carico specifico all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="adfd2-205">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="adfd2-206">Elimina le risorse di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="adfd2-207">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="adfd2-208">**Comandi toomanage probe di bilanciamento del carico**</span><span class="sxs-lookup"><span data-stu-id="adfd2-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="adfd2-209">Creare configurazione probe hello per lo stato di integrità nel servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="adfd2-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="adfd2-210">Tenere presente toorun questo comando, il servizio di bilanciamento del carico richiede una risorsa ip front-end (Check-out tooassign comando "azure front-end-indirizzo ip di rete" servizio di bilanciamento del tooload un indirizzo ip).</span><span class="sxs-lookup"><span data-stu-id="adfd2-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="adfd2-211">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="adfd2-212">Aggiorna un probe esistente del servizio/dispositivo di bilanciamento del carico con nuovi valori.</span><span class="sxs-lookup"><span data-stu-id="adfd2-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="adfd2-213">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="adfd2-214">Elencare le proprietà di tipo probe hello per un set di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="adfd2-215">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="adfd2-216">Rimuove il probe hello creato per servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="adfd2-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="adfd2-217">**Configurazioni ip di comandi toomanage front-end di bilanciamento del carico**</span><span class="sxs-lookup"><span data-stu-id="adfd2-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="adfd2-218">Crea un tooan di configurazione IP front-end esistente set bilanciamento di carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="adfd2-219">Gli aggiornamenti una configurazione esistente di un front-end comando IP.hello seguente aggiunge un indirizzo IP pubblico chiamato mypubip5 tooan esistente carico bilanciamento IP front-end denominato myfrontendip.</span><span class="sxs-lookup"><span data-stu-id="adfd2-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="adfd2-220">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="adfd2-221">Elenca tutte le risorse IP front-end hello configurate di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="adfd2-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="adfd2-222">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="adfd2-223">Elimina l'oggetto associato tooload bilanciamento di hello front-end IP</span><span class="sxs-lookup"><span data-stu-id="adfd2-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="adfd2-224">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="adfd2-225">**I comandi toomanage pool di indirizzi back-end di bilanciamento del carico**</span><span class="sxs-lookup"><span data-stu-id="adfd2-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="adfd2-226">Creare un pool di indirizzi back-end per un servizio/dispositivo di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="adfd2-227">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="adfd2-228">Elenca l'intervallo pool di indirizzi IP back-end per un gruppo di risorse specifico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="adfd2-229">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="adfd2-230">pool di indirizzi di rete lb eliminare [opzioni] < gruppo risorse >< lb-name ><name></span><span class="sxs-lookup"><span data-stu-id="adfd2-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="adfd2-231">Rimuove la risorsa dell'intervallo del pool IP hello back-end dal servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="adfd2-232">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="adfd2-233">**I comandi toomanage regole di bilanciamento del carico**</span><span class="sxs-lookup"><span data-stu-id="adfd2-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="adfd2-234">Crea regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-234">Create load balancer rules.</span></span>

<span data-ttu-id="adfd2-235">È possibile creare una regola di bilanciamento del carico di configurazione dell'endpoint di hello front-end di bilanciamento del carico hello e hello back-end indirizzo pool intervallo tooreceive hello in arrivo il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="adfd2-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="adfd2-236">Le impostazioni includono anche porte hello per endpoint IP front-end e le porte per l'intervallo di pool di indirizzi back-end hello.</span><span class="sxs-lookup"><span data-stu-id="adfd2-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="adfd2-237">Hello esempio seguente viene illustrato come regola toocreate un bilanciamento del carico, endpoint di front-end di hello in ascolto tooport 80 tooport 8080 per intervallo di pool di indirizzi back-end hello l'invio di traffico di rete TCP e il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="adfd2-238">Aggiorna una regola di sistema di bilanciamento del carico esistente impostata in un gruppo di risorse specifico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="adfd2-239">Nell'esempio seguente di hello, è stato modificato il nome della regola hello da mylbrule toomynewlbrule.</span><span class="sxs-lookup"><span data-stu-id="adfd2-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="adfd2-240">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="adfd2-241">Elenca tutte le regole di bilanciamento del carico configurate per un servizio/dispositivo di bilanciamento del carico in un gruppo di risorse specifico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="adfd2-242">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="adfd2-243">Elimina una regola di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="adfd2-244">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="adfd2-245">**Le regole NAT in ingresso di bilanciamento del carico di comandi toomanage**</span><span class="sxs-lookup"><span data-stu-id="adfd2-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="adfd2-246">Crea una regola NAT in ingresso per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="adfd2-247">In hello esempio seguente viene creata una regola NAT da IP front-end (che è stato definito in precedenza utilizzando il comando hello "ip front-end di rete di azure") con una porta di ascolto in entrata e porta in uscita di bilanciamento del carico hello utilizza il traffico di rete toosend hello.</span><span class="sxs-lookup"><span data-stu-id="adfd2-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="adfd2-248">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="adfd2-249">Aggiorna una regola NAT in ingresso esistente.</span><span class="sxs-lookup"><span data-stu-id="adfd2-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="adfd2-250">Nell'esempio seguente di hello, sono stati modificati hello in ingresso sulla porta di attesa da too81 80.</span><span class="sxs-lookup"><span data-stu-id="adfd2-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="adfd2-251">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="adfd2-252">Elenca tutte le regole NAT in ingresso per il servizio/dispositivo di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="adfd2-253">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="adfd2-254">Elimina regola NAT di bilanciamento del carico hello in un gruppo di risorse specifico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="adfd2-255">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="adfd2-256">**Indirizzi ip pubblici toomanage di comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="adfd2-257">Crea una risorsa IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-257">Creates a public ip resource.</span></span> <span data-ttu-id="adfd2-258">Verranno creare la risorsa indirizzo ip pubblico hello e associare il nome di dominio tooa.</span><span class="sxs-lookup"><span data-stu-id="adfd2-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="adfd2-259">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="adfd2-260">Aggiorna proprietà hello di una risorsa indirizzo ip pubblico esistente.</span><span class="sxs-lookup"><span data-stu-id="adfd2-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="adfd2-261">Nel seguente esempio hello indirizzo IP pubblico hello è stato modificato da tooStatic dinamica.</span><span class="sxs-lookup"><span data-stu-id="adfd2-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="adfd2-262">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="adfd2-263">network public-ip list [opzioni] &lt;resource-group&gt; Elenca tutte le risorse IP pubblico all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="adfd2-264">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="adfd2-265">indirizzo ip pubblico di rete Mostra [opzioni] < gruppo risorse ><name></span><span class="sxs-lookup"><span data-stu-id="adfd2-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="adfd2-266">Visualizza le proprietà di una risorsa IP pubblico all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="adfd2-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="adfd2-267">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="adfd2-268">Elimina una risorsa IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="adfd2-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="adfd2-269">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="adfd2-270">**Interfacce di rete toomanage comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="adfd2-271">Crea una risorsa denominata interfaccia di rete (NIC) che può essere utilizzato per servizi di bilanciamento del carico o associa tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="adfd2-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="adfd2-272">Opzioni dei parametri:</span><span class="sxs-lookup"><span data-stu-id="adfd2-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="adfd2-273">**Gruppi di sicurezza di rete toomanage comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="adfd2-274">**Regole di gruppo di sicurezza di rete di toomanage di comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="adfd2-275">**Profilo di gestione traffico toomanage comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="adfd2-276">**Endpoint di gestione traffico toomanage comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="adfd2-277">**Gateway di rete virtuale toomanage comandi**</span><span class="sxs-lookup"><span data-stu-id="adfd2-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="adfd2-278">provider di Azure: i comandi toomanage le registrazioni dei provider di risorse</span><span class="sxs-lookup"><span data-stu-id="adfd2-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="adfd2-279">**Elencare i provider attualmente registrati in Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="adfd2-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="adfd2-280">**Visualizzazione dei dettagli sulle hello richiesto lo spazio dei nomi di provider**</span><span class="sxs-lookup"><span data-stu-id="adfd2-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="adfd2-281">**Registrazione provider con sottoscrizione hello**</span><span class="sxs-lookup"><span data-stu-id="adfd2-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="adfd2-282">**Annullare la registrazione del provider con sottoscrizione hello**</span><span class="sxs-lookup"><span data-stu-id="adfd2-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="adfd2-283">risorse di Azure: i comandi toomanage le risorse</span><span class="sxs-lookup"><span data-stu-id="adfd2-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="adfd2-284">**Creare una risorsa in un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="adfd2-285">**Aggiornare una risorsa in un gruppo di risorse senza modelli o parametri**</span><span class="sxs-lookup"><span data-stu-id="adfd2-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="adfd2-286">**Gli elenchi di hello risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="adfd2-287">**Ottenere una risorsa all'interno di un gruppo di risorse o una sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="adfd2-288">**Eliminare una risorsa in un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="adfd2-289">ruolo di Azure: i comandi toomanage i ruoli Azure</span><span class="sxs-lookup"><span data-stu-id="adfd2-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="adfd2-290">**Ottenere tutte le definizioni di ruolo disponibili**</span><span class="sxs-lookup"><span data-stu-id="adfd2-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="adfd2-291">**Ottenere una definizione di ruolo disponibile**</span><span class="sxs-lookup"><span data-stu-id="adfd2-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="adfd2-292">**I comandi toomanage l'assegnazione di ruolo**</span><span class="sxs-lookup"><span data-stu-id="adfd2-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="adfd2-293">archiviazione di Azure: i comandi toomanage oggetti di archiviazione</span><span class="sxs-lookup"><span data-stu-id="adfd2-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="adfd2-294">**I comandi toomanage gli account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="adfd2-295">**I comandi toomanage le chiavi di account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="adfd2-296">**I comandi tooshow la stringa di connessione di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="adfd2-297">**I comandi toomanage ai contenitori di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="adfd2-298">**Firme di accesso condiviso toomanage comandi del contenitore di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="adfd2-299">**Comandi toomanage archiviati i criteri di accesso del contenitore di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="adfd2-300">**I comandi toomanage i BLOB di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="adfd2-301">**I comandi toomanage le operazioni di copia di blob**</span><span class="sxs-lookup"><span data-stu-id="adfd2-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="adfd2-302">**Firma di accesso condiviso di comandi toomanage del blob di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="adfd2-303">**I comandi toomanage le condivisioni di file di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="adfd2-304">**I comandi toomanage i file di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="adfd2-305">**I comandi toomanage directory dei file di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="adfd2-306">**I comandi toomanage le code di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="adfd2-307">**Firme di accesso condiviso toomanage comandi della coda di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="adfd2-308">**Comandi toomanage archiviati i criteri di accesso della coda di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="adfd2-309">**I comandi toomanage le proprietà di registrazione archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="adfd2-310">**I comandi toomanage le proprietà di metriche di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="adfd2-311">**I comandi toomanage le tabelle di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="adfd2-312">**Firme di accesso condiviso toomanage comandi della tabella di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="adfd2-313">**Comandi toomanage archiviati i criteri di accesso della tabella di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="adfd2-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="adfd2-314">tag di Azure: i comandi toomanage il tag di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="adfd2-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="adfd2-315">**Aggiungere un tag**</span><span class="sxs-lookup"><span data-stu-id="adfd2-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="adfd2-316">**Rimuovere un intero tag o un valore di tag**</span><span class="sxs-lookup"><span data-stu-id="adfd2-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="adfd2-317">**Elenca le informazioni di tag hello**</span><span class="sxs-lookup"><span data-stu-id="adfd2-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="adfd2-318">**Ottenere un tag**</span><span class="sxs-lookup"><span data-stu-id="adfd2-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="adfd2-319">macchina virtuale di Azure: i comandi toomanage le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="adfd2-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="adfd2-320">**Creare una macchina virtuale**</span><span class="sxs-lookup"><span data-stu-id="adfd2-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="adfd2-321">**Creare una macchina virtuale con le risorse predefinite**</span><span class="sxs-lookup"><span data-stu-id="adfd2-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="adfd2-322">A partire dalla versione 0,10 CLI, è possibile fornire un alias breve, ad esempio "UbuntuLTS" o "Win2012R2Datacenter" come hello `image-urn` per alcune immagini Marketplace più diffusi.</span><span class="sxs-lookup"><span data-stu-id="adfd2-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="adfd2-323">Eseguire `azure help vm quick-create` per le opzioni.</span><span class="sxs-lookup"><span data-stu-id="adfd2-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="adfd2-324">Inoltre, a partire dalla versione 0,10, `azure vm quick-create` viene utilizzata l'archiviazione premium per impostazione predefinita se è disponibile nell'area selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="adfd2-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="adfd2-325">**Macchine virtuali di hello elenco all'interno di un account**</span><span class="sxs-lookup"><span data-stu-id="adfd2-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="adfd2-326">**Ottenere una macchina virtuale all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="adfd2-327">**Eliminare una macchina virtuale all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="adfd2-328">**Arrestare una macchina virtuale all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="adfd2-329">**Riavviare una macchina virtuale all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="adfd2-330">**Avviare una macchina virtuale all'interno di un gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="adfd2-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="adfd2-331">**Arresto una macchina virtuale all'interno di un hello risorse di gruppo e rilascia le risorse di calcolo**</span><span class="sxs-lookup"><span data-stu-id="adfd2-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="adfd2-332">**Elencare le dimensioni delle macchine virtuali disponibili**</span><span class="sxs-lookup"><span data-stu-id="adfd2-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="adfd2-333">**Acquisire hello macchina virtuale come immagine del sistema operativo o l'immagine di macchina virtuale**</span><span class="sxs-lookup"><span data-stu-id="adfd2-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="adfd2-334">**Impostare lo stato di hello di hello VM tooGeneralized**</span><span class="sxs-lookup"><span data-stu-id="adfd2-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="adfd2-335">**Ottenere una visualizzazione dell'istanza di hello VM**</span><span class="sxs-lookup"><span data-stu-id="adfd2-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="adfd2-336">**Consentono di determinare le impostazioni di accesso Desktop remoto o SSH tooreset su una macchina virtuale e una password di hello tooreset di amministrazione o Sudo account hello**</span><span class="sxs-lookup"><span data-stu-id="adfd2-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="adfd2-337">**Aggiornare la macchina virtuale con nuovi dati**</span><span class="sxs-lookup"><span data-stu-id="adfd2-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="adfd2-338">**I comandi toomanage i dischi di dati delle macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="adfd2-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="adfd2-339">**Estensioni di risorsa comandi toomanage VM**</span><span class="sxs-lookup"><span data-stu-id="adfd2-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="adfd2-340">**I comandi toomanage la macchina virtuale Docker**</span><span class="sxs-lookup"><span data-stu-id="adfd2-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="adfd2-341">**Comandi toomanage immagini di macchina virtuale**</span><span class="sxs-lookup"><span data-stu-id="adfd2-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
