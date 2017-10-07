---
title: aaaIntroduction tooAzure Watcher di rete | Documenti Microsoft
description: Questa pagina viene fornita una panoramica di hello servizio Watcher di rete per il monitoraggio e la visualizzazione rete connesso alle risorse in Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Panoramica del monitoraggio della rete in Azure

Per creare una rete end-to-end in Azure è possibile orchestrare e comporre varie risorse di rete individuali, quali rete virtuale, ExpressRoute, gateway applicazione, servizi di bilanciamento del carico e altro ancora. Il monitoraggio è disponibile in ogni hello risorse di rete. Facciamo riferimento toothis monitoraggio come monitoraggio a livello di risorse.

rete di Hello end tooend può avere configurazioni complesse e le interazioni tra le risorse, creazione di scenari complessi che richiedono basata sullo scenario di monitoraggio tramite Watcher di rete.

Questo articolo illustra il monitoraggio a livello di risorsa e di scenario. Il monitoraggio della rete in Azure comprende due categorie generali:

* [**Controllo di rete** ](#network-watcher) -basata sullo Scenario di monitoraggio viene fornito con funzionalità di hello Watcher di rete. Il servizio include l'acquisizione pacchetti, l'hop successivo, la verifica del flusso IP, la visualizzazione dei gruppi di sicurezza e i registri dei flussi dei gruppi di sicurezza di rete. Monitoraggio a livello di scenario è inclusa una visualizzazione di tooend finale delle risorse di rete in Monitoraggio risorse di rete di contrasto tooindividual.
* [**Monitoraggio delle risorse**](#network-resource-level-monitoring): il monitoraggio a livello di risorsa include funzionalità di log di diagnostica, metriche, risoluzione dei problemi e integrità delle risorse. Tutte queste funzionalità vengono compilate a livello di risorse di rete hello.

## <a name="network-watcher"></a>Network Watcher

Watcher di rete è un servizio internazionale che consente di toomonitor e diagnosticare le condizioni di livello rete scenario, a e da Azure. Diagnostica di rete e gli strumenti di visualizzazione disponibili con Watcher di rete consentono di comprendere, diagnosticare e ottenere rete tooyour insights in Azure.

Watcher di rete presenta attualmente hello seguenti funzionalità:

* **[Topologia](network-watcher-topology-overview.md)**  -fornisce un hello con visualizzazione a livello di rete diversi interconnessioni e le associazioni tra le risorse di rete in un gruppo di risorse.
* **[Acquisizione pacchetti variabile](network-watcher-packet-capture-overview.md)**: acquisisce i dati dei pacchetti all'interno e all'esterno di una macchina virtuale. Filtri di opzioni e ottimizzare i controlli, ad esempio si trova ora in grado di tooset avanzati e versatilità di fornire i limiti delle dimensioni. Hello pacchetto possono essere archiviati in un archivio blob o su disco locale di hello in formato CAP.
* **[Verifica flusso IP](network-watcher-ip-flow-verify-overview.md)**: controlla se un pacchetto viene accettato o rifiutato in base ai parametri di pacchetto costituiti da informazioni a 5 tuple sul flusso, ovvero l'indirizzo IP di destinazione, l'indirizzo IP di origine, la porta di destinazione, la porta di origine e il protocollo. Se i pacchetti hello viene negato da un gruppo di sicurezza, hello regola e gruppo di pacchetti hello negato.
* **[Hop successivo](network-watcher-next-hop-overview.md)**  -determina hello hop successivo per i pacchetti hello infrastruttura di rete di Azure, consentendo di route definite dall'utente non è configurato correttamente qualsiasi toodiagnose indirizzato.
* **[Visualizzazione del gruppo di sicurezza](network-watcher-security-group-view-overview.md)**  -Ottiene le regole di sicurezza efficace e applicato hello che vengono applicate in una macchina virtuale.
* **[Registrazione NSG flusso](network-watcher-nsg-flow-logging-overview.md)**  -flusso di log per i gruppi di sicurezza di rete consentono di toocapture registri tootraffic correlati che vengono concesse o negate le regole di sicurezza hello gruppo hello. flusso di Hello è definito dalle informazioni tupla con 5: indirizzo IP di origine, IP di destinazione, porta di origine, destinazione porta e protocollo.
* **[Gateway di rete virtuale e la risoluzione dei problemi di connessione](network-watcher-troubleshoot-manage-rest.md)**  -fornisce hello possibilità tootroubleshoot gateway di rete virtuale e le connessioni.
* **[Limiti della sottoscrizione di rete](#network-subscription-limits)**  -consente l'utilizzo delle risorse di rete tooview rispetto ai limiti.
* **[Configurazione del Log di diagnostica](#diagnostic-logs)**  : fornisce un unico riquadro tooenable o disabilitare i log di diagnostica per le risorse di rete in un gruppo di risorse.
* **[Connettività (anteprima)](network-watcher-connectivity-overview.md)**  -verifica il possibilità di hello di stabilire una connessione TCP diretta da una macchina virtuale di tooa dato endpoint.

### <a name="role-based-access-control-rbac-in-network-watcher"></a>Controllo degli accessi in base al ruolo in Network Watcher

Watcher di rete utilizza hello [modello di controllo di accesso gestire (RBAC)](../active-directory/role-based-access-control-what-is.md). Hello queste autorizzazioni è necessarie hello Watcher di rete. È importante toomake che tale ruolo hello utilizzato per avviare le API di controllo di rete o l'utilizzo Watcher di rete dal portale hello disponga dell'accesso hello necessario.

|Risorsa| Autorizzazione|
|---|---| 
|Microsoft.Storage/ |Lettura|
|Microsoft.Authorization/| Lettura| 
|Microsoft.Resources/subscriptions/resourceGroups/| Lettura|
|Microsoft.Storage/storageAccounts/listServiceSas/ | Azione|
|Microsoft.Storage/storageAccounts/listAccountSas/ |Azione|
|Microsoft.Storage/storageAccounts/listKeys/ | Azione|
|Microsoft.Compute/virtualMachines/ |Lettura|
|Microsoft.Compute/virtualMachines/ |Scrittura|
|Microsoft.Compute/virtualMachineScaleSets/ |Lettura|
|Microsoft.Compute/virtualMachineScaleSets/ |Scrittura|
|Microsoft.Network/networkWatchers/packetCaptures/ |Lettura|
|Microsoft.Network/networkWatchers/packetCaptures/| Scrittura|
|Microsoft.Network/networkWatchers/packetCaptures/| Elimina|
|Microsoft.Network/networkWatchers/ |Scrittura |
|Microsoft.Network/networkWatchers/| Lettura |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>Limite sottoscrizioni di rete

Limiti della sottoscrizione rete forniscono i dettagli di utilizzo di hello di ogni risorsa di rete hello in una sottoscrizione in un'area con il numero massimo di hello delle risorse disponibili.

![Limite sottoscrizioni di rete][nsl]

## <a name="network-resource-level-monitoring"></a>Monitoraggio a livello di risorsa di rete

Hello seguenti caratteristiche sono disponibile per il monitoraggio a livello di risorse:

### <a name="audit-log"></a>Log di controllo

Vengono registrate le operazioni eseguite come parte della configurazione di hello delle reti. Questi registri possono essere visualizzati nel portale di Azure hello o recuperati utilizzando strumenti quali Power BI o gli strumenti di terze parti. I log di controllo sono disponibili tramite il portale di hello, PowerShell, CLI e API Rest. Per altre informazioni sui log di controllo, vedere l'articolo relativo alle [operazioni di controllo con Resource Manager](../resource-group-audit.md).

I log di controllo sono disponibili per le operazioni eseguite su tutte le risorse di rete.

### <a name="metrics"></a>Metrica

Le metriche sono costituite da contatori e misurazioni delle prestazioni raccolti in un determinato periodo di tempo. Attualmente le metriche sono disponibili per il gateway applicazione. Metrica può essere utilizzato tootrigger avvisi in base alla soglia. Vedere [diagnostica del Gateway applicazione](../application-gateway/application-gateway-diagnostics.md) tooview come metrica può essere utilizzato toocreate avvisi.

![Visualizzazione metriche][metrics]

### <a name="diagnostic-logs"></a>Log di diagnostica

Eventi periodici e spontanei vengono creati dalle risorse di rete e registrati negli account di archiviazione, inviate tooan Hub eventi o Analitica di Log. Questi log forniscono informazioni dettagliate sui integrità hello di una risorsa. e possono essere visualizzati con strumenti quali Power BI e Log Analytics. come i log di diagnostica tooview, visitare toolearn [Analitica Log](../log-analytics/log-analytics-azure-networking-analytics.md).

Sono disponibili log di diagnostica per il [servizio di bilanciamento del carico](../load-balancer/load-balancer-monitor-log.md), i [gruppi di sicurezza di rete](../virtual-network/virtual-network-nsg-manage-log.md), le route e il [gateway applicazione](../application-gateway/application-gateway-diagnostics.md).

Network Watcher offre una visualizzazione dei log di diagnostica contenente tutte le risorse di rete che supportano la registrazione diagnostica. Da questa visualizzazione è possibile abilitare e disabilitare le risorse di rete in modo facile e veloce.

![logs][logs]

### <a name="troubleshooting"></a>Risoluzione dei problemi

risoluzione dei problemi di un'esperienza nel portale di hello pannello Hello viene fornito sulle risorse di rete oggi toodiagnose problemi comuni associati a una singola risorsa. Questa esperienza è disponibile per hello seguenti risorse di rete - ExpressRoute, Gateway VPN, Gateway applicazione, i log di sicurezza di rete, route, DNS, bilanciamento del carico e gestione traffico. toolearn più sulla risorsa livello risoluzione dei problemi, visitare [diagnosticare e risolvere problemi di risoluzione dei problemi di Azure](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![Informazioni sulla risoluzione dei problemi][TS]

### <a name="resource-health"></a>Integrità delle risorse

integrità Hello di una risorsa di rete viene fornito con cadenza periodica. Le risorse includono il gateway VPN e il tunnel VPN. Integrità delle risorse è accessibile in hello portale di Azure. toolearn più sull'integrità delle risorse, visitare [Panoramica integrità delle risorse](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>Passaggi successivi

Ora che si conosce Network Watcher è possibile imparare a:

Eseguire un'acquisizione pacchetto sulla macchina virtuale, visitare il sito [acquisizione pacchetto variabile in hello portale di Azure](network-watcher-packet-capture-manage-portal.md)

Eseguire il monitoraggio attivo e la diagnostica usando l'[acquisizione pacchetti attivata da avvisi](network-watcher-alert-triggered-packet-capture.md).

Rilevare vulnerabilità della sicurezza con l'[analisi dell'acquisizione pacchetti tramite Wireshark](network-watcher-deep-packet-inspection.md), usando strumenti open source.

Informazioni su alcune delle hello altre chiavi [funzionalità di rete](../networking/networking-overview.md) di Azure.

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











