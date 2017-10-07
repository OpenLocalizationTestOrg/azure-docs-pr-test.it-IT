---
title: domande frequenti su DNS aaaAzure | Documenti Microsoft
description: Domande frequenti su DNS di Azure
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Domande frequenti su DNS di Azure

## <a name="about-azure-dns"></a>DNS di Azure

### <a name="what-is-azure-dns"></a>Che cos'è DNS di Azure?

Hello Domain Name System o DNS, è responsabile della conversione (o nel risolvere) un sito Web o servizio name tooits indirizzo IP. DNS di Azure è un servizio di hosting per i domini DNS, che fornisce la risoluzione dei nomi usando l'infrastruttura di Microsoft Azure. Ospitando i domini in Azure, è possibile gestire il servizio DNS i record mediante hello credenziali, API, strumenti e fatturazione come altri servizi di Azure.

I domini DNS nel servizio DNS di Azure sono ospitati nella rete globale di Azure dei server dei nomi DNS. Utilizziamo Anycast di rete in modo che ogni query DNS è stata risposta dal server DNS disponibile più vicino di hello. Ciò consente di accelerare le prestazioni e ottenere la disponibilità elevata per il dominio.

Hello servizio DNS di Azure si basa su Gestione risorse di Azure. Usufruisce quindi delle funzionalità di Resource Manager, come il controllo degli accessi in base al ruolo, i log di controllo e il blocco delle risorse. I domini e i record possono essere gestiti tramite hello portale di Azure, i cmdlet di Azure PowerShell e hello multipiattaforma CLI di Azure. Le applicazioni che richiedono la gestione automatica di DNS è possono integrare con il servizio di hello tramite hello SDK e API REST.

### <a name="how-much-does-azure-dns-cost"></a>Quanto costa DNS di Azure?

modello di fatturazione di Hello DNS di Azure si basa sul numero di hello delle zone DNS ospitate nel servizio DNS di Azure e il numero di hello di query DNS che ricevono. In base all'uso sono disponibili sconti.

Per ulteriori informazioni, vedere hello [DNS di Azure pagina dei prezzi](https://azure.microsoft.com/pricing/details/dns/).

### <a name="what-is-hello-sla-for-azure-dns"></a>Che cos'è hello contratto di servizio per il DNS di Azure?

È garantito che le richieste DNS valide riceverà una risposta da almeno un server dei nomi DNS di Azure almeno 99,99% di tempo hello.

Per ulteriori informazioni, vedere hello [pagina Contratto di servizio di Azure DNS](https://azure.microsoft.com/support/legal/sla/dns).

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>Che cos'è una "zona DNS"? È hello stesso come un dominio DNS? 

Un dominio è un nome univoco nel sistema di nome di dominio hello, ad esempio 'contoso.com'.

Una zona DNS è utilizzato toohost hello DNS record per un particolare dominio. Ad esempio, hello dominio 'contoso.com' può contenere più record DNS, ad esempio 'mail.contoso.com' (per un server di posta elettronica) e 'www.contoso.com' (per un sito web). Questi verrebbe ospitati nella zona DNS hello 'contoso.com'.

È un nome di dominio *solo un nome*, mentre una zona DNS è una risorsa di dati contenente i record DNS di hello per un nome di dominio. DNS di Azure consente una zona DNS toohost e gestire i record DNS hello per un dominio in Azure. Fornisce inoltre le query DNS tooanswer da hello Internet Server dei nomi DNS.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>È necessario toopurchase un toouse di nome di dominio DNS DNS di Azure? 

Non necessariamente.

Non è necessario toopurchase toohost un dominio una zona DNS di DNS di Azure. È possibile creare una zona DNS in qualsiasi momento senza il nome di dominio hello proprietario. Query DNS per questa zona verrà risolto solo se vengono indirizzati i server dei nomi DNS di Azure toohello assegnato toohello zona.

Nome di dominio toopurchase hello è necessario se si desidera toolink la zona DNS in gerarchia DNS globale hello – in questo modo, le query da un punto qualsiasi in hello world toofind la zona DNS di DNS e restituita una risposta con i record DNS.

## <a name="azure-dns-features"></a>Funzionalità DNS di Azure

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>DNS di Azure supporta il routing del traffico basato su DNS o il failover dell'endpoint?

Il failover dell'endpoint e il routing del traffico basato su DNS vengono garantiti da Gestione traffico di Azure. Si tratta di un servizio di Azure separato che può essere usato insieme a DNS di Azure. Per ulteriori informazioni, vedere hello [Panoramica di gestione traffico](../traffic-manager/traffic-manager-overview.md).

DNS di Azure supporta solo l'hosting 'statici' domini DNS, in cui ogni query DNS per un determinato record DNS riceve sempre hello stessa risposta DNS.

### <a name="does-azure-dns-support-domain-name-registration"></a>DNS di Azure supporta la registrazione del nome di dominio?

No. DNS di Azure attualmente non supporta l'acquisto dei nomi di dominio. Se si desidera toopurchase domini, è necessario toouse un registrar di nomi di dominio di terze parti. registrar Hello in genere una tariffa small annuale. domini Hello possono quindi essere ospitati in DNS di Azure per la gestione dei record DNS. Vedere [tooAzure un dominio DNS delegato](dns-domain-delegation.md) per informazioni dettagliate.

Questa è una funzionalità che Microsoft sta verificando nel backlog. È possibile utilizzare anche il sito di commenti e suggerimenti[registrare il supporto per questa funzionalità](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).

### <a name="does-azure-dns-support-private-domains"></a>DNS di Azure supporta domini "privati"?

No. DNS di Azure attualmente supporta solo i domini con connessione Internet.

Questa è una funzionalità che Microsoft sta verificando nel backlog. È possibile utilizzare anche il sito di commenti e suggerimenti[registrare il supporto per questa funzionalità](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).

Per informazioni sulle opzioni DNS interne in Azure, vedere [Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

### <a name="does-azure-dns-support-dnssec"></a>DNS di Azure supporta DNSSEC?

No. DNS di Azure attualmente non supporta DNSSEC.

Questa è una funzionalità che Microsoft sta verificando nel backlog. È possibile utilizzare anche il sito di commenti e suggerimenti[registrare il supporto per questa funzionalità](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>DNS di Azure supporta i trasferimenti di zona (AXFR/IXFR)?

No. DNS di Azure attualmente non supporta i trasferimenti di zona. Zone DNS possono essere [importati in DNS di Azure mediante Azure CLI hello](dns-import-export.md). I record DNS possono quindi essere gestiti tramite hello [il portale di gestione di DNS di Azure](dns-operations-recordsets-portal.md), nostro [API REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [i cmdlet di PowerShell](dns-operations-recordsets.md), o [ Strumento CLI](dns-operations-recordsets-cli.md).

Questa è una funzionalità che Microsoft sta verificando nel backlog. È possibile utilizzare anche il sito di commenti e suggerimenti[registrare il supporto per questa funzionalità](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).

### <a name="does-azure-dns-support-url-redirects"></a>DNS di Azure supporta i reindirizzamenti URL?

No. Servizi di reindirizzamento URL non sono effettivamente un servizio DNS - funzionano a livello HTTP hello, anziché a livello DNS hello. Alcuni provider DNS è toobundle un servizio di reindirizzamento URL come parte della loro offerta complessiva. Questo servizio non è attualmente supportato da DNS di Azure.

Questa funzionalità viene rilevata nel backlog. È possibile utilizzare anche il sito di commenti e suggerimenti[registrare il supporto per questa funzionalità](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).

## <a name="using-azure-dns"></a>Uso di DNS di Azure

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>È possibile ospitare un dominio usando DNS di Azure e un altro provider DNS?

Sì. DNS di Azure supporta i domini di hosting condiviso con altri servizi DNS.

toodo in tal caso, è necessario record NS hello toomodify per dominio hello (quale controllare quali provider ricevono DNS esegue una query per il dominio hello) toopoint toohello server dei nomi di entrambi i provider. Questi record NS necessario toobe modificato in 3 posizioni: nel sistema DNS di Azure, in altri provider, hello e nella zona padre hello (in genere configurate tramite nome di dominio di hello). Per altre informazioni sulla delega DNS, vedere [Delega del dominio DNS](dns-domain-delegation.md).

Inoltre, è necessario che i record DNS hello hello dominio sono sincronizzati tra entrambi i provider DNS tooensure. DNS di Azure attualmente non supporta i trasferimenti di zona DNS. È necessario record DNS toosynchronize utilizzando entrambi hello [il portale di gestione di DNS di Azure](dns-operations-recordsets-portal.md), il [API REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [i cmdlet di PowerShell](dns-operations-recordsets.md) , o [strumento CLI](dns-operations-recordsets-cli.md).

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>È necessario toodelegate il server dei nomi di dominio tooall 4 DNS di Azure?

Sì. DNS di Azure assegna 4 server dei nomi di zona DNS tooeach, per l'isolamento degli errori e una maggiore flessibilità. tooqualify per hello contratto di servizio DNS di Azure, è necessario toodelegate il server dei nomi di dominio tooall 4.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>Quali sono i limiti di utilizzo di hello per DNS di Azure?

Quando si utilizza il DNS di Azure, si applica Hello limiti predefiniti seguenti:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>È possibile spostare una zona DNS di Azure tra gruppi di risorse o tra sottoscrizioni?

Sì. Le zone DNS possono essere spostate tra gruppi di risorse o tra sottoscrizioni.

Lo spostamento di una zona DNS non influenza le query DNS. Server dei nomi Hello assegnato zona toohello rimangono hello che stesso e le query DNS vengono elaborati normalmente in tutto.

Per ulteriori informazioni e istruzioni su come toomove zone DNS, vedere [spostare le risorse tooa nuovo gruppo di risorse o sottoscrizione](../azure-resource-manager/resource-group-move-resources.md).

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>Quanto tempo occorre per effetto di tootake modifiche DNS?

Nuove zone DNS e i record DNS vengono in genere riportati sul server dei nomi DNS di Azure hello rapidamente, entro pochi secondi.

Modifica tooexisting i record DNS possono richiedere più tempo, ma devono comunque essere riflessi nel server dei nomi DNS di Azure hello entro 60 secondi. In questo caso, la cache DNS di fuori di DNS di Azure (per i client DNS e ai resolver ricorsivo DNS) possono incidere sulle hello tempo per un toobe modifica DNS effettivo. La durata della cache può essere controllata utilizzando proprietà Time-To-Live (TTL) di hello di ogni set di record.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>Come proteggere le zone DNS da eliminazioni accidentali?

DNS di Azure viene gestita mediante Gestione risorse di Azure e le funzionalità di controllo di accesso trae vantaggio da hello che Gestione risorse di Azure fornisce. Controllo di accesso basato sui ruoli può essere utilizzato toocontrol gli utenti che hanno accesso in lettura o scrittura zone tooDNS e set di record. Blocchi di risorse possono essere applicato tooprevent accidentale modifica o l'eliminazione di set di record e zone DNS.

Per altre informazioni, vedere [Protezione delle zone e dei record DNS](dns-protect-zones-recordsets.md).

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>Come configurare i record SPF in DNS di Azure?

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>Come configurare un nome di dominio internazionale, IDN, in DNS di Azure?

I nomi di dominio internazionali, IDN, usano la codifica per ogni nome DNS con "[punycode](https://en.wikipedia.org/wiki/Punycode)". Le query DNS vengono create usando i nomi con codifica punycode.

È possibile configurare International Domain Names (IDN) in DNS di Azure dal nome della zona hello conversione prima o toopunycode nome set di record. DNS di Azure non supporta attualmente la conversione incorporata da e verso punycode.

## <a name="next-steps"></a>Passaggi successivi

[Altre informazioni su DNS di Azure](dns-overview.md)
<br>
[Altre informazioni su zone e record DNS](dns-zones-records.md)
<br>
[Introduzione a DNS di Azure](dns-getstarted-portal.md)

