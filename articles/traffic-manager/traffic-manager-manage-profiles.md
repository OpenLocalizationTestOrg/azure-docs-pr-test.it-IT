---
title: i profili di Traffic Manager di Azure aaaManage | Documenti Microsoft
description: Questo articolo illustra come creare, disabilitare, abilitare ed eliminare un profilo di Gestione traffico di Azure.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Gestire un profilo di Gestione traffico di Azure

Profili di gestione traffico utilizzano routing del traffico distribuzione hello toocontrol metodi di servizi cloud di traffico tooyour o gli endpoint del sito Web. Questo articolo viene illustrato come toocreate e gestire i profili.

## <a name="create-a-traffic-manager-profile"></a>Creare un profilo di Gestione traffico

È possibile creare un profilo di gestione traffico mediante hello portale di Azure. Dopo la creazione del profilo, è possibile configurare gli endpoint, monitoraggio e altre impostazioni in hello portale di Azure. Gestione traffico supporta too200 degli endpoint per il profilo. Tuttavia, la maggior parte degli scenari di utilizzo richiede solo un numero ridotto di endpoint.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate un profilo di Traffic Manager

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com). Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/). 
2. In hello **Hub** menu, fare clic su **New** > **rete** > **vedere tutti**, fare clic su **traffico Gestione** hello tooopen profilo **profilo di Traffic Manager creare** pannello, quindi fare clic su **crea**.
3. In hello **profilo di Traffic Manager creare** pannello completo come segue:
    1. In **Nome** specificare un nome per il profilo. Questo nome deve toobe univoco all'interno di zona trafficmanager.net hello e restituisce il nome DNS hello <name>, trafficmanager.net, che viene utilizzato tooaccess profilo di Traffic Manager.
    2. In **il metodo di Routing**selezionare hello **priorità** metodo di routing.
    3. In **sottoscrizione**, selezionare la sottoscrizione di hello desiderato toocreate questo profilo
    4. In **gruppo di risorse**, creare un nuovo tooplace gruppo di risorse di questo profilo.
    5. In **percorso del gruppo di risorse**, selezionare il percorso di hello hello del gruppo di risorse. Questa impostazione fa riferimento il percorso toohello hello del gruppo di risorse e non ha alcun impatto su hello profilo di Traffic Manager che verrà distribuito a livello globale.
    6. Fare clic su **Crea**.
    7. Una volta completata la distribuzione globale di hello del profilo di Traffic Manager, è elencato nel gruppo di risorse corrispondente come una delle risorse di hello.

## <a name="disable-enable-or-delete-a-profile"></a>Disabilitare, abilitare o eliminare un profilo

È possibile disabilitare un profilo esistente in modo che Traffic Manager non fa riferimento endpoint toohello configurato di richieste utente. Quando si disabilita un profilo di Traffic Manager, profilo hello e hello contenute nel profilo hello rimangono invariate e modificabili nell'interfaccia di Traffic Manager hello.  I riferimenti riprendere quando si riabilita profilo hello. Quando si crea un profilo di gestione traffico nel portale di Azure hello, viene abilitata automaticamente. Se si decide che un profilo non sarà più necessario, è possibile eliminarlo.

### <a name="toodisable-a-profile"></a>toodisable un profilo

1. Se si utilizza un nome di dominio personalizzato, modificare il record CNAME hello del server DNS Internet in modo che non punta più tooyour profilo di gestione traffico.
2. Arrestare il traffico è indirizzato toohello endpoint tramite impostazioni profilo di Traffic Manager hello.
3. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com).
2. Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome che si desidera toomodify e quindi scegliere il profilo di gestione traffico hello in hello risultati che hello visualizzato.
3. In hello **profilo di gestione traffico** pannello, fare clic su **Panoramica**, nel pannello della panoramica hello fare clic su **disabilitare**, quindi confermare il profilo di gestione traffico di toodisable hello.

### <a name="tooenable-a-profile"></a>tooenable un profilo

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com).
2. Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome che si desidera toomodify e quindi scegliere il profilo di gestione traffico hello in hello risultati che hello visualizzato.
3. In hello **profilo di gestione traffico** pannello, fare clic su **Panoramica**e quindi, nel pannello della panoramica hello fare clic su **abilitare**.
5. Se si utilizza un nome di dominio personalizzato, creare un record di risorse CNAME al nome di dominio DNS Internet server toopoint toohello del profilo di Traffic Manager.
6. Il traffico è indirizzato toohello endpoint nuovamente.

### <a name="toodelete-a-profile"></a>toodelete un profilo

1. Verificare che i record di risorse DNS hello del server DNS Internet non utilizza non è più un record di risorse CNAME che punta il nome di dominio toohello del profilo di Traffic Manager.
2. Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome che si desidera toomodify e quindi scegliere il profilo di gestione traffico hello in hello risultati che hello visualizzato.
3. In hello **profilo di gestione traffico** pannello, fare clic su **Panoramica**, nel pannello della panoramica hello fare clic su **eliminare**, quindi confermare il profilo di gestione traffico di toodelete hello.

## <a name="next-steps"></a>Passaggi successivi

* [Aggiungere un endpoint](traffic-manager-endpoints.md)
* [Configurare il metodo di routing Priorità](traffic-manager-configure-priority-routing-method.md)
* [Configurare il metodo di routing Geografico](traffic-manager-configure-geographic-routing-method.md) 
* [Configurare il metodo di routing Ponderato](traffic-manager-configure-weighted-routing-method.md)
* [Configurare il metodo di routing Prestazioni](traffic-manager-configure-performance-routing-method.md)
