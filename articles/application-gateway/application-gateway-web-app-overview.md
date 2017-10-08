---
title: aaaOverview di multi-tenant back termina con Gateway applicazione Azure | Documenti Microsoft
description: Questa pagina fornisce una panoramica del supporto di Gateway applicazione hello per multi-tenant back-end.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>Supporto del gateway applicazione per i back-end multi-tenant

Il gateway applicazione di Azure supporta set di scalabilità di macchine virtuali, interfacce di rete, indirizzi IP pubblici/privati o il nome di dominio completo (FQDN) come parte dei propri pool back-end. Per impostazione predefinita, il gateway applicazione non modifica intestazione host HTTP in ingresso di hello da client hello e invia hello back-end di intestazione toohello inalterato. Esistono molti servizi come [App Web di Azure](../app-service-web/app-service-web-overview.md) e [gestione API](../api-management/api-management-key-concepts.md) che sono di natura multi-tenant e si basano su un'intestazione host specifico o l'endpoint corretto toohello tooresolve estensione SNI. Gateway applicazione supporta ora il possibilità hello per gli utenti toooverwrite hello in arrivo intestazione host HTTP in base alle impostazioni di back-end HTTP di hello. Questa funzionalità garantisce il supporto di App Web di Azure e Gestione API come back-end multi-tenant Questa funzionalità è disponibile per hello standard e WAF SKU. Multi-tenant back end supporto anche funziona con terminazione e fine tooend SSL scenari SSL.

![Scenario con app Web](./media/application-gateway-web-app-overview/scenario.png)

le impostazioni HTTP di hello Hello possibilità toospecify sono definite in un host e può essere applicato tooany nuovamente terminare pool durante la creazione di regole. Multi-tenant nuovamente termina hello di supporto seguenti due metodi di override estensione SNI e intestazione host.

1. valore in hello Hello possibilità tooset hello host nome tooa fisso impostazioni HTTP. Questa funzionalità garantisce viene eseguito l'override di tale intestazione host hello toothis valore per tutti i pool di back-end toohello il traffico in cui sono applicate impostazioni hello HTTP. Quando si utilizza tooend fine SSL, viene utilizzato questo nome host sottoposto a override in hello estensione SNI. Questa funzionalità consente scenari in cui una farm di pool back-end prevede un'intestazione host diverso dall'intestazione dell'host hello in arrivo cliente.

2. nome di host hello per tooderive di possibilità Hello da hello IP o FQDN di membri del pool back-end hello. Le impostazioni HTTP forniscono anche un nome di opzione toopick hello host di nome di dominio completo del membro di un pool back-end se è configurato con hello opzione tooderive il nome host da un membro del pool back-end singolo. Quando si utilizza tooend fine SSL, questo nome host è derivato da hello FQDN e viene utilizzato per estensioni SNI hello. Questa funzionalità consente scenari in cui un pool di back-end può avere due o più servizi PaaS multi-tenant come App web di Azure e membro di tooeach intestazione host della richiesta di hello contiene il nome di host hello derivato dal relativo nome di dominio completo.

> [!NOTE]
> In entrambi hello precedente casi le impostazioni di hello interessano solo il comportamento di traffico in tempo reale hello e non hello integrità probe il comportamento. Custom le ricerche già supporto hello possibilità toospecify un'intestazione host nella configurazione di probe hello. Probe personalizzati supportano ora anche hello possibilità tooderive hello host intestazione comportamento dalle impostazioni HTTP hello attualmente configurato. Questa configurazione può essere specificata tramite hello `PickHostNameFromback endAddress` parametro nella configurazione del probe hello. Per end tooend funzionalità toowork, sia probe hello e le impostazioni HTTP hello devono essere corretta configurazione di hello tooreflect modificato.

Con questa funzionalità, i clienti specificare opzioni hello nelle impostazioni HTTP hello e personalizzate probe toohello di configurazione appropriato. Questa impostazione viene quindi associata tooa listener e un back end pool tramite una regola.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooset di un gateway applicazione con un'applicazione web come un back end membro del pool, visitare il sito: [configurare App del servizio web App con Gateway applicazione](application-gateway-web-app-powershell.md)
