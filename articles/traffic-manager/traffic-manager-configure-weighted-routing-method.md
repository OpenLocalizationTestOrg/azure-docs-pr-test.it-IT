---
title: metodo di routing tramite Azure Traffic Manager il traffico round robin ponderato aaaConfigure | Documenti Microsoft
description: Questo articolo viene illustrato come tooload bilanciare il traffico usando un metodo round robin in Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a>Configurazione metodo di routing del traffico hello ponderato in Traffic Manager

Un modello comune di metodo routing del traffico è tooprovide un set di endpoint identici, che includono servizi cloud e siti Web e inviare traffico tooeach in uno schema round-robin. Hello alla procedura seguente descrive come tooconfigure questo tipo di metodo di routing del traffico.

> [!NOTE]
> Siti Web di Azure offre già funzionalità di bilanciamento del carico round robin per i siti Web che si trovano all'interno di un data center (nota anche come area). Gestione traffico permette di toospecify metodo di routing del traffico round robin per siti Web in Data Center diversi.

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a>metodo di routing del traffico hello ponderato tooconfigure

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com). Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/). 
2. Nella barra di ricerca del portale hello, cercare hello **profili di gestione traffico** e quindi fare clic su nome del profilo hello desiderati come metodo di routing hello tooconfigure per.
3. In hello **profilo di gestione traffico** pannello, verificare che sia hello servizi cloud e siti Web che si desidera tooinclude nella configurazione sono presenti.
4. In hello **impostazioni** fare clic su **configurazione**e in hello **configurazione** pannello completo come segue:
    1. Per **impostazioni del metodo di routing del traffico**, verificare che sia di metodo di routing del traffico hello **Weighted**. In caso contrario, fare clic su **Weighted** dall'elenco a discesa hello.
    2. Set hello **le impostazioni di monitoraggio Endpoint** identici per tutti i ogni endpoint in questo profilo come indicato di seguito:
        1. Seleziona hello appropriato **protocollo**e specificare hello **porta** numero. 
        2. In **Percorso** immettere una barra */*. toomonitor endpoint, è necessario specificare un percorso e nome file. Barra "/" è una voce valida per il percorso relativo hello e implica che il file hello trovi nella directory radice di hello (impostazione predefinita).
        3. Nella parte superiore di hello della pagina hello, fare clic su **salvare**.
5. Testare le modifiche di hello nella configurazione, come indicato di seguito:
    1.  Nella barra di ricerca del portale hello, cercare il nome del profilo di Traffic Manager hello e scegliere il profilo di gestione traffico hello nei risultati di hello che hello visualizzato.
    2.  In hello **Traffic Manager** profilo pannello, fare clic su **Panoramica**.
    3.  Hello **profilo di gestione traffico** pannello viene visualizzato il nome DNS hello del profilo di Traffic Manager appena creato. È utilizzabile da qualsiasi endpoint destra di toohello tooget instradati ai client (ad esempio, passando tooit tramite un browser web) come determinato dal tipo di routing hello. In questo caso tutte le richieste vengono instradate a ogni endpoint secondo il metodo Round robin.
6. Dopo avere utilizza profilo di Traffic Manager, modificare il record DNS hello nel toopoint di server DNS autorevole il nome di dominio della società dominio nome toohello Traffic Manager.

![Configurare il metodo di routing del traffico Ponderato in Gestione traffico][1]

## <a name="next-steps"></a>Passaggi successivi

- Informazioni sul [metodo di routing del traffico Priorità](traffic-manager-configure-priority-routing-method.md).
- Informazioni sul [metodo di routing del traffico Prestazioni](traffic-manager-configure-performance-routing-method.md).
- Informazioni sul [metodo di routing Geografico](traffic-manager-configure-geographic-routing-method.md).
- Informazioni su come troppo[verificare le impostazioni di gestione traffico](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
