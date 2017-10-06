---
title: Power BI con SQL Data Warehouse aaaUse | Documenti Microsoft
description: Suggerimenti per l'uso di Power BI con Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Usare Power BI con SQL Data Warehouse
Come con Database SQL di Azure SQL Data Warehouse diretto Connect consente utente tooleverage potente logico distribuzione insieme alle funzionalità analitiche di hello di Power BI.  Con la connessione diretta le query vengono inviate tooyour indietro Azure SQL Data Warehouse in tempo reale durante l'esplorazione dati hello.  Questa operazione, combinati con scala hello di SQL Data Warehouse, consente agli utenti report dinamici toocreate in minuti per terabyte di dati.  Inoltre, introduzione hello di hello Apri nel pulsante di Power BI consente agli utenti toodirectly connettere Power BI tootheir SQL Data Warehouse senza la raccolta di informazioni da altre parti di Azure.

Quando si usa Direct Connect, occorre notare quanto segue:

* Specificare hello nome completo del server durante la connessione (vedere di seguito per altri dettagli)
* Verificare le regole del firewall per database hello configurati troppo "consentono accesso tooAzure servizi".
* Ogni azione, ad esempio la selezione di una colonna o l'aggiunta di un filtro direttamente eseguirà una query data warehouse di hello
* Riquadri vengono aggiornati all'incirca ogni 15 minuti (aggiornamento non è necessario toobe pianificata)
* Non sono disponibili domande e risposte per i set di dati di Direct Connect.
* Le modifiche allo schema non vengono rilevate automaticamente.
* Tutte le query di Direct Connect scadranno dopo 2 minuti

Queste restrizioni e note possono cambiare mentre continuiamo tooimprove hello esperienze. Hello passaggi tooconnect è illustrata di seguito.  

## <a name="using-hello-open-in-power-bi-button"></a>Pulsante 'Apri in Power BI' hello
toomove modo più semplice di Hello tra SQL Data Warehouse e Power BI è hello Apri nel pulsante di Power BI. Questo pulsante consente tooseamlessly iniziare a creare nuovi dashboard in Power BI.  

1. tooget avviato passare l'istanza di SQL Data Warehouse tooyour nel portale di Azure classico hello.
2. Fare clic su pulsante 'Apri in Power BI' hello.
3. Se non è in grado di toosign in direttamente, o se non si dispone di un account Power BI, sarà necessario toosign-in.  
4. Si verrà reindirizzati pre-popolati toohello pagina connessione a SQL Data Warehouse, con informazioni hello del proprio SQL Data Warehouse.
5. Dopo aver immesso le credenziali sarà completamente connesso tooyour SQL Data Warehouse.

## <a name="connecting-through-hello-power-bi-portal"></a>Connessione tramite il portale di Power BI hello
In aggiunta toousing Ciao Apri pulsante Power BI, gli utenti possono connettersi tootheir SQL Data Warehouse tramite hello portale di Power BI.

1. Fare clic su "Dati" nella parte inferiore di hello del riquadro di spostamento hello.
2. Selezionare 'Database'.
3. Una volta nella pagina database hello, selezionare "Azure SQL Data Warehouse" e quindi fare clic su 'Connetti'.
4. Immettere le informazioni di connessione necessarie hello.  Nome del server e nome del database è reperibile nel portale di Azure hello.
5. Nuovo si verrà reindirizzati verrà visualizzata la pagina principale di toohello di Power BI e dopo la connessione viene stabilita una nuova voce in 'set di dati con nome hello dell'istanza.  
6. È possibile fare clic su hello nuovo set di dati tooexplore tutti hello tabelle e viste nel database. Selezione di una colonna invierà un'origine toohello indietro di query, creando dinamicamente l'oggetto visivo. Gli oggetti visivi possono essere salvati in un nuovo report e riaggiunti tooyour dashboard.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
