---
title: procedure consigliate di RemoteApp aaaAzure | Documenti Microsoft
description: Procedure consigliate per la configurazione e l'uso di Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Procedure consigliate per la configurazione e l'uso di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) per informazioni dettagliate.
> 
> 

Hello le seguenti informazioni consentono di configurare e utilizzare Azure RemoteApp in modo efficiente.

## <a name="connectivity"></a>Connettività
* Utilizzare sempre hello client più recente. L'uso di client meno recenti potrebbe causare problemi di connettività e altre situazioni di funzionalità ridotta. Abilitazione degli aggiornamenti automatici delle applicazioni per il dispositivo verificare che tale client più recente di hello viene sempre installato.
* Utilizzare sempre hello più stabile e affidabile internet connessione disponibile tooyou.  
* Usare solo connessioni proxy supportate per prestazioni di connettività ottimali.  proxy SOCKS Hello non è supportata.

## <a name="applications"></a>Applicazioni
* Salvare e chiudere le applicazioni RemoteApp al termine con un'applicazione hello. Non chiudere un'applicazione hello potrebbe comportare la perdita di dati.
* Convalidare le applicazioni personalizzate prima di usarle in Azure RemoteApp. Ciò include la verifica che su una piattaforma di sessione di lavoro e non utilizzare le risorse non necessarie, ad esempio memoria e CPU che potrà esaurire un altro utente in hello stessa raccolta. Per informazioni, scaricare e consultare hello [compatibilità procedure consigliate per applicazioni per Servizi Desktop remoto](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Configurazione e gestione
* Mantenere le immagini modello backup toodate, l'installazione degli aggiornamenti software e altre correzioni importanti, in base alle esigenze. In questo modo si garantisce che in Azure RemoteApp. auto-scale toomeet della capacità, ogni istanza applicazione di una patch.  
* Assicurarsi che la distribuzione di Active Directory Federation Services (ADFS) sia protetta e affidabile. In caso contrario le autenticazioni client potrebbero non riuscire, impedendo agli utenti di accedere ad Azure RemoteApp.
* Configurare immagini modello con le applicazioni, i ruoli o le funzionalità installate, in modo che siano prive di stato. Non basarsi su tutte le istanze di macchine virtuali hello in un servizio di RemoteApp in uno stato persistente.
  * Archiviare tutti i dati utente in profili utente o un altro servizio di archiviazione percorsi toohello esterno, ad esempio on-premise le condivisioni file o OneDrive.
  * Archiviare dati condivisa nel servizio esterno toohello posizioni di archiviazione, ad esempio on-premise le condivisioni file o OneDrive.
  * Configurare le impostazioni a livello di sistema nell'immagine modello hello anziché sulle singole macchine virtuali in un servizio.
  * Disabilitare gli aggiornamenti software automatici per le applicazioni pubblicate - invece applicarli manualmente immagine modello toohello e testarle prima di distribuire il modello di hello.

