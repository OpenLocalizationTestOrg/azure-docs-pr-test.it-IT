---
title: "Azure RemoteApp: in che modo la larghezza di banda di rete influisce sulla qualità dell'esperienza? | Microsoft Docs"
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
ms.openlocfilehash: 74116902e973fba440b3c662fdf76202d052b4c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp: in che modo la larghezza di banda di rete influisce sulla qualità dell'esperienza?
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Quando si esamina la [larghezza di banda di rete complessiva](remoteapp-bandwidth.md) necessaria per Azure RemoteApp, tenere presenti i fattori descritti di seguito. Questi fanno tutti parte di un sistema dinamico che influisce sulla soddisfazione complessiva degli utenti. 

* **Larghezza di banda disponibile e condizioni della rete** : una serie di parametri, come perdita, latenza e instabilità, nella stessa rete in un determinato momento può influire sull'esperienza di streaming delle applicazioni, offrendo un'esperienza utente complessiva di livello inferiore. La larghezza di banda disponibile nella rete è un fattore importante nei casi di congestione, perdita casuale e latenza, perché tutti questi parametri influiscono sul meccanismo di controllo della congestione, che a sua volta controlla la velocità di trasmissione per evitare conflitti.  Ad esempio, una rete con perdita di dati o con latenza elevata rende spiacevole l'esperienza utente anche con una larghezza di banda di 1000 MB. La perdita e la latenza variano in base al numero di utenti connessi alla rete e alle operazioni che tali utenti stanno svolgendo, ad esempio streaming video, download o upload di file di grandi dimensioni, stampa.
* **Scenario di utilizzo**: l'esperienza dipende sia dalle operazioni eseguite dai singoli utenti che dagli utenti della rete nel loro complesso. Ad esempio, la lettura di una diapositiva richiede l'aggiornamento di un solo fotogramma. Se l'utente legge rapidamente e scorre il contenuto di un documento di testo, è necessario aggiornare un numero maggiore di fotogrammi al secondo. La comunicazione di andata e ritorno al server in questo scenario finisce per consumare una maggiore larghezza di banda di rete. Si consideri inoltre un esempio estremo: più utenti che guardano video ad alta definizione (ad esempio con risoluzione 4K), partecipano a conferenze telefoniche HD, giocano con videogiochi 3D o usano sistemi CAD. Tutto questo può rendere praticamente inutilizzabile anche una rete con una larghezza di banda molto elevata.
* **Risoluzione dello schermo e numero di schermi** : è necessaria una maggiore larghezza di banda di rete per aggiornare completamente schermi più grandi rispetto a schermi più piccoli. La tecnologia sottostante è molto efficiente nella codifica e nella trasmissione delle sole aree delle schermate effettivamente da aggiornare, ma a volte deve essere aggiornata l'intera schermata. Quando l'utente dispone di uno schermo con risoluzione superiore (ad esempio a 4K), l'aggiornamento richiede maggiore larghezza di banda di rete rispetto a uno schermo con una risoluzione inferiore (ad esempio 1024x768 px). La stessa logica vale se si usano più schermi per il reindirizzamento. Maggiore il numero di schermi, maggiore deve essere la larghezza di banda.
* **Reindirizzamento degli Appunti e del dispositivo**: si tratta di un problema non molto evidente, ma in molti casi se un utente archivia una grande quantità di dati negli Appunti, è necessario un certo tempo per il trasferimento di tali informazioni dal client Desktop remoto al server. L'esperienza downstream può risentire dell'esperienza dell'invio del contenuto degli Appunti upstream. Lo stesso vale per il reindirizzamento del dispositivo. Se uno scanner o una webcam produce una grande quantità di dati da inviare upstream al server, una stampante deve ricevere un documento di grandi dimensioni oppure una risorsa di archiviazione locale deve essere disponibile per un'app in esecuzione nel cloud per la copia di un file di grandi dimensioni, gli utenti potrebbero notare la perdita di fotogrammi o blocchi temporanei dei video, perché i dati necessari per il reindirizzamento del dispositivo richiedono una maggiore larghezza di banda di rete. 

Quando si valutano le esigenze relative alla larghezza di banda di rete, è necessario tenere conto del fatto che l'impatto di tutti questi fattori è il risultato della combinazione di questi ultimi.

Tornare ora all'[articolo principale sulla larghezza di banda di rete](remoteapp-bandwidth.md) o passare al test della [larghezza di banda di rete](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Altre informazioni
* [Uso previsto della larghezza di banda di rete di Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp: scenari comuni di test relativi all'utilizzo della larghezza di banda di rete](remoteapp-bandwidthtests.md)
* [Larghezza di banda di rete di Azure RemoteApp: linee guida generali (se non è possibile verificare direttamente)](remoteapp-bandwidthguidelines.md)

