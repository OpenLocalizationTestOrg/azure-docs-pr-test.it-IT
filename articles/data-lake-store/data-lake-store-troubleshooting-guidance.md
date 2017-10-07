---
title: domande frequenti per archivio Azure Data Lake aaaFrequently | Documenti Microsoft
description: Guida alla risoluzione dei problemi o ai problemi di migrazione con Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Domande frequenti su Azure Data Lake Store
In questo articolo si apprenderà sulle domande frequenti su aspetti correlati tooAzure archivio Data Lake.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>Come è possibile proteggere ulteriormente i dati da emergenze che interessano l'intera area o da eliminazioni accidentali?
dati Hello nell'account archivio Azure Data Lake sono guasti hardware tootransient resilienti all'interno di un'area attraverso repliche automatizzate. Ciò garantisce la durabilità e disponibilità elevata, hello riunione SLA di archivio Azure Data Lake. Ecco alcune indicazioni su come proteggere i dati di toofurther da rare interruzioni a livello di area o eliminazioni accidentali.

### <a name="disaster-recovery-guidance"></a>Indicazioni sul ripristino di emergenza
È essenziale per ogni cliente tooprepare proprio piano di ripristino di emergenza. Vedere la documentazione di Azure seguito toobuild toohello il piano di ripristino di emergenza. Di seguito sono riportate alcune risorse che consentono di creare proprio piano.

* [Ripristino di emergenza e disponibilità elevata per le applicazioni Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Indicazioni tecniche sulla resilienza di Azure](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>Procedure consigliate
Si consiglia di copiare l'account archivio Data Lake di tooanother dati critici in un'altra area con una frequenza allineata toohello le esigenze del piano di ripristino di emergenza. Esistono diversi metodi toocopy dati inclusi [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) o [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md). Azure Data Factory è un servizio utile per creare e distribuire pipeline di spostamento dati a intervalli ricorrenti.

Se si verifica un'interruzione dell'alimentazione locale, è quindi possibile accedere ai dati nell'area di hello in cui è stati copiati i dati hello. È possibile monitorare hello [Dashboard di integrità del servizio di Azure](https://azure.microsoft.com/status/) toodetermine hello globo hello lo stato di servizio di Azure.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>Indicazioni per il ripristino dal danneggiamento o dall'eliminazione accidentale dei dati
Anche se Azure Data Lake Store offre la resilienza dei dati tramite le repliche automatiche, ciò non impedisce all'applicazione o agli sviluppatori/utenti di danneggiare i dati o di eliminarli accidentalmente.

#### <a name="best-practices"></a>Procedure consigliate
l'eliminazione accidentale di tooprevent, è consigliabile impostare i criteri di accesso corretto hello per l'account archivio Data Lake.  Ciò include l'applicazione [blocchi di risorse di Azure](../azure-resource-manager/resource-group-lock-resources.md) toolock verso il basso importanti risorse nonché applicazione account e i file di accesso a livello del controllo utilizzando hello disponibile [funzionalità di sicurezza di archivio Data Lake](data-lake-store-security-overview.md). È anche opportuno creare regolarmente copie dei dati critici usando [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) o [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) in un altro account Data Lake Store, in una cartella o in una sottoscrizione di Azure.  Può trattarsi di toorecover utilizzato da un problema di danneggiamento o eliminazione di dati. Azure Data Factory è un servizio utile per creare e distribuire pipeline di spostamento dati a intervalli ricorrenti.

Le organizzazioni possono anche abilitare [registrazione diagnostica](data-lake-store-diagnostic-logs.md) per loro archivio Azure Data Lake account toocollect itinerari di controllo di accesso ai dati che fornisce informazioni che potrebbe essere stato eliminato o aggiornato un file.

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione ad Azure Data Lake Store](data-lake-store-get-started-portal.md)
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)

