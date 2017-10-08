---
title: metodo di routing tramite Azure Traffic Manager il traffico prestazioni aaaConfigure | Documenti Microsoft
description: "Questo articolo viene illustrato come tooconfigure tooroute Traffic Manager il traffico toohello endpoint con latenza più bassa"
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a>Configurare il metodo di routing del traffico delle prestazioni di hello

Hello metodo di routing del traffico di prestazioni consente di toodirect traffico toohello endpoint con latenza più bassa di hello dalla rete hello del client. In genere, hello Data Center con latenza più bassa hello è hello più vicino nella distanza geografica. Questo metodo di routing del traffico non può basarsi per le modifiche in tempo reale sul carico o sulla configurazione di rete.

##  <a name="tooconfigure-performance-routing-method"></a>metodo di routing prestazioni tooconfigure

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com). Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/). 
2. Nella barra di ricerca del portale hello, cercare hello **profili di gestione traffico** e quindi fare clic su nome del profilo hello desiderati come metodo di routing hello tooconfigure per.
3. In hello **profilo di gestione traffico** pannello, verificare che sia hello servizi cloud e siti Web che si desidera tooinclude nella configurazione sono presenti.
4. In hello **impostazioni** fare clic su **configurazione**e in hello **configurazione** pannello completo come segue:
    1. Nelle **impostazioni del metodo di routing del traffico** per **Metodo di routing** selezionare **Prestazioni**.
    2. Set hello **le impostazioni di monitoraggio Endpoint** identici per tutti i ogni endpoint in questo profilo come indicato di seguito:
        1. Seleziona hello appropriato **protocollo**e specificare hello **porta** numero. 
        2. In **Percorso** immettere una barra */*. toomonitor endpoint, è necessario specificare un percorso e nome file. Barra "/" è una voce valida per il percorso relativo hello e implica che il file hello trovi nella directory radice di hello (impostazione predefinita).
        3. Nella parte superiore di hello della pagina hello, fare clic su **salvare**.
5.  Testare le modifiche di hello nella configurazione, come indicato di seguito:
    1.  Nella barra di ricerca del portale hello, cercare il nome del profilo di Traffic Manager hello e scegliere il profilo di gestione traffico hello nei risultati di hello che hello visualizzato.
    2.  In hello **Traffic Manager** profilo pannello, fare clic su **Panoramica**.
    3.  Hello **profilo di gestione traffico** pannello viene visualizzato il nome DNS hello del profilo di Traffic Manager appena creato. È utilizzabile da qualsiasi endpoint destra di toohello tooget instradati ai client (ad esempio, passando tooit tramite un browser web) come determinato dal tipo di routing hello. In questo caso tutte le richieste vengono indirizzato toohello endpoint con latenza più bassa di hello dalla rete hello del client.
6. Dopo avere utilizza profilo di Traffic Manager, modificare il record DNS hello nel toopoint di server DNS autorevole il nome di dominio della società dominio nome toohello Traffic Manager.

![Configurazione del metodo di routing del traffico delle prestazioni con Gestione traffico][1]

## <a name="next-steps"></a>Passaggi successivi

- Informazioni sul [metodo di routing del traffico Ponderato](traffic-manager-configure-weighted-routing-method.md).
- Informazioni sul [metodo di routing Priorità](traffic-manager-configure-priority-routing-method.md).
- Informazioni sul [metodo di routing Geografico](traffic-manager-configure-geographic-routing-method.md).
- Informazioni su come troppo[verificare le impostazioni di gestione traffico](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png