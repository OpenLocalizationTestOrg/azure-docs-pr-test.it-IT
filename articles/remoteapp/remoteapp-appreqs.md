---
title: aaaApp requisiti per Azure RemoteApp | Documenti Microsoft
description: Informazioni sui requisiti di hello per le app che si desidera toouse in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>Requisiti delle app
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp supporta applicazioni basate su Windows a 32 bit o a 64 bit in streaming Windows da un'immagine di Windows Server 2012 R2. La maggior parte delle applicazioni basate su Windows a 32 bit o a 64 bit vengono eseguite "così come sono" in un ambiente Azure RemoteApp (Servizi Desktop remoto, in precedenza noti come Servizi terminal). Tuttavia, esiste una differenza tra esecuzione e corretta esecuzione: alcune applicazioni funzionano correttamente e offrono buone prestazioni, mentre altre no. Hello le seguenti informazioni vengono fornite indicazioni per lo sviluppo di applicazioni in un ambiente di Servizi Desktop remoto e la verifica della compatibilità tooensure.

Suggerimento: è in corso la creazione di alcuni esempi di app per gli utenti. Verranno pubblicati altri argomenti sull'uso di Microsoft Access, QuickBooks e App-V in RemoteApp.

## <a name="requirements"></a>Requisiti
Questi tre requisiti, se seguiti, contribuiscono a una corretta esecuzione dell'applicazione in RemoteApp:

1. Le applicazioni che soddisfano tutte [requisiti di certificazione per le app desktop di Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) e rispettare troppo[Servizi Desktop remoto, le linee guida di programmazione](https://msdn.microsoft.com/library/aa383490.aspx) avrà compatibilità completa con RemoteApp.
2. Applicazioni non devono mai archiviare dati in locale nell'immagine di hello o istanze di RemoteApp che possono essere perse.  Dopo aver creato una raccolta RemoteApp, le istanze di hello vengono clonate e sono senza state e devono contenere solo le applicazioni. Archiviare i dati in un'origine esterna o all'interno di hello del profilo utente.
3. Le immagini personalizzate non devono mai contenere dati che possono essere persi.  

## <a name="testing-your-apps"></a>Test delle app
Utilizzare queste applicazioni tootesting passaggi:

1. Installare Windows Server 2012 R2 e l'applicazione
2. Abilitare Desktop remoto
3. Creare due account utente, UserA e UserB, aggiunta di entrambi gruppo di sicurezza utente account toohello Desktop remoto.
4. Verificare la compatibilità di multi-sessione definendo due toohello di sessioni di servizi desktop remoto PC simultanee durante l'avvio di un'applicazione hello.
5. Convalidare il comportamento dell'app

## <a name="application-development-guidelines"></a>Linee guida sullo sviluppo di applicazioni
Utilizzare hello alle linee guida per lo sviluppo di applicazioni per RemoteApp.

### <a name="multiple-users"></a>Più utenti
* L'installazione di un' [applicazione per un singolo utente ](https://msdn.microsoft.com/library/aa380661.aspx)può creare problemi in un ambiente multiutente.
* Le applicazioni devono [archiviare informazioni specifiche dell'utente](https://msdn.microsoft.com/library/aa383452.aspx) in posizioni specifiche dell'utente, separatamente dalle informazioni globali che si applica agli utenti di tooall.
* RemoteApp usa più [spazi dei nomi per gli oggetti del kernel](https://msdn.microsoft.com/library/aa382954.aspx); uno spazio dei nomi globale viene usato principalmente dai servizi nelle applicazioni client/server.
* Non è sicuro tooassume che hello Nome computer o hello [indirizzo IP](https://msdn.microsoft.com/library/aa382942.aspx) computer assegnato toohello sono associati a un singolo utente poiché più utenti possono accedere simultaneamente tooa Host sessione Desktop remoto (la sessione Desktop remoto Server host).

### <a name="performance"></a>Prestazioni
* Disabilitare [effetti grafici](https://msdn.microsoft.com/library/aa380822.aspx) prima di aggiungere tooRemoteApp l'app.
* disabilitare la disponibilità di toomaximize della CPU per tutti gli utenti, [attività in background ](https://msdn.microsoft.com/library/aa380665.aspx) o creare attività in background efficiente che non sono a elevato utilizzo di risorse.
* È consigliabile ottimizzare e bilanciare l' [utilizzo del thread](https://msdn.microsoft.com/library/aa383520.aspx) dell'applicazione per un ambiente multiutente e multiprocessore.
* toooptimize prestazioni, è consigliabile per le applicazioni troppo[rilevare](https://msdn.microsoft.com/library/aa380798.aspx) se sono in esecuzione in una sessione client.

