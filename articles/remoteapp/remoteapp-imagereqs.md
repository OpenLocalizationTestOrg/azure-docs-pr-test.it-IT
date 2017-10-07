---
title: requisiti immagine di RemoteApp aaaAzure | Documenti Microsoft
description: Informazioni sui requisiti di hello per la creazione di immagini toobe utilizzato con Azure RemoteApp
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
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Requisiti per le immagini di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp utilizza un toohost immagine di Windows Server 2012 R2 tutti i programmi di hello che si desidera tooshare con gli utenti. toocreate un'immagine personalizzata, è possibile iniziare con un'immagine esistente o [crearne uno nuovo](remoteapp-create-custom-image.md).

> [!TIP]
> Non tutti sanno che i consente di sottoscrizione di Azure RemoteApp in che accedere tooa immagine di Windows Server 2012 R2 hello raccolta di macchine Virtuali di Azure che è possibile utilizzare toocreate la propria immagine modello. [Provare](remoteapp-image-on-azurevm.md).  
> 
> 

i requisiti per l'immagine di hello che può essere caricato per l'utilizzo con Azure RemoteApp Hello sono:

* Applicazioni personalizzate non archiviano i dati in locale nell'immagine di hello. Queste immagini sono senza stato e devono contenere solo le applicazioni.
* immagine di Hello non contiene dati che possono essere persi.
* dimensioni dell'immagine Hello devono essere un multiplo del numero di MB. Se si tenta di tooupload un'immagine che non è un multiplo esatto, caricamento hello avrà esito negativo.
* dimensioni dell'immagine Hello devono essere 127 GB o più piccoli.
* Deve essere inclusa in un file VHD (i file VHDX non sono attualmente supportati).
* Hello disco rigido virtuale non deve essere una macchina virtuale di generazione 2.
* è possibile Hello disco rigido virtuale a dimensione fissa o ad espansione dinamica. Un disco rigido virtuale ad espansione dinamica è consigliato perché richiede meno tooAzure tooupload tempo rispetto a un file di disco rigido virtuale a dimensione fissa.
* Hello disco deve essere inizializzato con stile di partizionamento hello il record di avvio principale (MBR, Master Boot Record). Hello stile di partizione GUID partizione GPT (tabella) non è supportata.
* Hello VHD deve contenere una singola installazione di Windows Server 2012 R2. Può contenere più volumi, ma solo uno che contiene un'installazione di Windows.
* ruolo di Hello sessione Desktop remoto Host () e funzionalità esperienza Desktop hello devono essere installati.
* ruolo Gestore connessione Desktop remoto Hello deve *non* installato.
* Hello Encrypting File System (EFS) deve essere disabilitato.
* Hello immagine deve essere preparata con Sysprep utilizzando parametri hello **/oobe /generalize /shutdown** (non utilizzare hello **/mode: VM** parametro).
* Il caricamento del disco VHD da una catena di snapshot non è supportato.

Vedere [Creare un'immagine di Azure RemoteApp](remoteapp-imageoptions.md) per ulteriori informazioni sulla creazione di immagini per Azure RemoteApp.

