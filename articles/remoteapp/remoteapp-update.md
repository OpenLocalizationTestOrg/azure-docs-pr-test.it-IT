---
title: aaaUpdate la raccolta RemoteApp di Azure | Documenti Microsoft
description: Informazioni su come tooupdate raccolta di Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Aggiornare una raccolta in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Non esiste, verrà un'ora, inevitabilmente, quando è necessario tooupdate hello App o l'immagine nella raccolta di Azure RemoteApp. Se si utilizza una delle immagini hello incluse con la sottoscrizione di Azure RemoteApp, insieme a un cloud o ibrida, che tutti gli aggiornamenti vengono gestiti da Azure RemoteApp, pertanto è possibile posizionare semplice.

Tuttavia, se si utilizza un'immagine personalizzata (che è stato generato da zero o creato mediante la modifica di uno dei nostri immagini), è responsabile della gestione di App e l'immagine di hello. Se è necessario tooupdate un'immagine o una qualsiasi delle App hello in essa contenuti, è necessario toocreate una nuova versione aggiornata dell'immagine di hello e quindi sostituire hello esistente immagine nella raccolta con la nuova immagine aggiornata.

Quindi, come si esegue l'aggiornamento della raccolta? È piuttosto semplice:

1. Aggiornare l'immagine di hello utilizzati nella raccolta. Applicare le patch o gli aggiornamenti necessari e quindi salvarla con un nuovo nome.
2. [Caricare](remoteapp-uploadimage.md) o [importare](remoteapp-image-on-azurevm.md) tooRemoteApp tale immagine.
3. A questo punto, nella pagina insieme hello, fare clic su **aggiornamento**.
4. Scegliere nuova immagine hello hello **immagine modello** elenco.
5. Di seguito è la parte più impegnativa hello, è necessario toodecide come toodeal con tutti gli utenti che attualmente utilizzano un'app nella raccolta di hello. È necessario hello opzioni seguenti:
   
   * **Concedi agli utenti 60 minuti dopo l'aggiornamento di hello**. Non appena hello aggiornamento è completato, Azure RemoteApp verrà visualizzato un messaggio tooany gli utenti attivi informa toosave loro lavoro e log off e accedere di nuovo. Dopo 60 minuti, tutti gli utenti attivi che non si sono disconnessi vengono disconnessi automaticamente. Gli utenti possono accedere di nuovo immediatamente.
   * **Disconnettere gli utenti immediatamente**. Non appena hello aggiornamento è completato, disconnettersi da tutti gli utenti automaticamente senza alcun avviso. Se si sceglie questa opzione, gli utenti potrebbero perdere i dati. Tuttavia, possono comunque riconnettersi app toohello immediatamente.
6. Fare clic su hello segno di spunta toostart hello aggiornamento.

