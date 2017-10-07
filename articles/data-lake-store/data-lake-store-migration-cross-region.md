---
title: migrazione tra aree di archivio Data Lake aaaAzure | Documenti Microsoft
description: Informazioni sulla migrazione tra aree per Azure Data Lake Store.
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>Eseguire la migrazione di Data Lake Store tra aree

Come archivio Azure Data Lake diventa disponibile in aree di nuovo, è possibile scegliere una migrazione occasionale, tootake sfruttare la nuova area hello toodo. Informazioni su quali tooconsider durante la pianificazione e completata la migrazione di hello.

## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**. Per altre informazioni, vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/).
* **Un account Data Lake Store in due aree diverse**. Per altre informazioni, vedere l'[introduzione ad Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Azure Data Factory**. Per ulteriori informazioni, vedere [tooAzure introduzione Data Factory](../data-factory/data-factory-introduction.md).


## <a name="migration-considerations"></a>Considerazioni sulla migrazione

Identificare innanzitutto strategia di migrazione hello adatto per l'applicazione che scrive, legge o elabora i dati in archivio Data Lake. Quando si sceglie una strategia, considerare i requisiti di disponibilità dell'applicazione e i tempi di inattività hello che si verifica durante una migrazione. Ad esempio, l'approccio più semplice potrebbe essere toouse hello "sollevamento e spostamento" cloud migrazione modello. Questo approccio, si posiziona un'applicazione hello nel proprio paese esistenti mentre tutti i dati vengono copiati toohello nuova area. Termine del processo di copia hello, riprendere l'applicazione nella nuova area hello e quindi eliminare account archivio Data Lake precedente hello. Tempo di inattività durante la migrazione di hello è obbligatorio.

tooreduce i tempi di inattività, si potrebbe iniziare immediatamente l'inserimento di nuovi dati nella nuova area hello. Quando si dispone di dati di hello minimi necessari, è possibile eseguire l'applicazione nella nuova area hello. In background hello, continuare toocopy dati meno recenti da hello esistente account archivio Data Lake account toohello nuovo archivio Data Lake nella nuova area hello. Usando questo approccio, è possibile apportare hello commutatore toohello nuova area del tempo di inattività minimo. Dopo avere copiato tutti i dati meno recenti di hello, eliminare account archivio Data Lake precedente hello.

Di seguito sono riportati altri tooconsider dettagli importanti quando si pianifica la migrazione:

* **Volume dei dati**. volume Hello dei dati (in GB, il numero di hello di file e cartelle e così via) influisce sul tempo hello e le risorse che necessarie per la migrazione di hello.

* **Nome dell'account Data Lake Store**. nuovo nome account Hello nella nuova area hello deve essere globalmente univoco. Ad esempio, il nome di hello del vecchio account archivio Data Lake negli Stati Uniti orientali 2 potrebbe essere contosoeastus2.azuredatalakestore.net. Per il nuovo account Data Lake Store nell'area Europa settentrionale è possibile usare il nome contosoeuropasettentrionale.azuredatalakestore.net.

* **Strumenti**. È consigliabile usare hello [attività di copia di Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) toocopy i file di archivio Data Lake. Data Factory supporta lo spostamento dei dati con prestazioni e affidabilità elevate. Tenere presente che Data Factory copia solo la gerarchia di cartelle hello e contenuto del file hello. È necessario toomanually applicare qualsiasi elenchi di controllo di accesso (ACL) utilizzati in hello vecchio account toohello nuovo account. Per ulteriori informazioni, incluse le destinazioni di prestazioni per gli scenari migliore, vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](../data-factory/data-factory-copy-activity-performance.md). Se si desidera copiare più rapidamente dati, potrebbe essere necessario toouse altre unità lo spostamento dei dati di Cloud. Altri strumenti, come AdlCopy, non supportano la copia di dati tra aree.  

* **Costi per la larghezza di banda**. Vengono applicati [costi per la larghezza di banda](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) perché i dati vengono trasferiti all'esterno di un'area di Azure.

* **Elenchi di controllo di accesso applicati ai dati**. Proteggere i dati nella nuova area hello applicando gli ACL toofiles e cartelle. Per altre informazioni, vedere [Protezione dei dati archiviati in Azure Data Lake Store](data-lake-store-secure-data.md). È consigliabile utilizzare tooupdate migrazione hello e modificare l'ACL. È possibile toouse impostazioni tooyour corrente impostazioni simili. È possibile visualizzare gli elenchi ACL hello che vengono applicati tooany file tramite il portale di Azure, hello [i cmdlet di PowerShell](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission), o SDK.  

* **Posizione dei servizi di analisi**. Per prestazioni ottimali, i servizi analitica, ad esempio Azure Data Lake Analitica o Azure HDInsight, devono essere hello stessa area dati.  

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica dell’Archivio Data Lake di Azure](data-lake-store-overview.md)
