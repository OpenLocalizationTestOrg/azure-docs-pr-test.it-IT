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
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Gestire i cluster Hadoop in HDInsight mediante hello CLI di Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Informazioni su come hello toouse [interfaccia della riga di comando di Azure](../cli-install-nodejs.md) toomanage Hadoop cluster in Azure HDInsight. Hello CLI di Azure è implementato in Node.js. Può essere usato in tutte le piattaforme che supportano Node.js, incluse Windows, Mac e Linux.

Questo articolo descrive solo con hello CLI di Azure HDInsight. Per indicazioni generali su come toouse CLI di Azure, vedere [installare e configurare Azure CLI][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **CLI di Azure** -vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) per informazioni sull'installazione e configurazione.
* **Connettersi tooAzure**tramite hello il seguente comando:
  
        azure login
  
    Per ulteriori informazioni sull'autenticazione con un account aziendale o dell'istituto di istruzione, vedere [connettersi tooan sottoscrizione di Azure da hello Azure CLI](../xplat-cli-connect.md).
* **Cambia modalità di gestione risorse di Azure toohello**tramite hello il seguente comando:
  
        azure config mode arm

tooget della Guida in linea, utilizzare hello **-h** passare.  ad esempio:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>Creare un cluster con hello CLI
Vedere [Crea cluster HDInsight con hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Elencare i cluster e visualizzarne i dettagli
Utilizzare hello toolist i comandi seguenti e visualizzare i dettagli del cluster:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Visualizzazione della riga di comando dell'elenco di cluster][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Eliminare cluster
Utilizzare hello successivo comando toodelete un cluster:

    azure hdinsight cluster delete <Cluster Name>

È anche possibile eliminare un cluster di gruppo di risorse hello contenente cluster hello. Si noti, questa operazione eliminerà tutte le risorse di hello gruppo hello inclusi account di archiviazione predefinito hello.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Ridimensionare i cluster
hello toochange dimensioni del cluster Hadoop:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Abilitare/disabilitare l'accesso HTTP per un cluster
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Abilitare/disabilitare l'accesso RDP per un cluster
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come attività di amministrazione del cluster HDInsight di tooperform diverse. toolearn informazioni, vedere hello seguenti articoli:

* [Amministrazione di HDInsight tramite hello portale di Azure][hdinsight-admin-portal]
* [Amministrare HDInsight con Azure PowerShell][hdinsight-admin-powershell]
* [Introduzione ad Azure HDInsight][hdinsight-get-started]
* [Come toouse hello CLI di Azure][azure-command-line-tools]

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
