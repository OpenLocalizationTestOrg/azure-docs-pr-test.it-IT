---
title: "aaaAzure RemoteApp - modalità della larghezza di banda di rete e la qualità di verifica lavoro insieme? | Microsoft Docs"
description: "Informazioni su come la larghezza di banda di rete in Azure RemoteApp può influire sulla qualità dell'esperienza utente."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp: in che modo la larghezza di banda di rete influisce sulla qualità dell'esperienza?
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Quando si sta esaminando hello [globale della larghezza di banda di rete](remoteapp-bandwidth.md) richiesto per Azure RemoteApp, tenere hello presente seguenti fattori: questi rientrano tutti in un sistema dinamico che impatti hello soddisfazione degli utenti. 

* **Larghezza di banda disponibile e le condizioni della rete corrente** -un set di parametri (perdita, latenza, instabilità) nella stessa rete in un determinato momento hello può compromettere l'applicazione hello dei flussi, vale a dire un'esperienza utente complessiva abbassato. Hello larghezza di banda della rete è una funzione di congestione, perdita casuale, la latenza in quanto tutti questi parametri influiscono sul meccanismo di controllo della congestione hello, che nei controlli di attivazione hello conflitti tooavoid velocità di trasmissione.  Ad esempio, una rete di perdita di dati o una rete ad alta latenza verrà migliorare hello esperienza utente non valido anche in una rete con larghezza di banda di 1000 MB. Hello perdita e la latenza variano in base al numero di hello di utenti che si trovano in hello stessa rete e operazioni (ad esempio, riproduzione di video, download o caricamento di file di grandi dimensioni, stampa) agli utenti.
* **Scenario di utilizzo** -esperienza hello varia a seconda degli utenti a cui hello eseguono come utenti singoli e come un gruppo su hello stessa rete. Ad esempio, la lettura di una diapositiva richiede solo un singolo frame toobe aggiornata. Se l'utente hello skims e scorre il contenuto di hello di un documento di testo, è necessario un maggior numero di frame toobe aggiornati al secondo. Hello nuovamente la comunicazione e via toohello server in questo scenario il consumare maggiore larghezza di banda di rete. Si consideri inoltre un esempio estremo: più utenti che guardano video ad alta definizione (ad esempio con risoluzione 4K), partecipano a conferenze telefoniche HD, giocano con videogiochi 3D o usano sistemi CAD. Tutto questo può rendere praticamente inutilizzabile anche una rete con una larghezza di banda molto elevata.
* **Schermata di risoluzione e hello il numero delle schermate** -maggiore larghezza di banda di rete è toofull necessarie schermate più grande di aggiornamento più schermi più piccoli. tecnologia sottostante Hello non un processo di codifica e la trasmissione delle schermate di hello che sono state aggiornate solo le aree hello buona, ma raramente, schermo intero hello deve toobe aggiornato. Quando l'utente di hello dispone di uno schermo con risoluzione superiore (ad esempio risoluzione 4K), l'aggiornamento richiede maggiore larghezza di banda di rete di una schermata con una risoluzione inferiore (ad esempio 1024x768px). La stessa logica vale se si usano più schermi per il reindirizzamento. Larghezza di banda deve tooincrease con numero di hello delle schermate.
* **Il reindirizzamento degli Appunti e dispositivo** : si tratta di un problema non molto evidente, ma in molti casi se un utente archivia un grande blocco degli Appunti toohello dati richiede un po' di tempo per tale tootransfer informazioni dal client Desktop remoto hello toohello server. esperienza downstream Hello può essere interessato da un'esperienza di hello di invio del contenuto degli Appunti hello a monte. Hello vale anche per il reindirizzamento dei dispositivi - se uno scanner webcam produce una grande quantità di dati che necessita di server a monte toohello toobe inviato, o una stampante deve tooreceive un documento di grandi dimensioni o esigenze di archiviazione locale, all'indirizzo toobe tooan disponibili app in esecuzione in hello cloud toocopy un file di grandi dimensioni, è possibile notare fotogramma eliminato o temporaneamente "bloccato" video perché i dati di hello necessari per il reindirizzamento della periferica hello sta aumentando larghezza di banda hello è necessaria. 

Quando si valutano le esigenze di larghezza di banda di rete, verificare che tooconsider tutti questi fattori funziona come un sistema.

Tornare a questo punto, toohello [articolo larghezza di banda di rete principale](remoteapp-bandwidth.md), o lo spostamento del tootesting il [della larghezza di banda di rete](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Altre informazioni
* [Uso previsto della larghezza di banda di rete di Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp: scenari comuni di test relativi all'utilizzo della larghezza di banda di rete](remoteapp-bandwidthtests.md)
* [Larghezza di banda di rete di Azure RemoteApp: linee guida generali (se non è possibile verificare direttamente)](remoteapp-bandwidthguidelines.md)

