---
title: le origini dati tooannotate aaaHow | Documenti Microsoft
description: Evidenziazione come tooarticle come tooannotate asset di dati in Azure Data Catalog, inclusi i nomi descrittivi, tag, descrizioni e gli esperti.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>Come origini dati tooannotate
## <a name="introduction"></a>Introduzione
**Microsoft Azure Data Catalog** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali. In altre parole, il catalogo dati è sui consentendo alle persone di individuare, comprendere e utilizzare origini dati e aiutare le organizzazioni tooget maggior valore dai dati esistenti. Quando un'origine dati viene registrata con il catalogo dati, i metadati viene copiato e indicizzato dal servizio hello, ma storia hello non finisce qui. Catalogo dati consente agli utenti tooprovide i propri metadati di hello toosupplement metadati descrittivi, ad esempio descrizioni e contrassegni: estratti dall'origine dati hello e più comprensibile toomore utenti dell'origine dati di hello toomake.

## <a name="annotation-and-crowdsourcing"></a>Annotazione e crowdsourcing
Oggi tutti hanno un parere. E questo è positivo.
Data Catalog riconosce che utenti diversi hanno prospettive diverse sulle origini dati aziendali e che ognuna di queste prospettive può essere utile. Prendere in considerazione hello seguente scenario:

* l'amministratore di sistema Hello SA hello contratto di servizio per server hello o servizi che l'origine dati host hello.
* amministratore del database Hello SA backup hello pianificare per ogni database e l'elaborazione ETL consentiti windows hello.
* proprietario del sistema Hello SA processo hello per gli utenti toorequest accesso toohello origine dati.
* amministratore dei dati Hello sa come asset di hello e gli attributi nell'origine dati hello mapping toohello modello di dati dell'organizzazione.
* analista di Hello sa come dati hello utilizzati nel contesto di hello hello dei processi di business che supporta.

Ognuna di queste prospettive è utile, e il catalogo dati utilizza un toometadata approccio crowdsourcing che consente di ogni uno toobe acquisito e utilizzato tooprovide un quadro completo di origini dati registrate. Tramite il portale di catalogo dati hello, ogni utente può aggiungere e modificare il proprio annotazioni, pur essendo in grado di tooview annotazioni fornite da altri utenti.

## <a name="different-types-of-annotations"></a>Diversi tipi di annotazioni
Dati del catalogo supporta hello seguenti tipi di annotazioni:

| Annotazione | Note |
| --- | --- |
| Nome descrittivo |È possibile fornire nomi descrittivi a livello di asset di dati hello, asset di dati hello toomake più facilmente comprensibile. I nomi descrittivi sono particolarmente utili quando il nome di oggetto sottostante hello è toousers criptiche, abbreviato o in caso contrario non sono significativi. |
| Descrizione |È possibile fornire descrizioni asset di dati hello e attributo / i livelli delle colonne. Le descrizioni sono annotazioni di testo breve in formato libero che descrivono la prospettiva dell'utente hello asset di dati hello o il relativo utilizzo. |
| Tag (tag utente) |È possibile specificare i tag asset di dati hello e attributo / i livelli delle colonne. Tag utente sono etichette definite dall'utente che possono essere utilizzato toocategorize asset di dati o attributi. |
| Tag (tag glossario) |È possibile specificare i tag asset di dati hello e attributo / i livelli delle colonne. Tag di glossario sono definite a livello centralizzato termini che possono essere utilizzato toocategorize asset di dati o gli attributi mediante una comune tassonomia di business. Per ulteriori informazioni vedere [come tooset backup hello glossario aziendale per contrassegnare i governato](data-catalog-how-to-business-glossary.md) |
| Esperti |Gli esperti possono essere forniti a livello di asset di dati hello. Gli esperti identificano utenti o gruppi con prospettive esperta sui dati hello e possono essere utilizzato come punti di contatto per gli utenti individuare hello registrato origini dati e domande che non vengono fornite le annotazioni esistenti hello. |
| Richiedere l'accesso |È possibile fornire informazioni sulla richiesta di accesso a livello di asset di dati hello. Queste informazioni sono per gli utenti di individuare un'origine dati che essi non hanno ancora tooaccess autorizzazioni. Gli utenti possono immettere l'indirizzo di posta elettronica hello di hello utente o gruppo che concede l'accesso, hello URL del processo di hello o strumento è necessario che agli utenti l'accesso toogain o immettere processo hello stesso come testo. |
| Documentazione |È possibile fornire la documentazione a livello di asset di dati hello. La documentazione degli asset è costituita da informazioni in formato RTF che possono includere collegamenti e immagini e fornire informazioni aggiuntive rispetto a descrizioni e tag. |

## <a name="annotating-multiple-assets"></a>Asset con più annotazioni
Quando si selezionano più asset di dati nel portale di catalogo dati hello, gli utenti possono annotare tutte le risorse selezionate in un'unica operazione. Annotazioni verranno applicata tooall selezionato asset, rendendo semplice tooselect e fornire una descrizione di coerenza e set di tag e gli esperti per gli asset di dati correlati.

> [!NOTE]
> Tag e gli esperti inoltre possono essere forniti quando lo strumento di registrazione di origine utilizzando i dati del catalogo dati hello registrazione asset di dati.
>
>

Quando la selezione di più tabelle e viste, solo le colonne che selezionati tutti i dati hanno in comune di attività verrà visualizzata nel portale di hello catalogo dati. In questo modo il tag di tooprovide gli utenti e le descrizioni per tutte le colonne con hello stesso nome per tutti gli asset selezionati.

## <a name="annotations-and-discovery"></a>Individuazione e annotazioni
Come hello metadati estratti dall'origine dati hello durante la registrazione viene aggiunto l'indice di ricerca catalogo dati toohello, viene indicizzato anche i metadati specificati dall'utente. Questo significa che non solo si annotazioni rendono più semplice per i dati di hello toounderstand utenti che individuano annotazioni rendono più semplice per gli asset di dati utenti toodiscover hello annotato eseguendo una ricerca utilizzando termini hello che rendono toothem senso.

## <a name="summary"></a>Riepilogo
Registrazione di un'origine dati con Data Catalog rende individuabili tali dati copiando i metadati strutturali e descrittivo dall'origine dati hello in hello servizio catalogo. Una volta registrata un'origine dati, gli utenti possono fornire annotazioni toomake più semplice toodiscover e comprendere nel portale di catalogo dati hello.

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva di Azure Data Catalog](data-catalog-get-started.md) esercitazione per informazioni dettagliate su come origini dati tooannotate.
