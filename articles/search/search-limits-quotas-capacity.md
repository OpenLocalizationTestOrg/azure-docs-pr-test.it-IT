---
title: i limiti di aaaService in ricerca di Azure | Documenti Microsoft
description: "Limiti del servizio utilizzati per la pianificazione della capacità e limiti massimi per richieste e risposte in Ricerca di Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Limiti dei servizi in Ricerca di Azure
I limiti massimi per archiviazione, carichi di lavoro e quantità di indici, documenti e altri oggetti dipendono dal [piano tariffario scelto per Ricerca di Azure](search-create-service-portal.md): **Gratuito**, **Basic** o **Standard**.

* **gratuito** è un servizio condiviso multi-tenant fornito con la sottoscrizione di Azure. Questa è un'opzione di alcun costo aggiuntivo per i sottoscrittori esistenti che consente di tooexperiment con servizio hello prima di iscriversi a risorse dedicate.
* Il piano **Basic** fornisce risorse di elaborazione dedicate per carichi di lavoro di produzione di dimensioni ridotte.
* Il piano **Standard** prevede computer dedicati con maggiore capacità di elaborazione e archiviazione a ogni livello. Il piano Standard è disponibile in quattro livelli: S1, S2, S3 e ad alta densità S3 (S3 HD).

> [!NOTE]
> Il provisioning di un servizio viene eseguito in base al piano tariffario specifico. Se è necessario toojump livelli tooget più capacità, è necessario eseguire il provisioning di un nuovo servizio (non è disponibile alcun aggiornamento sul posto). Per altre informazioni, vedere [Scegliere uno SKU o un piano tariffario](search-sku-tier.md). toolearn ulteriori sull'impostazione di capacità all'interno di un servizio è stato già effettuato il provisioning, vedere [livelli di risorsa per query e indicizzazione carichi di lavoro di scala](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Limiti per sottoscrizione
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Limiti per servizio
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Limiti per indice
Esiste una corrispondenza uno a uno tra i limiti sugli indici e sugli indicizzatori. Dato un limite di 200 degli indici, il limite massimo per gli indicizzatori hello è anche 200 per hello stesso servizio.

| Risorsa | Free | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Indice: numero massimo di campi per indice |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Numero massimo di profili di punteggio per indice |100 |100 |100 |100 |100 |100 |
| Numero massimo di funzioni per profilo |8 |8 |8 |8 |8 |8 |
| Indicizzatori: carico di indicizzazione massimo per chiamata |10.000 documenti |Limitato solo da numero massimo di documenti |Limitato solo da numero massimo di documenti |Limitato solo da numero massimo di documenti |Limitato solo da numero massimo di documenti |N/D <sup>2</sup> |
| Indicizzatori: tempo massimo di esecuzione | 1-3 minuti <sup>3</sup> |24 ore |24 ore |24 ore |24 ore |N/D <sup>2</sup> |
| Indicizzatore BLOB: dimensioni massime per un BLOB, MB |16 |16 |128 |256 |256 |N/D <sup>2</sup> |
| Indicizzatore BLOB: numero massimo di caratteri di contenuto estratti da un BLOB |32.000 |64.000 |4 milioni |4 milioni |4 milioni |N/D <sup>2</sup> |

<sup>1</sup> livello basic è hello solo SKU con un limite inferiore pari a 100 campi per indice.

<sup>2</sup> S3 HD attualmente non supporta gli indicizzatori. In caso di esigenze urgenti per questa funzionalità, contattare il supporto tecnico di Azure.

<sup>3</sup> indicizzatore tempo di esecuzione massimo per il livello gratuito hello è 3 minuti per le origini blob e 1 minuto per tutte le altre origini dati.

## <a name="document-size-limits"></a>Limiti per la dimensione dei documenti
| Risorsa | Free | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Dimensione individuale dei documenti per l'API di indice |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |

Quando si chiama un'API di indice, si riferisce toohello dimensioni massime dei documenti. Dimensioni del documento sono effettivamente un limite alle dimensioni di hello di hello corpo della richiesta API di indice. Poiché è possibile passare un batch di più documenti toohello API indice in una sola volta, il limite di dimensioni hello effettivamente dipende il numero di documenti nel batch hello. Per un batch con un unico documento, dimensione massima del documento hello è 16 MB di JSON.

tookeep dimensioni del documento verso il basso, tenere presente i dati non queryable tooexclude dalla richiesta di hello. Le immagini e altri dati binari non sono a query direttamente e non devono essere archiviati nell'indice hello. dati non disponibile per query di toointegrate i risultati della ricerca, definire un campo non ricercabili che archivia una risorsa di toohello riferimento URL.

## <a name="workload-limits-queries-per-second"></a>Limiti dei carichi di lavoro (query al secondo)
| Risorsa | Free | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QUERY AL SECONDO |N/D  |~3 per replica |~15 per replica |~60 per replica |>60 per replica |>60 per replica |

Le query al secondo (query al secondo) è un'approssimazione in base all'euristica, utilizzando i valori di tooderive stimato cliente simulato ed effettivi dei carichi di lavoro. Velocità effettiva esatta variano varia a seconda del natura hello e dati di query hello.

Anche se in precedenza, vengono fornite stime approssimative, una velocità effettiva è difficile toodetermine, soprattutto in hello che gratuito condiviso del servizio in cui la velocità effettiva è basata sulla larghezza di banda disponibile e la concorrenza per le risorse di sistema. Livello gratuito hello, risorse di calcolo e archiviazione sono condivisi da più sottoscrittori, in modo da query al secondo per la soluzione verrà sempre variano a seconda di quanti altri carichi di lavoro in esecuzione in hello contemporaneamente.

Livello standard hello, è possibile stimare variano più strettamente poiché è possibile controllare più parametri hello. Nella sezione hello best practices [gestire la soluzione di ricerca](search-manage.md) per indicazioni su come toocalculate query al secondo per i carichi di lavoro.

## <a name="api-request-limits"></a>Limiti delle richieste API
* 16 MB al massimo per <sup>1</sup> richiesta
* 8 KB al massimo per la lunghezza dell'URL
* 1000 documenti al massimo per ogni batch di carichi, unioni o eliminazioni di indice
* 32 campi al massimo nella clausola $orderby
* 32.766 byte (32 KB meno 2 byte) di testo con codifica UTF-8 per la dimensione massima del termine di ricerca

<sup>1</sup> in ricerca di Azure, il corpo di hello di una richiesta è limite tooan soggetto di 16 MB, che impone un limite pratico contenuto hello di singoli campi o le raccolte che non sono vincolate dai limiti teorici in caso contrario (vedere [supportati tipi di dati](https://msdn.microsoft.com/library/azure/dn798938.aspx) per ulteriori informazioni sulla composizione dei campi e le restrizioni).

## <a name="api-response-limits"></a>Limiti delle risposte API
* 1000 documenti al massimo restituiti per pagina di risultati della ricerca
* 100 suggerimenti al massimo restituiti per richiesta di API di suggerimento

## <a name="api-key-limits"></a>Limiti delle chiavi API
Le chiavi API vengono utilizzate per l'autenticazione del servizio. Sono disponibili due tipi. Chiavi amministratore sono specificate nell'intestazione della richiesta hello e assegnare l'accesso in lettura e scrittura toohello servizio. Le chiavi di query sono di sola lettura, specificato nell'URL hello e le applicazioni distribuite in genere tooclient.

* 2 chiavi di amministrazione al massimo per ogni servizio
* 50 chiavi di query al massimo per ogni servizio
