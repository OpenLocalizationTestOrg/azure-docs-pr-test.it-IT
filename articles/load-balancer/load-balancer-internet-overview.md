---
title: aaaInternet affiancate Panoramica del servizio di bilanciamento del carico | Documenti Microsoft
description: "Panoramica del bilanciamento del carico Internet e delle relative funzionalità. Modalità di funzionamento del bilanciamento del carico per Azure con macchine virtuali e servizi cloud."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a>Panoramica del bilanciamento del carico Internet

Servizio di bilanciamento del carico di Azure esegue il mapping hello pubblica IP indirizzo numero di porta e in ingresso traffico toohello privato IP indirizzo e numero di porta della macchina virtuale hello e viceversa per il traffico di risposta hello dalla macchina virtuale hello. Regole di bilanciamento del carico consentono di toodistribute specifici tipi di traffico tra più macchine virtuali o servizi. Ad esempio, è possibile distribuire il carico di hello del traffico di richiesta web in più server web o ruoli web.

Per un servizio cloud contenente istanze di ruoli web o ruoli di lavoro, è possibile definire un endpoint pubblico nel file di definizione (con estensione csdef) servizio hello.

Hello *servicedefinition* file contiene la configurazione di endpoint hello e quando si dispone di più istanze del ruolo per una distribuzione di ruolo web o di lavoro, bilanciamento del carico hello verrà configurato appositamente. distribuzione del cloud tooyour Hello modo tooadd istanze è Modifica numero di istanze di hello nel file di configurazione del servizio hello (con estensione csfg).

Hello figura riportata di seguito viene illustrato un endpoint con bilanciamento del carico per il traffico web che viene condiviso tra tre macchine virtuali per hello porta pubblica e privata TCP 80. Queste tre macchine virtuali appartengono a un set con carico bilanciato.

![esempio di bilanciamento del carico pubblico](./media/load-balancer-internet-overview/IC727496.png)

Figura 1. Endpoint con bilanciamento del carico per il traffico Web

Quando i client Internet inviano richieste di pagine web toohello indirizzo IP pubblico del servizio cloud hello sulla porta TCP 80, hello bilanciamento del carico di Azure distribuisce le richieste di hello tra hello tre macchine virtuali nel set di bilanciamento del carico hello. Per ulteriori informazioni sugli algoritmi di bilanciamento di carico, vedere hello [pagina Panoramica di bilanciamento carico](load-balancer-overview.md#load-balancer-features).

Per impostazione predefinita, Azure Load Balancer distribuisce il traffico di rete in modo uniforme tra più istanze di macchine virtuali. È inoltre possibile configurare l'affinità di sessione. Per altre informazioni, vedere l'articolo [Modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md).

## <a name="next-steps"></a>Passaggi successivi

Informazioni su [bilanciamento del carico interno](load-balancer-internal-overview.md) toobetter capire quale servizio di bilanciamento del carico è una soluzione migliore per la distribuzione cloud.

È anche possibile [iniziare a creare un bilanciamento del carico con connessione Internet](load-balancer-get-started-internet-arm-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento specifico del traffico di rete per il bilanciamento del carico.

Se l'applicazione deve tookeep connessioni attive per i server di bilanciamento del carico, è possibile comprendere più su [impostazioni di timeout TCP per un servizio di bilanciamento del carico di inattività](load-balancer-tcp-idle-timeout.md). Quando si utilizza Bilanciamento carico di Azure, questo risulterà utile toolearn sul comportamento di connessione inattiva.
