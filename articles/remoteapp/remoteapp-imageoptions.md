---
title: un'immagine di Azure RemoteApp aaaCreate | Documenti Microsoft
description: Informazioni sulle opzioni di hello disponibili per la creazione di immagini per Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Creare un'immagine di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp utilizza immagini toohold hello App che si condivide con gli utenti. (È acquisire l'immagine e usarlo come macchine virtuali toocreate - questo è l'accedono agli utenti di hello quando effettuano l'accesso in Azure RemoteApp.) toocreate una raccolta di Azure RemoteApp con la scelta delle applicazioni, anche se la cloud ibrida, è innanzitutto necessario creare un'immagine con le applicazioni installate. Quindi, creare una raccolta che utilizza quell'immagine, assegnare gli utenti toohello insieme e pubblicare gli utenti toothose app.

Per creare o usare le immagini sono disponibili diverse opzioni. Hello base [requisito](remoteapp-imagereqs.md) per un'immagine che eseguono Windows Server 2012 R2 e che hanno installato il ruolo hello sessione Desktop remoto Host (). Sarà interessante vedere come soddisfare questo requisito.

Sono disponibili le opzioni seguenti per quanto riguarda tooimages hello:

* È possibile importare e usare un' [immagine basata su una macchina virtuale di Azure](remoteapp-image-on-azurevm.md). Questa opzione è utile per le applicazioni line-of-business che richiedono impostazioni personalizzate. È possibile personalizzare hello immagine toowork per app hello.
* È possibile [creare e caricare un'immagine personalizzata](remoteapp-create-custom-image.md). Questa opzione è utile se si ha già un'immagine usata per la distribuzione locale di Servizi Desktop remoto.
* È possibile utilizzare uno di hello [immagini modello](remoteapp-images.md) inclusi nella sottoscrizione di RemoteApp. Queste immagini vengono create e gestiti da team RemoteApp hello e contengono alcune applicazioni standard (ad esempio applicazioni di Office hello) che è possibile rendere disponibili tooyour utenti. Si noti che solo immagine di Office 365 Pro Plus hello può essere utilizzata in un ambiente di produzione.

Indipendentemente da dove si ottenga un'immagine o modalità di creazione, è opportuno conoscere hello toomake [requisiti delle app](remoteapp-appreqs.md) tooensure che l'app funziona bene in RemoteApp. Quindi, hello è toocreate un [cloud](remoteapp-create-cloud-deployment.md) o [ibrida](remoteapp-create-hybrid-deployment.md) insieme.

