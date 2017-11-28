---
title: aaaHow toodelete un cluster HDInsight - Azure | Documenti Microsoft
description: "Informazioni sui vari modi in cui è possibile eliminare un cluster HDInsight hello."
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
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="7ca93-103">Eliminare un cluster HDInsight tramite il browser, PowerShell o hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="7ca93-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="7ca93-104">La fatturazione di cluster HDInsight inizia dopo che un cluster viene creato e si arresta quando viene eliminato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ca93-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="7ca93-105">La fatturazione avviene con tariffa oraria, perciò si deve sempre eliminare il cluster in uso quando non lo si usa più.</span><span class="sxs-lookup"><span data-stu-id="7ca93-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="7ca93-106">In questo documento, viene illustrato come un cluster mediante toodelete hello portale di Azure, Azure PowerShell e hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="7ca93-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ca93-107">L'eliminazione di un cluster HDInsight non comporta l'eliminazione di account di archiviazione di Azure hello o archivio Data Lake associata a cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ca93-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="7ca93-108">È possibile riutilizzare i dati archiviati in tali servizi in hello future.</span><span class="sxs-lookup"><span data-stu-id="7ca93-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="7ca93-109">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7ca93-109">Azure portal</span></span>

1. <span data-ttu-id="7ca93-110">Accedi toohello [portale di Azure](https://portal.azure.com) e selezionare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ca93-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="7ca93-111">Se il cluster HDInsight non è bloccato toohello dashboard, è possibile cercarlo per nome utilizzando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="7ca93-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![ricerca nel portale](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="7ca93-113">Una volta pannello hello aperto per i cluster di hello, selezionare hello **eliminare** icona.</span><span class="sxs-lookup"><span data-stu-id="7ca93-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="7ca93-114">Quando richiesto, selezionare **Sì** cluster hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="7ca93-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![icona di eliminazione](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="7ca93-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ca93-116">Azure PowerShell</span></span>

<span data-ttu-id="7ca93-117">Da un prompt di PowerShell, usare hello cluster hello toodelete di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7ca93-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="7ca93-118">Sostituire **CLUSTERNAME** con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ca93-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="7ca93-119">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="7ca93-119">Azure CLI 1.0</span></span>

<span data-ttu-id="7ca93-120">Da un prompt dei comandi, utilizzare hello seguente cluster hello toodelete:</span><span class="sxs-lookup"><span data-stu-id="7ca93-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="7ca93-121">Sostituire **CLUSTERNAME** con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ca93-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7ca93-122">L'interfaccia della riga di comando di Azure 2.0 non supporta attualmente l'eliminazione dei cluster HDInsight (31 luglio 2017).</span><span class="sxs-lookup"><span data-stu-id="7ca93-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>