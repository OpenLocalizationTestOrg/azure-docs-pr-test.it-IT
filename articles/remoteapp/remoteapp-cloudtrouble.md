---
title: raccolte di cloud di RemoteApp aaaTroubleshoot - creazione | Documenti Microsoft
description: Informazioni su come tootroubleshoot RemoteApp cloud errori nella creazione di raccolta
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Risoluzione dei problemi di creazione di raccolte di cloud di RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Se si riscontrano problemi durante la creazione di una raccolta nel cloud, controllare hello le seguenti informazioni.

## <a name="your-image-is-invalid"></a>L'immagine non è valida
Se viene visualizzato un messaggio ad esempio, "GoldImageInvalid" quando si resta in attesa per Azure tooprovision la raccolta, significa che l'immagine modello non soddisfa hello [definito requisiti immagine](remoteapp-imagereqs.md). In tal caso, passare a leggere quelli [requisiti](remoteapp-imagereqs.md), correggere l'immagine e si tenta di toocreate nuovamente la raccolta.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Errori comuni visualizzati nel portale di gestione di Azure hello
    DNS server could not be reached
    ProvisioningTimeout

La creazione di raccolte cloud spesso non riesce perché si usano immagini personalizzate.  Se si verifica uno di hello sopra gli errori e si utilizza una raccolta di hello toocreate immagine personalizzata, verificare hello seguenti operazioni:

* Assicurarsi che immagine personalizzata hello caricato soddisfi i requisiti di immagine.
* In genere hello problema comune è che l'immagine hello non è stato correttamente preparata con Sysprep.  
* Verificare immagine hello possibile avvio all'interno di Hyper-V o provare a creare una VM IAAS direttamente nella sottoscrizione di Azure utilizzando l'immagine di hello. Se hello macchina virtuale non riesce tooboot e non avviare, quindi questo indica in genere che tale immagine personalizzata hello non è stato preparato correttamente.  Verificare l'immagine personalizzata hello è stato compilato in seguito hello come toocreate immagine di un modello personalizzato per RemoteApp

Se si utilizza una delle immagini di Microsoft hello incluse con la sottoscrizione, provare di nuovo insieme di toocreate hello. Se hello problema persiste, contattare il supporto tecnico Microsoft.

    PlatformImageTrialModeOnly

Se questo errore viene visualizzato in genere significa che è stato aggiornato tooa pagato account ma che si sta tentando di toouse un'immagine forniti da Microsoft che è valida solo durante la modalità di valutazione del servizio hello hello. In questo caso, provare a ripetere la raccolta cloud toocreate, ma essere toospecify che l'immagine corretta hello.

