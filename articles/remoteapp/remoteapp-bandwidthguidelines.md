---
title: larghezza di banda RemoteApp aaaAzure - linee guida generali | Documenti Microsoft
description: Linee guida di base sulla larghezza di banda di rete per le raccolte e le app Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Larghezza di banda di rete di Azure RemoteApp: linee guida generali (se non è possibile verificare direttamente)
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Se non si dispone hello toorun ora o la funzionalità di hello [test della larghezza di banda di rete](remoteapp-bandwidthtests.md) per Azure RemoteApp, di seguito sono riportate alcune linee guida piuttosto generica che consentono di stimare la larghezza di banda di rete per ogni utente.

Se si dispone di una combinazione di questi scenari, non è consigliabile un valore minore di (o uguale a) 10 MB/s come hello larghezza di banda minima per le app moderne in un ambiente remoto connesso a Internet. Questo però, come si è detto, non garantisce un'esperienza utente superiore alla media.

## <a name="complex-powerpoint-simple-powerpoint"></a>Presentazioni complesse, presentazioni semplici
Azure RemoteApp funziona meglio in una LAN a 100 MB. In hello 10 MB/s rete profilo quando più del 5%, utente hello instabilità sopra ms 120 visualizzeranno un'esperienza di Media. A hello di 1 MB/s diverso è ritornare - ad esempio, in una presentazione, utente hello potrebbe non essere visibili transizioni animate affatto perché i frame vengono ignorati.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, PDF misto, PDF, testo
Profilo di rete 10 MB/s è tooLAN Chiudi nella maggior parte degli aspetti. 1 MB/s fornirà un'esperienza di OK, sebbene vi siano alcune instabilità quando un utente scorre mentre vi sono immagini nella schermata di hello.

## <a name="flash-video-youtube"></a>Video Flash (YouTube)
100 MB/s LAN fornisce un'esperienza ottimale hello, mentre i 10 MB/s è accettabile (a indicare che è sincronizzato con frequenza dei fotogrammi hello, ma aumenta di variazione). Con 1 MB/s l'instabilità è molto elevata ed evidente.

## <a name="word-typing-word-remote-input"></a>Digitazione in Word (input remoto in Word)
Si tratta di uno scenario con un utilizzo ridotto della larghezza di banda. Con 256 KB/s l'esperienza ha la stessa qualità di quella offerta da una LAN.

## <a name="learn-more"></a>Altre informazioni
* [Uso previsto della larghezza di banda di rete di Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp - In che modo la larghezza di banda di rete influisce sulla qualità dell'esperienza?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp: scenari comuni di test relativi all'utilizzo della larghezza di banda di rete](remoteapp-bandwidthtests.md)

