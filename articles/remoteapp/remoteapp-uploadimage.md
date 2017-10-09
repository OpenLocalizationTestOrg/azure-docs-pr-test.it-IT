---
title: un'immagine personalizzata per Azure RemoteApp aaaUpload | Documenti Microsoft
description: Informazioni su come tooupload immagine di un oggetto personalizzato per Azure RemoteApp
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Caricare un'immagine personalizzata per RemoteApp di Azure
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Dopo aver creato l'immagine modello personalizzato o lo abbia aggiornato con le modifiche, è necessario tooupload tale libreria di immagini immagine tooyour Azure RemoteApp. Usare i passaggi seguenti.

## <a name="before-you-start"></a>Prima di iniziare
1. Verificare che l'immagine personalizzata soddisfi hello [requisiti dell'immagine](remoteapp-imagereqs.md) e [requisiti dell'applicazione](remoteapp-appreqs.md).
2. Installare hello [modulo Azure PowerShell](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Procedura dettagliata su come immagine personalizzata tooupload
1. Aprire il portale di gestione di Azure e passare toohello RemoteApp pagina.
2. In hello **immagini modello** scheda, fare clic su **caricare** nella parte inferiore di hello della pagina hello.
3. Immettere un nome descrittivo per l'immagine e specificare una posizione dell'account di archiviazione hello. Verificare che il percorso di hello è hello stesso percorso la raccolta RemoteApp o in un percorso in cui si desidera toocreate uno.
4. Quando richiesto, scaricare hello script tooyour PC locale.
5. Copiare i parametri del comando hello negli Appunti tooyour casella di testo hello.
6. Aprire una finestra di Windows PowerShell con privilegi elevati.
7. Da hello finestra Windows PowerShell con privilegi elevati passare toohello stessa directory in cui è stato scaricato script hello.
8. Hello Incolla copiati comando e premere **invio**.
   
   verrà avviato il processo di caricamento Hello e durata può dipendere da molti fattori, tra cui la velocità di rete e le dimensioni dell'immagine di hello
9. Se il caricamento non riesce a causa di interruzioni di rete o elementi simili, è sempre possibile riprendere il processo di caricamento hello che è stata avviata. tooresume un'operazione di caricamento, eseguire script hello utilizzando hello stessa riga di comando.

> [!WARNING]
> Non modificare mai script caricamento hello. Controlli specifici sono stati implementati tooensure che hello immagine soddisfa i requisiti di immagine hello e requisiti dell'applicazione.
> 
> 

## <a name="common-problems"></a>Problemi frequenti
* Assicurarsi di usare Windows PowerShell, e non Azure PowerShell. Modulo di Azure PowerShell tooinstall hello è necessario perché alcuni moduli sono necessari durante il processo di caricamento hello.
* Non modificare script hello, le convalide sono disponibili per comodità.
* Se il file di disco rigido virtuale hello Ottiene bloccato durante il caricamento, copiare il file hello o spostarlo tooa nuovo percorso e il tentativo di caricare nuovamente. Il caricamento potrebbe essere ostacolato da qualche processo di Windows in esecuzione.  

