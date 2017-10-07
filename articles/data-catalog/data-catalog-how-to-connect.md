---
title: aaaHow tooconnect toodata origini | Documenti Microsoft
description: "Come-tooarticle evidenziazione della modalità di individuazione delle origini toodata tooconnect con Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>Come origini toodata tooconnect
## <a name="introduction"></a>Introduzione
**Microsoft Azure Data Catalog** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali. In altre parole, **Azure Data Catalog** è tutte sulle persone assistenza individuare, comprendere e utilizzare origini dati e aiutare le organizzazioni tooget più valore dai dati esistenti. Un aspetto essenziale di questo scenario Usa hello: una volta che un utente consente di individuare un tipo di dati di origine e in grado di comprendere lo scopo, hello è tooput dell'origine dati toohello tooconnect toouse relativi dati.

## <a name="data-source-locations"></a>Percorsi di origine dati
Durante la registrazione dell'origine dati **Azure Data Catalog** riceve i metadati sull'origine dati hello. Questi metadati includono dettagli hello del percorso dell'origine dati hello. Dettagli Hello della posizione di hello variano da origine toodata di origine dati, ma conterrà sempre hello tooconnect di informazioni necessarie. Ad esempio, il percorso di hello per una tabella di SQL Server include nome hello del server, nome del database, nome dello schema e nome della tabella, mentre il percorso di hello per un report di SQL Server Reporting Services include il nome di server hello e report di toohello percorso hello. Altri tipi di origini dati saranno necessario percorsi che riflettono la struttura hello e le funzionalità di sistema di origine hello.

## <a name="integrated-client-tools"></a>Strumenti client integrato
Hello più semplice modo tooconnect tooa l'origine dati è toouse hello "Apri in...." menu di hello **Azure Data Catalog** portale. Questo menu Visualizza un elenco di opzioni per la connessione toohello asset di dati selezionata.
Quando si utilizza la visualizzazione affiancata predefinita hello, questo menu è disponibile in hello ogni sezione.

 ![Apertura di una tabella di SQL Server in Excel da hello dati asset immagine](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Quando si utilizza la visualizzazione elenco hello, menu hello è disponibile nella barra di ricerca hello nella parte superiore di hello della finestra portale hello.

 ![Apertura di un report di SQL Server Reporting Services in Gestione Report dalla barra di ricerca hello](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Applicazioni client supportate
Quando si utilizza hello "Apri in...." origini di menu per i dati nel portale di Azure Data Catalog hello, un'applicazione hello corretta del client deve essere installata nel computer client di hello.

| Apri in applicazione | Estensione file/protocollo | Versioni applicazione supportate |
| --- | --- | --- |
| Excel |odc |Excel 2010 o versioni successive |
| Excel (prime 1000) |odc |Excel 2010 o versioni successive |
| Power Query |xlsx |Excel 2016 o Excel 2010 o Excel 2013 con hello Power Query per il componente aggiuntivo per Excel installato. |
| Power BI Desktop |pbix |Power BI Desktop luglio 2016 o versioni successive |
| SQL Server Data Tools |vsweb:// |Visual Studio 2013 Update 4 o versioni successive con strumenti di SQL Server installati |
| Gestione report |http:// |Vedere i [requisiti del browser per SQL Server Reporting Services](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Dati e strumenti
opzioni di Hello disponibili nel menu di hello dipenderanno dal tipo di hello dell'asset di dati attualmente selezionata. Ovviamente, non tutti gli strumenti possibili includerà hello "Apri in...." menu, ma è ancora facile tooconnect origine dati di toohello utilizzando uno strumento client. Quando un asset di dati è selezionato in hello **Azure Data Catalog** portale, percorso completo di hello viene visualizzato nel riquadro Proprietà hello.

 ![Informazioni sulla connessione per una tabella SQL Server](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

informazioni di connessione Hello dettagli saranno diversi dal tipo di origine toodata tipo origine dati, ma informazioni hello incluse nel portale di hello fornirà tutto ciò che occorre tooconnect toohello origine in qualsiasi strumento client. Gli utenti possono copiare i dettagli della connessione hello per le origini dati hello individuati utilizzando **Azure Data Catalog**, consentendo loro toowork con dati hello nello strumento di loro scelta.

## <a name="connecting-and-data-source-permissions"></a>Autorizzazioni dell'origine dati e di connessione
Sebbene **Azure Data Catalog** rende origini dati individuabile, accesso dati toohello stesso rimangano sotto controllo hello del proprietario dell'origine dati hello o un amministratore. Individuazione di un'origine dati in **Azure Data Catalog** non assegnare a un utente autorizzazioni tooaccess hello origini dati stesso.

toomake è più semplice per gli utenti individuare un tipo di dati di origine, ma non dispone dell'autorizzazione tooaccess i dati, gli utenti possono fornire informazioni per hello proprietà richiesta di accesso durante l'annotazione di un'origine dati. Informazioni fornite qui di seguito, inclusi il processo di toohello collegamenti o punto di contatto per ottenere l'accesso all'origine dati: vengono visualizzate insieme alle informazioni sul percorso di origine di hello dati nel portale di hello.

 ![Informazioni sulla connessione con istruzioni fornite per la richiesta di accesso](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Riepilogo
Registrazione di un'origine dati con **Azure Data Catalog** rende individuabili tali dati copiando i metadati strutturali e descrittivo dall'origine dati hello in hello servizio catalogo. Una volta che un'origine dati è stata registrata e individuata, gli utenti possono connettersi toohello origine dei dati da hello **Azure Data Catalog** portale "Apri in...." " o usando gli strumenti dati preferiti.

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva di Azure Data Catalog](data-catalog-get-started.md) esercitazione per informazioni dettagliate su come tooconnect toodata origini.
