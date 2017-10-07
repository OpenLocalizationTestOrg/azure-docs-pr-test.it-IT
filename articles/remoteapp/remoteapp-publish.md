---
title: un'app in Azure RemoteApp aaaPublish | Documenti Microsoft
description: Informazioni su come toopublish applicazioni e risorse in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>Come toopublish un'app in RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Dopo aver creato la raccolta RemoteApp, è necessario toopublish hello applicazioni o risorse che si desidera toomake disponibili per gli utenti. Hello immagini modello fornite con la sottoscrizione solo con pochi App pubblicato per impostazione predefinita - tooshare hello altre App, è necessario toopublish li.

> [!NOTE]
> È necessario tooupdate un'app? È necessario troppo[aggiornamento hello immagine](remoteapp-update.md) prima.
> 
> 

In hello **pubblicazione** , fare clic nel portale di hello **pubblica**. È possibile aggiungere un'app dall'immagine modello **avviare** menu o fornire hello percorso toowhere hello app viene installata in immagine modello hello. Se si sceglie tooadd da hello **avviare** menu, scegliere hello app toopublish dall'elenco di hello. Se si sceglie tooprovide hello percorso toohello app, immettere un nome per l'applicazione hello e hello percorso toohello app. Utilizzare le variabili di percorso hello - ad esempio, "% systemdrive %" invece di "c:\".

> [!NOTE]
> Se si vuole che l'app da hello tooadd **avviare** menu, è necessario toohave *aggiunto tale toohello app **avviare** menu l'immagine modello.* In caso contrario, RemoteApp verranno visualizzati solo ciò che *è* su hello **avviare** menu e si verrà confondere. 
> 
> toomake che l'app è in hello **avviare** menu, inserire un file di collegamento - **lnk** : hello %systemdrive%\ProgramData\Microsoft\Windows\Start Avvio\Programmi cartella.
> 
> Se si è dimenticato tooadd hello app toohello **avviare** menu quando è stato creato il modello di hello, scegliere tooadd hello percorso toohello app. (in alternativa, ricreare l'immagine modello, tuttavia questa procedura è piuttosto complicata).
> 
> 

