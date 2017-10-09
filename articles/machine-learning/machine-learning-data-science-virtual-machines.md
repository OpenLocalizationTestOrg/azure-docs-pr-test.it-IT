---
title: Macchine virtuali di Azure Data Science come IPython Notebook server aaaProvision | Documenti Microsoft
description: Impostare una macchina virtuale di Data Science come server Notebook di IPython con gli strumenti di supporto.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>Eseguire il provisioning delle macchine virtuali di Data Science di Azure come server Notebook di IPython
Le istruzioni sono fornite di seguito che descrivono come tooset di una macchina virtuale di Azure e una macchina virtuale di Azure con il servizio SQL Server IPython Notebook. macchina virtuale di Windows Hello è configurato con supporto di strumenti, ad esempio IPython Notebook, Azure Storage Explorer, AzCopy, nonché altre utilità che sono utili per i progetti di analisi scientifica dei dati. Azure Storage Explorer e AzCopy, ad esempio, fornire agevolmente archiviazione tooAzure tooupload dei dati dal computer locale o toodownload è tooyour locali dall'archiviazione. 

Questo menu Collega tootopics che descrivono come tooset backup hello diversi ambienti di analisi scientifica dei dati utilizzata dal hello [Team Data Science processo (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Diversi tipi di macchine virtuali di Azure possono essere eseguito il provisioning e configurato toobe utilizzato come parte di un ambiente di analisi scientifica dei dati basati su cloud. Hello decisione su quale versione della macchina virtuale toouse dipende dal tipo hello e la quantità di dati toobe modellato con machine learning e destinazione hello per tali dati nel cloud hello. 

* Per informazioni aggiuntive sulla hello domande tooconsider quando si effettua questa decisione, vedere [pianificare dell'ambiente Azure Machine Learning dati scienza](machine-learning-data-science-plan-your-environment.md). 
* Per un catalogo di alcuni degli scenari di hello potrebbero verificarsi quando si esegue analitica avanzate, vedere [scenari per hello processo avanzato di Analitica e tecnologia in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md)

Sono disponibili due set di istruzioni:

* [Configurare una macchina virtuale di Azure come un server di IPython Notebook per analitica avanzate](machine-learning-data-science-setup-virtual-machine.md) viene illustrato l'utilizzo tooprovision una macchina virtuale Azure con IPython Notebook e altri strumenti di analisi scientifica dei dati toodo per i casi in cui un formato di archiviazione di Azure diverso da SQL può essere utilizzato toostore hello dati.
* [Configurare una macchina virtuale di Azure SQL Server come server di IPython Notebook per analitica avanzate](machine-learning-data-science-setup-sql-server-virtual-machine.md) viene illustrato l'utilizzo tooprovision una macchina virtuale di Azure SQL Server con IPython Notebook e altri strumenti di analisi scientifica dei dati toodo per i casi in cui un database SQL può essere utilizzato toostore hello dati.

Una volta eseguito il provisioning e configurata, queste macchine virtuali possono essere utilizzati come server di IPython Notebook per l'elaborazione dei dati e l'esplorazione di hello e per altre attività necessarie in combinazione con Azure Machine Learning e hello Team Data Science processo (TDSP). Hello passaggi successivi nel processo di analisi scientifica dei dati hello vengono eseguito il mapping in hello [il percorso di apprendimento TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e possono includere passaggi che spostano i dati in SQL Server o HDInsight, elaborare e in tale posizione di esempio in preparazione per l'apprendimento dai dati hello con Azure Machine Learning.

> [!NOTE]
> Macchine virtuali di Azure è disponibile con **pagamento a consumo**. tooensure che non vengono fatturate quando non si utilizza la macchina virtuale, è toobe in hello **arrestato (deallocato)** dello stato da hello [portale di Azure classico](http://manage.windowsazure.com/). Per istruzioni dettagliate o come toodeallocate di macchina virtuale, vedere [arrestare e deallocare una macchina virtuale quando non è in uso](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

