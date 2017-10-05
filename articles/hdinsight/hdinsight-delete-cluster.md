---
title: Come eliminare un cluster HDInsight - Azure | Microsoft Docs
description: Informazioni sui vari modi per eliminare un cluster HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 65dac529df15d2dd43eec17673d82a2832f7692e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a><span data-ttu-id="79a65-103">Eliminare un cluster HDInsight tramite browser, PowerShell o l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="79a65-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span></span>

<span data-ttu-id="79a65-104">La fatturazione del cluster HDInsight inizia dopo la creazione del cluster e si interrompe solo quando questo viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="79a65-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="79a65-105">La fatturazione avviene con tariffa oraria, perciò si deve sempre eliminare il cluster in uso quando non lo si usa più.</span><span class="sxs-lookup"><span data-stu-id="79a65-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="79a65-106">Questo documento spiega come eliminare un cluster tramite il portale di Azure, Azure PowerShell e l'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="79a65-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79a65-107">L'eliminazione di un cluster HDInsight non comporta l'eliminazione degli account di archiviazione di Azure o Data Lake Store associati al cluster.</span><span class="sxs-lookup"><span data-stu-id="79a65-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster.</span></span> <span data-ttu-id="79a65-108">È possibile usare nuovamente in futuro i dati archiviati in questi servizi.</span><span class="sxs-lookup"><span data-stu-id="79a65-108">You can reuse data stored in those services in the future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="79a65-109">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="79a65-109">Azure portal</span></span>

1. <span data-ttu-id="79a65-110">Accedere al [portale di Azure](https://portal.azure.com) e selezionare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79a65-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="79a65-111">Se il cluster HDInsight non è bloccato sul dashboard, è possibile cercarlo per nome usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="79a65-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span></span>
   
    ![ricerca nel portale](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="79a65-113">Dopo l'apertura del pannello per il cluster, selezionare l'icona **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="79a65-113">Once the blade opens for the cluster, select the **Delete** icon.</span></span> <span data-ttu-id="79a65-114">Quando richiesto, selezionare **Sì** per eliminare il cluster.</span><span class="sxs-lookup"><span data-stu-id="79a65-114">When prompted, select **Yes** to delete the cluster.</span></span>
   
    ![icona di eliminazione](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="79a65-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="79a65-116">Azure PowerShell</span></span>

<span data-ttu-id="79a65-117">Da un prompt di PowerShell, usare il comando seguente per eliminare il cluster:</span><span class="sxs-lookup"><span data-stu-id="79a65-117">From a PowerShell prompt, use the following command to delete the cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="79a65-118">Sostituire **CLUSTERNAME** con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79a65-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="79a65-119">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="79a65-119">Azure CLI 1.0</span></span>

<span data-ttu-id="79a65-120">Da un prompt, usare il comando seguente per eliminare il cluster:</span><span class="sxs-lookup"><span data-stu-id="79a65-120">From a prompt, use the following to delete the cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="79a65-121">Sostituire **CLUSTERNAME** con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79a65-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="79a65-122">L'interfaccia della riga di comando di Azure 2.0 non supporta attualmente l'eliminazione dei cluster HDInsight (31 luglio 2017).</span><span class="sxs-lookup"><span data-stu-id="79a65-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>