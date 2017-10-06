---
title: archivio aaaNever i dati sensibili nel immagini personalizzate per Azure RemoteApp | Documenti Microsoft
description: Informazioni sulle linee guida hello per l'archiviazione dei dati in immagini personalizzate in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Non archiviare mai dati sensibili in immagini personalizzate
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Quando si ospita l'applicazione in Azure RemoteApp, hello primo passaggio consiste toocreate un'immagine personalizzata. Utilizziamo che istanze VM toocreate immagine personalizzata che servono le app agli utenti di tooyour. immagine personalizzata Hello deve contenere solo le applicazioni e dati sensibili mai che possono essere persi, ad esempio i database SQL, file personale o file di dati speciali ad esempio i file aziendali QuickBooks. Tutti i dati sensibili devono trovarsi tooAzure esterno RemoteApp in un file server, un'altra macchina virtuale di Azure, o in SQL Azure. immagine di Hello deve semplicemente un'applicazione hello host che si connette toohello origine dei dati e presenta i dati di hello. Per altre informazioni vedere [Requisiti per le immagini di Azure RemoteApp](remoteapp-imagereqs.md) . 

toounderstand perché è consigliabile non archiviare i dati sensibili, è necessario toounderstand funzionamento di Azure RemoteApp. Quando una raccolta viene creata o aggiornata, in background hello cloni più copie dell'immagine di hello vengono create. Tutte le istanze di macchina virtuale sono repliche esatte dell'immagine personalizzata hello; Quando gli utenti di avviare le applicazioni sono connessi tooone di queste istanze di macchina virtuale. Ma non è garantito hello stessa istanza e non è importante perché sono non persistenti. Hello istanze di macchina virtuale, le applicazioni di hosting hello non sono permanenti e possono essere eliminato in modo permanente o eliminati in base, ad esempio, durante l'aggiornamento della raccolta. 

Una volta raccolta hello viene eseguito il provisioning e gli utenti avviano toohello connessione macchine virtuali, i dati utente sono persistenti e protetti poiché viene salvato in archiviazione separata all'interno di un disco rigido virtuale che si chiama un [disco (UPD)](remoteapp-upd.md), ovvero profilo utente hello in c:\users\<userprofile >. Avvio di un'applicazione hello UPD viene montato e considerato come un profilo utente locale dal sistema operativo hello. Altre informazioni su come [Azure RemoteApp salva dati e impostazioni](remoteapp-upd.md).

Dati di esempio che non devono trovarsi nell'immagine hello:

* Dati condivisi per gli utenti tooaccess
* SQL DB o QuickBooks DB
* Tutti i dati in D:\

Dati di esempio che possono risiedere in hello predefinito profilo toobe vengono copiati in UPD ogni degli utenti:

* File di configurazione di ogni utente
* Script che gli utenti devono mantenere nel loro disco profili utente

Punti principali:

* Non memorizzare mai dati sensibili che possono essere perso sull'immagine di hello durante la creazione di un'immagine personalizzata.
* Dati sensibili sempre deve risiedere in un file server separato, separare le VM di Azure, in cloud hello e toohello sempre esterno istanze della macchina virtuale che ospita le applicazioni all'interno di Azure RemoteApp. 
* Dati utente viene salvati e viene mantenuto nel disco di profilo utente hello (UDP)

