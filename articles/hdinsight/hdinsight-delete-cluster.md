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
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>Eliminare un cluster HDInsight tramite il browser, PowerShell o hello CLI di Azure

La fatturazione di cluster HDInsight inizia dopo che un cluster viene creato e si arresta quando viene eliminato il cluster hello. La fatturazione avviene con tariffa oraria, perciò si deve sempre eliminare il cluster in uso quando non lo si usa più. In questo documento, viene illustrato come un cluster mediante toodelete hello portale di Azure, Azure PowerShell e hello Azure CLI 1.0.

> [!IMPORTANT]
> L'eliminazione di un cluster HDInsight non comporta l'eliminazione di account di archiviazione di Azure hello o archivio Data Lake associata a cluster hello. È possibile riutilizzare i dati archiviati in tali servizi in hello future.

## <a name="azure-portal"></a>Portale di Azure

1. Accedi toohello [portale di Azure](https://portal.azure.com) e selezionare il cluster HDInsight. Se il cluster HDInsight non è bloccato toohello dashboard, è possibile cercarlo per nome utilizzando il campo di ricerca hello.
   
    ![ricerca nel portale](./media/hdinsight-delete-cluster/navbar.png)

2. Una volta pannello hello aperto per i cluster di hello, selezionare hello **eliminare** icona. Quando richiesto, selezionare **Sì** cluster hello toodelete.
   
    ![icona di eliminazione](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

Da un prompt di PowerShell, usare hello cluster hello toodelete di comando seguente:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Sostituire **CLUSTERNAME** con nome hello del cluster HDInsight.

## <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

Da un prompt dei comandi, utilizzare hello seguente cluster hello toodelete:

    azure hdinsight cluster delete CLUSTERNAME

Sostituire **CLUSTERNAME** con nome hello del cluster HDInsight.

> [!NOTE]
> L'interfaccia della riga di comando di Azure 2.0 non supporta attualmente l'eliminazione dei cluster HDInsight (31 luglio 2017).