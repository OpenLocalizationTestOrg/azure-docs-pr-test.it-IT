---
title: utilizzo della larghezza di banda di rete di Azure RemoteApp aaaEstimate | Documenti Microsoft
description: Informazioni sui requisiti di larghezza di banda di rete hello per le applicazioni che le raccolte RemoteApp di Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Uso previsto della larghezza di banda di rete di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp utilizza hello Remote Desktop Protocol (RDP) toocommunicate tra le applicazioni in esecuzione nel cloud di Azure hello e gli utenti. Questo articolo fornisce alcune linee guida di base che è possibile utilizzare tooestimate utilizzo della rete e la valutazione potenzialmente l'utilizzo della larghezza di banda di rete per ogni utente di Azure RemoteApp.

La stima dell'utilizzo della larghezza di banda per utente è molto complessa e richiede l'esecuzione di più applicazioni contemporaneamente all'interno di scenari multitasking in cui le applicazioni possono influire sulle prestazioni le une delle altre in base alla richiesta di larghezza di banda di ognuna. Tipo anche hello del client Desktop remoto (ad esempio, i client Mac e i client HTML5) può provocare risultati di larghezza di banda toodifferent. toohelp che seguendo questi problemi, di interruzione scenari di utilizzo di hello in alcuni degli scenari reali tooreplicate hello comuni categorie. (Dove uno scenario reale hello è, naturalmente, una combinazione di categorie e differisce dall'utente.)

Prima di continuare, tenere presente che si suppone RDP offre un'esperienza ottimale tooexcellent per la maggior parte degli scenari di utilizzo su reti con una latenza inferiore a 120 ms e larghezza di banda su 5 MB - si basa su toodynamically possibilità di RDP regolare tramite la rete disponibile hello larghezza di banda e hello stimato applicazione alle esigenze di larghezza di banda. In questo articolo va oltre quelli toolook "la maggior parte degli scenari di utilizzo" bordo hello, in scenari iniziano toounwind ed esperienza utente inizia toodegrade.

Ora l'estrazione hello seguenti articoli per i dettagli di hello, inclusi i fattori tooconsider, indicazioni di base e ciò che è non include il nostro stime.

* [In che modo la larghezza di banda di rete influisce sulla qualità dell'esperienza?](remoteapp-bandwidthexperience.md)
* [Scenari comuni di test relativi all'utilizzo della larghezza di banda di rete](remoteapp-bandwidthtests.md)
* [Linee guida rapide se non si dispone di hello ora o sulla capacità tootest](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>Cosa non è considerato
Quando si rivede hello proposta di test e questi consigli generali (e assolutamente generici), tenere presente che vi sono molti i fattori che non vengono prese in considerazione. Ad esempio, hello complicazioni esperienza utente forniti dalla natura asimmetrica di hello del caricamento e download della larghezza di banda. natura asimmetrica di Hello della maggior parte delle reti Wi-Fi inoltre avrà un impatto sulle prestazioni di hello e percezione di esperienza utente hello. Per gli scenari interattivi traffico downstream hello potrebbe avere una priorità inferiore rispetto alle hello a monte, che può aumentare il numero di hello dei fotogrammi video o audio persi e pertanto influire sulla percezione di utente hello di hello dei flussi. È possibile eseguire la propria toosee esperimenti che cos'è utile per il caso di utilizzo specifico e la rete.

Anche se viene illustrato il reindirizzamento della periferica, è non tiene impatto della larghezza di banda di hello considerazione hello del traffico di rete causato dai dispositivi collegati, come archiviazione, stampanti, gli scanner, webcam e altri dispositivi USB. effetto Hello di tali dispositivi in genere picchi temporaneamente hello esigenze di larghezza di banda e scompare quando hello attività è stata completata. Se questo accade di frequente, tuttavia, la mancanza di larghezza di banda potrebbe rendersi evidente.

Inoltre non vengono trattati come un utente può influire sulle altri utenti all'interno di hello stessa rete. Ad esempio, un utente utilizza 4K video in rete 100 MB/s potrà un impatto significativo sul altri utenti nella stessa rete durante il tentativo toodo hello stessa attività. Sfortunatamente ottiene sempre più difficile impatto di hello toodetermine di uso simultaneo toogive una raccomandazione comune o comprensiva sulla modalità di funzionamento sistema hello in funzione di aggregazione. Possiamo dire è che hello sottostante tecnologia protocollo renderanno hello meglio la larghezza di banda disponibile hello, ma presenta alcune limitazioni.

