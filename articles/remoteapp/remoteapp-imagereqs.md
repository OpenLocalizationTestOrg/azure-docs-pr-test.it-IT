---
title: Requisiti delle immagini di Azure RemoteApp | Documentazione Microsoft
description: Informazioni sui requisiti per la creazione di immagini da usare con Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Requisiti per le immagini di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Azure RemoteApp usa un'immagine di Windows Server 2012 R2 per ospitare tutti i programmi da condividere con gli utenti. Per creare un’immagine personalizzata, è possibile iniziare con un’immagine esistente oppure [crearne una nuova](remoteapp-create-custom-image.md).

> [!TIP]
> Non tutti sanno che la sottoscrizione di Azure RemoteApp consente di accedere a un'immagine di Windows Server 2012 R2 nella raccolta di VM di Azure che è possibile usare per creare la propria immagine modello. [Provare](remoteapp-image-on-azurevm.md).  
> 
> 

I requisiti per l'immagine che possono essere caricati e usati con l'app Azure RemoteApp sono i seguenti:

* Le applicazioni personalizzate non archiviano dati in locale nell'immagine. Queste immagini sono senza stato e devono contenere solo le applicazioni.
* L'immagine non contiene dati che possono essere persi.
* La dimensione dell'immagine dev'essere un multiplo di MB. Se si prova a caricare un'immagine che non è un multiplo esatto, l'operazione non andrà a buon fine.
* L'immagine deve avere una dimensione massima di 127 GB.
* Deve essere inclusa in un file VHD (i file VHDX non sono attualmente supportati).
* Il file VHD non deve essere una macchina virtuale di seconda generazione.
* Il file VHD può essere di dimensioni fisse o a espansione dinamica. È consigliabile un file VHD a espansione dinamica perché i tempi di caricamento di questo file in Azure sono inferiori rispetto a uno di dimensioni disse.
* Il disco deve essere inizializzato con lo stile di partizione MBR (Master Boot Record). Lo stile di partizione basato sulla tabella di partizione GUID (GPT) non è supportato.
* Il file VHD deve contenere una singola installazione di Windows Server 2012 R2. Può contenere più volumi, ma solo uno che contiene un'installazione di Windows.
* È necessario installare il ruolo Host sessione Desktop remoto e la funzionalità Esperienza desktop.
* Il ruolo Gestore connessione Desktop remoto *non* deve essere installato.
* EFS (Encrypting File System) deve essere disabilitato.
* L'immagine deve essere preparata con SYSPREP usando i parametri **/oobe /generalize /shutdown** (NON usare il parametro **/mode:vm**).
* Il caricamento del disco VHD da una catena di snapshot non è supportato.

Vedere [Creare un'immagine di Azure RemoteApp](remoteapp-imageoptions.md) per ulteriori informazioni sulla creazione di immagini per Azure RemoteApp.

