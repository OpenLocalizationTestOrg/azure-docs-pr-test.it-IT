---
title: 'Gestire i cluster Hadoop tramite l''interfaccia della riga di comando di Azure: Azure HDInsight | Microsoft Docs'
description: Informazioni su come usare l'interfaccia della riga di comando di Azure per gestire i cluster Hadoop in Azure HDInsight. L'interfaccia della riga di comando di Azure funziona in Windows, Mac e Linux.
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
ms.openlocfilehash: 0ee9f2f28978b207dcaf8f77950bd82a897d3fd1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-the-azure-cli"></a><span data-ttu-id="6f14d-104">Gestire cluster Hadoop in HDInsight tramite la CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="6f14d-104">Manage Hadoop clusters in HDInsight using the Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="6f14d-105">Informazioni su come usare l' [Interfaccia della riga di comando di Azure](../cli-install-nodejs.md) per gestire i cluster Hadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6f14d-105">Learn how to use the [Azure Command-line Interface](../cli-install-nodejs.md) to manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="6f14d-106">L'interfaccia della riga di comando di Azure viene implementata in Node.js.</span><span class="sxs-lookup"><span data-stu-id="6f14d-106">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="6f14d-107">Può essere usato in tutte le piattaforme che supportano Node.js, incluse Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="6f14d-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="6f14d-108">In questo articolo viene illustrato solo l’uso dell’interfaccia della riga di comando di Azure con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6f14d-108">This article covers only using the Azure CLI with HDInsight.</span></span> <span data-ttu-id="6f14d-109">Per una guida generale sull'uso dell'interfaccia della riga di comando di Azure, vedere [Installare e configurare l'interfaccia della riga di comando di Azure][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="6f14d-109">For a general guide on how to use Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="6f14d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6f14d-110">Prerequisites</span></span>
<span data-ttu-id="6f14d-111">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="6f14d-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="6f14d-112">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="6f14d-112">**An Azure subscription**.</span></span> <span data-ttu-id="6f14d-113">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6f14d-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6f14d-114">**Interfaccia della riga di comando di Azure** : per informazioni sull’installazione e la configurazione vedere [Installare e configurare l’interfaccia della riga di comando di Azure](../cli-install-nodejs.md) .</span><span class="sxs-lookup"><span data-stu-id="6f14d-114">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="6f14d-115">**Collegarsi ad Azure**, usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6f14d-115">**Connect to Azure**, using the following command:</span></span>
  
        azure login
  
    <span data-ttu-id="6f14d-116">Per altre informazioni sull'autenticazione con un account aziendale o dell'istituto di istruzione, vedere [Connettersi a una sottoscrizione Azure dall'interfaccia della riga di comando di Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6f14d-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="6f14d-117">**Passare alla modalità Gestione risorse di Azure**, usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6f14d-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="6f14d-118">Per ottenere assistenza, utilizzare l’opzione **-h** .</span><span class="sxs-lookup"><span data-stu-id="6f14d-118">To get help, use the **-h** switch.</span></span>  <span data-ttu-id="6f14d-119">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6f14d-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-the-cli"></a><span data-ttu-id="6f14d-120">Creare cluster con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="6f14d-120">Create clusters with the CLI</span></span>
<span data-ttu-id="6f14d-121">Vedere [Creare cluster Hadoop in HDInsight tramite l'interfaccia della riga di comando di Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6f14d-121">See [Create clusters in HDInsight using the Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="6f14d-122">Elencare i cluster e visualizzarne i dettagli</span><span class="sxs-lookup"><span data-stu-id="6f14d-122">List and show cluster details</span></span>
<span data-ttu-id="6f14d-123">Utilizzare i comandi seguenti per elencare e mostrare i dettagli dei cluster:</span><span class="sxs-lookup"><span data-stu-id="6f14d-123">Use the following commands to list and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="6f14d-124">![Visualizzazione della riga di comando dell'elenco di cluster][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="6f14d-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="6f14d-125">Eliminare cluster</span><span class="sxs-lookup"><span data-stu-id="6f14d-125">Delete clusters</span></span>
<span data-ttu-id="6f14d-126">Utilizzare il comando seguente per eliminare un cluster:</span><span class="sxs-lookup"><span data-stu-id="6f14d-126">Use the following command to delete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="6f14d-127">È inoltre possibile eliminare un cluster eliminando il gruppo di risorse che lo contiene.</span><span class="sxs-lookup"><span data-stu-id="6f14d-127">You can also delete a cluster by deleting the resource group that contains the cluster.</span></span> <span data-ttu-id="6f14d-128">Tenere presente che questa operazione eliminerà tutte le risorse nel gruppo, compreso l’account di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="6f14d-128">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="6f14d-129">Ridimensionare i cluster</span><span class="sxs-lookup"><span data-stu-id="6f14d-129">Scale clusters</span></span>
<span data-ttu-id="6f14d-130">Per modificare le dimensioni del cluster Hadoop:</span><span class="sxs-lookup"><span data-stu-id="6f14d-130">To change the Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="6f14d-131">Abilitare/disabilitare l'accesso HTTP per un cluster</span><span class="sxs-lookup"><span data-stu-id="6f14d-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="6f14d-132">Abilitare/disabilitare l'accesso RDP per un cluster</span><span class="sxs-lookup"><span data-stu-id="6f14d-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="6f14d-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f14d-133">Next steps</span></span>
<span data-ttu-id="6f14d-134">In questo articolo si è appreso come eseguire diverse attività amministrative relative ai cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6f14d-134">In this article, you have learned how to perform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="6f14d-135">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f14d-135">To learn more, see the following articles:</span></span>

* <span data-ttu-id="6f14d-136">[Amministrare HDInsight con il portale di Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="6f14d-136">[Administer HDInsight by using the Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="6f14d-137">[Amministrare HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="6f14d-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="6f14d-138">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="6f14d-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="6f14d-139">[Come usare l'interfaccia della riga di comando di Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="6f14d-139">[How to use the Azure CLI][azure-command-line-tools]</span></span>

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
