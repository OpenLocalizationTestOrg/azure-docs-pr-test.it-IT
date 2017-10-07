---
title: App aaaUsing App-V con Azure RemoteApp | Documenti Microsoft
description: Informazioni su come App toouse App-V in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Uso delle app App-V in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

È possibile usare le applicazioni App-V in una raccolta ibrida di Azure RemoteApp, che richiede l'aggiunta al dominio.

Prima di iniziare, verificare che client di App-V 5.1 hello tooinstall con gli aggiornamenti più recenti di hello. Sarà necessario toocreate un [immagine personalizzata](remoteapp-create-custom-image.md) che include il client App-V hello.  

È facile toouse infrastruttura App-V esistente con Azure RemoteApp. Poiché una raccolta ibrida è distribuita in una rete virtuale di Azure con controller di dominio di accesso tooyour e le macchine virtuali hello vengono aggiunti a un dominio, è possibile usare App-v dell'infrastruttura e la distribuzione metodi tooeasyily host App-V applicazione esistente in Azure RemoteApp. Di seguito sono riportate alcune considerazioni che è necessario tenere in base al tipo di hello della distribuzione di App-V che è installata:

| Opzioni di configurazione |  | Positive | Negative |
| --- | --- | --- | --- |
| Metodo di distribuzione |Streaming (su richiesta) |App è sempre hello nuova e più recente |Prima latenza |
| Montato |Più veloce; App è già presente nel hello VM |Bloat: occupa lo spazio dell'immagine (limite di 127 GB) | |
| Archiviazione percorso app |Contenuto condiviso |App eseguita nella memoria dell'istanza di Azure RemoteApp |Mostro memoria e il server di collegamento toostreaming (file) in cui risiede l'applicazione hello |
| Disco (memorizzato nella cache) |Esecuzione rapida. Applicazione non dipende dalla disponibilità dell'origine del contenuto |Bloat: occupa lo spazio dell'immagine (limite di 127 GB) | |
| Destinazione |Utente |Richiede un'infrastruttura App-V autonoma completa | |
| Globale (computer) |Prepubblicazione o destinazione mediante server di pubblicazione |Necessario tooupdate l'immagine di Azure, se si desidera app hello tooupdate (grande). Occupa spazio nell'immagine. | |

 Dopo aver creato l'immagine personalizzata e la raccolta ibrida, pubblicare l'applicazione, assegnare gli utenti e sfruttare le applicazioni App-V esistenti ospitate in Azure RemoteApp recapitati tooany dispositivo ovunque.

