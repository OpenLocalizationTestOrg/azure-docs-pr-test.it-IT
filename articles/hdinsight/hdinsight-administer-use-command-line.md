---
title: i cluster Hadoop aaaManage mediante Azure CLI - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come i cluster toouse hello interfaccia della riga di comando di Azure toomanage Hadoop in HDInsight di Azure. Hello CLI di Azure funziona in Windows, Mac e Linux.
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="63e98-104">Gestire i cluster Hadoop in HDInsight mediante hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="63e98-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="63e98-105">Informazioni su come hello toouse [interfaccia della riga di comando di Azure](../cli-install-nodejs.md) toomanage Hadoop cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="63e98-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="63e98-106">Hello CLI di Azure è implementato in Node.js.</span><span class="sxs-lookup"><span data-stu-id="63e98-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="63e98-107">Può essere usato in tutte le piattaforme che supportano Node.js, incluse Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="63e98-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="63e98-108">Questo articolo descrive solo con hello CLI di Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="63e98-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="63e98-109">Per indicazioni generali su come toouse CLI di Azure, vedere [installare e configurare Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="63e98-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="63e98-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="63e98-110">Prerequisites</span></span>
<span data-ttu-id="63e98-111">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="63e98-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="63e98-112">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="63e98-112">**An Azure subscription**.</span></span> <span data-ttu-id="63e98-113">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="63e98-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="63e98-114">**CLI di Azure** -vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) per informazioni sull'installazione e configurazione.</span><span class="sxs-lookup"><span data-stu-id="63e98-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="63e98-115">**Connettersi tooAzure**tramite hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="63e98-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="63e98-116">Per ulteriori informazioni sull'autenticazione con un account aziendale o dell'istituto di istruzione, vedere [connettersi tooan sottoscrizione di Azure da hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="63e98-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="63e98-117">**Cambia modalità di gestione risorse di Azure toohello**tramite hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="63e98-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="63e98-118">tooget della Guida in linea, utilizzare hello **-h** passare.</span><span class="sxs-lookup"><span data-stu-id="63e98-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="63e98-119">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="63e98-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="63e98-120">Creare un cluster con hello CLI</span><span class="sxs-lookup"><span data-stu-id="63e98-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="63e98-121">Vedere [Crea cluster HDInsight con hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="63e98-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="63e98-122">Elencare i cluster e visualizzarne i dettagli</span><span class="sxs-lookup"><span data-stu-id="63e98-122">List and show cluster details</span></span>
<span data-ttu-id="63e98-123">Utilizzare hello toolist i comandi seguenti e visualizzare i dettagli del cluster:</span><span class="sxs-lookup"><span data-stu-id="63e98-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="63e98-124">![Visualizzazione della riga di comando dell'elenco di cluster][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="63e98-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="63e98-125">Eliminare cluster</span><span class="sxs-lookup"><span data-stu-id="63e98-125">Delete clusters</span></span>
<span data-ttu-id="63e98-126">Utilizzare hello successivo comando toodelete un cluster:</span><span class="sxs-lookup"><span data-stu-id="63e98-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="63e98-127">È anche possibile eliminare un cluster di gruppo di risorse hello contenente cluster hello.</span><span class="sxs-lookup"><span data-stu-id="63e98-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="63e98-128">Si noti, questa operazione eliminerà tutte le risorse di hello gruppo hello inclusi account di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="63e98-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="63e98-129">Ridimensionare i cluster</span><span class="sxs-lookup"><span data-stu-id="63e98-129">Scale clusters</span></span>
<span data-ttu-id="63e98-130">hello toochange dimensioni del cluster Hadoop:</span><span class="sxs-lookup"><span data-stu-id="63e98-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="63e98-131">Abilitare/disabilitare l'accesso HTTP per un cluster</span><span class="sxs-lookup"><span data-stu-id="63e98-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="63e98-132">Abilitare/disabilitare l'accesso RDP per un cluster</span><span class="sxs-lookup"><span data-stu-id="63e98-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="63e98-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63e98-133">Next steps</span></span>
<span data-ttu-id="63e98-134">In questo articolo, si è appreso come attività di amministrazione del cluster HDInsight di tooperform diverse.</span><span class="sxs-lookup"><span data-stu-id="63e98-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="63e98-135">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="63e98-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="63e98-136">[Amministrazione di HDInsight tramite hello portale di Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="63e98-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="63e98-137">[Amministrare HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="63e98-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="63e98-138">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="63e98-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="63e98-139">[Come toouse hello CLI di Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="63e98-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Elencare e visualizzare i cluster"
