---
title: aaaOverview del bordo IoT di Azure | Documenti Microsoft
description: Viene descritto hello architetturale concetti chiave di Azure IoT Edge come gateway, i moduli e istanze di Service Broker.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Concetti dell'architettura di Azure IoT Edge

Prima di esaminare qualsiasi codice di esempio o creare proprio gateway di campo tramite IoT Edge, è necessario comprendere i concetti chiave hello che supportano l'architettura di hello del bordo IoT.

## <a name="iot-edge-modules"></a>Moduli di IoT Edge

Per compilare un gateway con Azure IoT Edge, è necessario creare e assemblare i *moduli di IoT Edge*. Utilizzano i moduli *messaggi* tooexchange dati tra loro. Un modulo riceve un messaggio, esegue un'azione su di esso, facoltativamente, li trasforma in un nuovo messaggio e pubblica quindi per tooprocess altri moduli. Alcuni moduli potrebbero produrre solo nuovi messaggi e non elaborare mai i messaggi in arrivo. Una catena di moduli crea una pipeline di elaborazione dei dati con ogni modulo eseguendo una trasformazione sui dati hello in un determinato punto nella pipeline.

![Catena di moduli nel gateway compilati con Azure IoT Edge][1]

Bordo IoT contiene hello seguenti componenti:

* Moduli già scritti che eseguono funzioni di gateway comuni.
* interfacce Hello un sviluppatore possono utilizzare moduli personalizzati toowrite.
* Hello infrastruttura necessarie toodeploy ed eseguire un set di moduli.

Hello SDK fornisce un livello di astrazione che consente di toobuild gateway toorun in vari sistemi operativi e piattaforme.

![Livello di astrazione di Azure IoT Edge][2]

## <a name="messages"></a>Messaggi

Sebbene pensa moduli passando tooeach altri messaggi è un modo pratico di tooconceptualize funzionamento di un gateway, non in modo accurato riflette cosa accade. I moduli di IoT Edge utilizzano un toocommunicate broker tra loro. I moduli pubblicano broker toohello messaggi (tramite modelli di messaggistica, ad esempio, bus o di pubblicazione/sottoscrizione) e quindi consentono hello broker route hello messaggio toohello moduli connesso tooit.

Un modulo Usa hello **Broker_Publish** funzione toopublish un broker toohello messaggi. broker di Hello recapita modulo tooa messaggi richiamando una funzione di callback. Un messaggio è costituito da un set di proprietà chiave/valore e contenuto passato come blocco di memoria.

![ruolo Hello di Service Broker in Azure IoT Edge hello][3]

## <a name="message-routing-and-filtering"></a>Routing e filtro dei messaggi

Esistono due modi toodirect messaggi toohello corretto IoT bordo i moduli:

* È possibile passare un set di collegamenti possono essere passati broker toohello in modo da Service broker hello hello origine e sink per ogni modulo.
* Un modulo è possibile filtrare per proprietà hello del messaggio hello.

Un modulo deve agire solo su un messaggio se il messaggio hello destinato. I collegamenti e il filtro dei messaggi creano una pipeline dei messaggi.

## <a name="next-steps"></a>Passaggi successivi

toosee questi concetti applicati in un esempio è possibile eseguire, vedere [architettura esplorare Azure IoT Edge][lnk-hello-world].

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md