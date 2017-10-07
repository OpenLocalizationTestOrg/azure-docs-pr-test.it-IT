---
title: aaaDNS zone e record Panoramica - DNS di Azure | Documenti Microsoft
description: Panoramica del supporto per l'hosting di zone e record DNS in DNS di Microsoft Azure.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>Panoramica delle zone e dei record DNS

Questa pagina illustra i concetti chiave di hello di domini, zone DNS e i record DNS e set di record e in che modo sono supportati nel sistema DNS di Azure.

## <a name="domain-names"></a>Nomi di dominio

Hello Domain Name System è una gerarchia di domini. gerarchia di Hello inizia dal dominio 'root' hello, il cui nome è semplicemente '**.**'.  seguito dai domini di primo livello, come "com", "net", "org", "uk" o "jp",  e quindi dai domini di secondo livello, come "org.uk" o "co.jp" domini Hello nella gerarchia di hello DNS vengono distribuiti a livello globale, ospitati da server dei nomi DNS in tutto il mondo hello.

Un nome di dominio è un'organizzazione che consente un nome di dominio, ad esempio 'contoso.com' toopurchase.  Acquisto di un dominio offre nome si hello toocontrol destra hello gerarchia DNS con questo nome, consentendo ad esempio il sito web aziendale di toodirect nome hello 'www.contoso.com' tooyour. registrar Hello può ospitare hello dominio nel proprio server dei nomi per conto dell'utente o consentono di server dei nomi alternativi toospecify.

DNS di Azure fornisce un'infrastruttura di server di nome distribuita a livello globale, a disponibilità elevata, è possibile usare toohost il dominio. Ospitando i domini di DNS di Azure, è possibile gestire i record DNS con hello credenziali, API, strumenti, fatturazione e supporto di altri servizi di Azure.

DNS di Azure attualmente non supporta l'acquisto dei nomi di dominio. Se si desidera toopurchase un nome di dominio, è necessario toouse un registrar di nomi di dominio di terze parti. registrar Hello in genere una tariffa small annuale. domini Hello possono quindi essere ospitati in DNS di Azure per la gestione dei record DNS. Vedere [tooAzure un dominio DNS delegato](dns-domain-delegation.md) per informazioni dettagliate.

## <a name="dns-zones"></a>Zone DNS

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>Record DNS

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>Time-To-Live

ora Hello toolive o durata (TTL), specifica per quanto tempo ogni record viene memorizzato nella cache dai client prima eseguita nuovamente la query. In hello sopra riportato, hello TTL è 3600 secondi o 1 ora.

Nel sistema DNS di Azure, hello durata (TTL) specificata per i set di record hello, non per ogni record, pertanto hello stesso valore viene utilizzato per tutti i record all'interno di tale record impostati.  È possibile specificare qualsiasi valore TTL compreso tra 1 e 2.147.483.647 secondi.

### <a name="wildcard-records"></a>Record con caratteri jolly

DNS di Azure supporta [record con caratteri jolly](https://en.wikipedia.org/wiki/Wildcard_DNS_record). I record con caratteri jolly vengono restituiti in query tooany risposta con un nome corrispondente (a meno che non esiste una corrispondenza più vicina da un set di record senza caratteri jolly). DNS di Azure supporta set di record con caratteri jolly per tutti i tipi di record tranne NS e SOA.

toocreate un record con caratteri jolly è impostata, utilizzare il nome di set di record hello '\*'. In alternativa, è anche possibile usare un nome con "\*" come etichetta più a sinistra, ad esempio "\*.foo".

### <a name="cname-records"></a>Record CNAME

Set di record CNAME non può coesistere con altri set di record con hello stesso nome. Ad esempio, è possibile creare un record CNAME impostato con il nome relativo hello 'www' e un record con il nome relativo hello 'www' in hello stesso tempo.

Poiché apice zona hello (nome = ' @') contiene sempre i record NS e SOA di hello set che sono stati creati quando è stata creata hello zona, non è possibile creare un record CNAME impostato al vertice zona hello.

Questi vincoli sono causati da standard DNS hello e non sono limitazioni del servizio DNS di Azure.

### <a name="ns-records"></a>Record NS

set di record di Hello NS al vertice zona hello (nome ' @') viene creato automaticamente con ogni zona DNS e viene eliminato automaticamente quando viene eliminata hello (non può essere eliminata separatamente).

Questo set di record contiene i nomi di hello della zona di hello DNS di Azure nome server toohello assegnato. È possibile aggiungere nomi aggiuntivi server toothis NS set di record, toosupport CO-ospitano i domini con più di un provider DNS. È inoltre possibile modificare hello durata (TTL) e i metadati per questo set di record. Tuttavia, è Impossibile rimuovere o modificare server dei nomi DNS di Azure prepopolato hello. 

Si noti che questo si applica solo toohello NS set di record al vertice zona hello. Altri set di record NS nella zona (come le aree figlio toodelegate usato) possono essere creati, modificati ed eliminato senza vincoli.

### <a name="soa-records"></a>Record SOA

Viene creato automaticamente un set di record SOA al vertice hello di ciascuna zona (nome = ' @') e viene eliminata automaticamente quando viene eliminata hello.  I record SOA non possono essere creati o eliminati separatamente.

È possibile modificare tutte le proprietà del record SOA hello ad eccezione di proprietà 'host' hello, nome del server primario nome toohello toorefer preconfigurato fornite da DNS di Azure.

### <a name="spf-records"></a>Record SPF

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>Record SRV

[I record SRV](https://en.wikipedia.org/wiki/SRV_record) usati da diverse posizioni server toospecify di servizi. Quando si specifica un record SRV in DNS di Azure:

* Hello *servizio* e *protocollo* deve essere specificato come parte del nome di set di record hello, preceduto da caratteri di sottolineatura.  Ad esempio, "\_sip.\_tcp.name".  Per un record al vertice zona hello, non è disponibile alcuna necessità toospecify ' @' nel nome del record hello, semplicemente hello servizio e il protocollo, ad esempio utilizzare '\_sip.\_ TCP'.
* Hello *priorità*, *peso*, *porta*, e *destinazione* vengono specificati come parametri di ogni record nel set di record di hello.

### <a name="txt-records"></a>Record TXT

Record TXT sono stringhe di testo tooarbitrary nomi dominio toomap utilizzato. Vengono utilizzati in più applicazioni, in particolare correlati tooemail configurazione, ad esempio hello [Sender Policy Framework (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) e [DomainKeys identificato posta elettronica (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).

standard DNS Hello consente a un singolo toocontain di record TXT più stringhe, ognuna delle quali può essere up too254 caratteri. Se sono usate più stringhe, vengono concatenate dai client e considerate come stringa singola.

Quando si chiama hello REST API DNS di Azure, è necessario toospecify ogni stringa TXT separatamente.  Quando si utilizza hello portale di Azure, PowerShell o CLI interfacce deve specificare una singola stringa per ogni record, viene automaticamente suddivise in segmenti di 254 caratteri, se necessario.

Hello più stringhe in un record DNS non devono essere confuso con hello più record TXT in un set di record TXT.  Un set di record TXT può contenere più record, *ognuno dei quali* può contenere più stringhe.  DNS di Azure supporta una lunghezza di stringa totale di caratteri too1024 in ogni record TXT impostare (per tutti i record combinati).

## <a name="tags-and-metadata"></a>Tag e metadati

### <a name="tags"></a>Tag

I tag sono un elenco di coppie nome-valore e vengono utilizzati dalle risorse toolabel Gestione risorse di Azure.  Azure Resource Manager utilizza viste filtrate tooenable tag della fattura di Azure e consente inoltre tooset un criterio per i quali tag sono necessari. Per ulteriori informazioni sui tag, vedere [tramite tag tooorganize le risorse di Azure](../azure-resource-manager/resource-group-using-tags.md).

DNS di Azure supporta l'uso di tag di Azure Resource Manager in risorse di zona DNS.  Non supporta i tag nei set di record DNS, anche se in alternativa sono supportati i "metadati", come illustrato di seguito.

### <a name="metadata"></a>Metadata

Come impostare i tag, un'alternativa toorecord DNS di Azure supporta annotazione del set di record mediante 'metadata'.  Tootags simile, dei metadati consente si tooassociate coppie nome-valore con ogni set di record.  Ciò può risultare utile, ad esempio cui toorecord hello scopo di ogni record è stato impostato.  A differenza dei tag, i metadati non possono essere utilizzato tooprovide una visualizzazione filtrata della fattura di Azure e non possono essere specificato in un criterio di gestione risorse di Azure.

## <a name="etags"></a>ETag

Si supponga che due utenti o i due processi provare toomodify un record DNS in hello stesso tempo. Quale prevale? E la riga confermata hello sapere che è stato sovrascritto le modifiche create da un altro utente?

DNS di Azure Usa eTag toohandle modifiche simultanee toohello stessa risorsa in modo sicuro. Gli ETag sono separati dai ["tag" di Azure Resource Manager](#tags). Ogni risorsa DNS (zona o set di record) ah un Etag associato. Quando viene recuperata una risorsa, viene recuperato anche il relativo valore Etag. Quando si aggiorna una risorsa, è possibile scegliere nuovamente toopass hello Etag in modo DNS di Azure è possibile verificare tale hello Etag su hello server corrispondenze. Poiché ogni aggiornamento tooa risorsa comporta hello Etag rigenerate, una mancata corrispondenza Etag indica che una modifica simultanea si è verificato. ETag è utilizzabile anche quando si crea un nuovo tooensure risorse che hello risorsa non esiste già.

Per impostazione predefinita, il DNS di Azure PowerShell utilizza eTag tooblock modifiche simultanee toozones e set di record. Hello facoltativo *-sovrascrivere* switch possono essere utilizzati toosuppress controllo Etag, nel qual caso ogni simultanee vengono sovrascritte le modifiche che si sono verificati.

A livello di hello di hello REST API DNS di Azure, ETag vengono specificati utilizzando le intestazioni HTTP.  Il comportamento è specificato in hello nella tabella seguente:

| Intestazione | Comportamento |
| --- | --- |
| None |PUT riesce sempre (nessun controllo di Etag) |
| If-Match <etag> |PUT riesce solo se la risorsa esiste e l'Etag corrisponde |
| If-match * |PUT riesce solo se la risorsa esiste |
| If-none-match * |PUT riesce solo se la risorsa non esiste |


## <a name="limits"></a>Limiti

Quando si utilizza il DNS di Azure, si applica Hello limiti predefiniti seguenti:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>Passaggi successivi

* toostart tramite DNS di Azure, informazioni su come troppo[creare una zona DNS](dns-getstarted-create-dnszone-portal.md) e [creare record DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate una zona DNS esistente, informazioni su come troppo[importare ed esportare un file di zona DNS](dns-import-export.md).
