---
title: aaaSet backup glossario aziendale hello per contrassegnare gestita in Azure Data Catalog | Documenti Microsoft
description: Come tooarticle evidenziazione glossario hello aziendale in Azure Data Catalog per definire e utilizzare un tootag di vocabolario aziendale comune registrato asset di dati.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>Impostare glossario aziendale hello per governato tag
## <a name="introduction"></a>Introduzione
Azure Data Catalog consente l'individuazione dell'origine dati, in modo da poter facilmente individuare e comprendere le origini dati hello necessari tooperform analysis e prendere decisioni. Queste funzionalità verificare l'impatto maggiore sul hello quando è possibile trovare e comprendere più ampia gamma di hello delle origini dati disponibili.

L'assegnazione di tag è una delle funzionalità di Data Catalog che aiuta a capire i dati relativi agli asset. Tramite l'assegnazione di tag, è possibile associare le parole chiave con una risorsa o una colonna, che a sua volta rende più semplice asset di hello toodiscover tramite ricerca o esplorazione. Tag consente inoltre di più facile comprendere il contesto di hello e finalità dell'asset hello.

L'assegnazione di tag può, tuttavia, causare a volte problemi. Alcuni dei problemi causati dall'assegnazione di tag sono illustrati di seguito:

* Hello l'utilizzo di abbreviazioni su alcune attività e testo espanso nelle altre. Questa incoerenza ostacola l'individuazione di hello degli asset, anche se con finalità di hello è asset hello tootag con hello stesso tag.
* Potenziali variazioni nel significato, a seconda del contesto. Ad esempio, un tag chiamato *ricavi* a un cliente set di dati potrebbe ricavi per cliente, ma hello stesso tag in un set di dati di vendita trimestrali potrebbe indicano i ricavi trimestrali per società hello.  

toohelp affrontare queste e altre problematiche simile, il catalogo dati include un glossario aziendale.

Utilizzando glossario di hello catalogo dati business, un'organizzazione è possibile documentare i termini aziendali principali e i relativi toocreate definizioni un vocabolario aziendale comune. Questo controllo consente la coerenza nell'utilizzo di dati organizzazione hello. Dopo aver definito un termine di glossario aziendale hello, possono essere assegnato tooa asset di dati nel catalogo di hello. Questo approccio, *governato tag*, è hello stesso approccio di tag.

## <a name="glossary-availability-and-privileges"></a>Disponibilità e privilegi del glossario
Glossario aziendale Hello è disponibile solo nell'edizione Standard di Azure Data Catalog hello. Hello edizione gratuita di catalogo di dati non include un glossario e non fornisce funzionalità per contrassegnare gestita.

È possibile accedere glossario aziendale hello tramite hello **glossario** opzione nel menu di navigazione del portale di hello catalogo dati.  

![L'accesso a glossario aziendale hello](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

Gli amministratori del catalogo dati e i membri del glossario hello ruolo administrators possa creare, modificare ed eliminare i termini del glossario in glossario aziendale hello. Tutti gli utenti del catalogo dati è possono visualizzare le definizioni di termini hello e alle risorse dei tag con i termini del glossario.

![Aggiunta di un nuovo termine di glossario](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>Creazione dei termini di glossario
Gli amministratori del catalogo dati e gli amministratori di glossario possono creare i termini del glossario facendo hello **nuovo termine** pulsante. Ogni termine di glossario contiene hello seguenti campi:

* Una definizione di business per il termine hello
* Una descrizione che acquisisce le regole di utilizzo o business hello destinato per asset hello o una colonna
* Un elenco di parti interessate che conoscono hello più sul termine hello
* termine padre Hello, che definisce una gerarchia di hello in cui hello è organizzato termine

## <a name="glossary-term-hierarchies"></a>Gerarchie dei termini di glossario
Utilizzando glossario di hello catalogo dati business, un'organizzazione può descrivere il vocabolario aziendale come una gerarchia di termini e può creare una classificazione di termini che meglio rappresenta la tassonomia di business.

Un termine deve essere univoco in un determinato livello della gerarchia. I nomi duplicati non sono consentiti. Non esiste alcun toohello limita il numero di livelli in una gerarchia, ma una gerarchia è spesso più facile comprensione quando sono presenti tre livelli o meno.

utilizzo di Hello delle gerarchie nel glossario aziendale hello è facoltativo. Lasciando hello padre termine campo vuoto per i termini del glossario crea un elenco semplice (non gerarchici) delle condizioni nel glossario hello.  

## <a name="tagging-assets-with-glossary-terms"></a>Assegnazione di tag agli asset con termini di glossario
Dopo aver definiti i termini del glossario all'interno del catalogo hello, esperienza hello della codifica di asset è glossario hello toosearch ottimizzato quando un utente digita un tag. portale di catalogo dati Hello Visualizza un elenco di toochoose termini di glossario corrispondente da. Se un termine di glossario hello selezione dall'elenco di hello, termine hello viene aggiunto toohello asset come tag (anche noto come un tag di glossario). Hello utente può anche scegliere toocreate un nuovo tag digitando un termine che non sia in hello glossario (anche noto come un tag utente).

![Assegnazione di tag ad asset di dati con un tag utente o due tag di glossario](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> Tag utente vengono hello solo tipo di tag supportati in hello edizione gratuita di catalogo dati.
>
>

### <a name="hover-behavior-on-tags"></a>Comportamento al passaggio del mouse sui tag
Nel portale di catalogo dati hello hello due tipi di tag sono i comportamenti visivamente distinti e presenti diversi al passaggio del mouse. Quando passa il mouse su un tag di utente, è possibile visualizzare il testo di tag hello e hello o più utenti che hanno aggiunto il tag di hello. Quando si passa il mouse su un tag di glossario, è anche possibile visualizzare hello definizioni del termine di glossario hello e un collegamento tooopen hello business glossario tooview hello completa del termine hello.

### <a name="search-filters-for-tags"></a>Filtri di ricerca per i tag
È possibile cercare sia che i tag di glossario che i tag utente e applicarli come filtri in una ricerca.

## <a name="summary"></a>Riepilogo
Glossario aziendale hello in Azure Data Catalog e hello governato consente la codifica è possibile di identificare, gestire e individuare gli asset di dati in modo coerente. Glossario aziendale Hello possibile promuovere l'apprendimento di vocabolario aziendale hello dai membri dell'organizzazione. Glossario di Hello supporta inoltre l'acquisizione metadati significativo, che semplifica la comprensione e l'individuazione di asset.

## <a name="next-steps"></a>Passaggi successivi
* [Documentazione relativa all'API REST per operazioni che riguardano il glossario aziendale](https://msdn.microsoft.com/library/mt708855.aspx)
