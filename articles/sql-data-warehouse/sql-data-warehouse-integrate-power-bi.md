---
title: Usare Power BI con SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Usare Power BI con SQL Data Warehouse
Analogamente al database SQL di Azure, SQL Data Warehouse Direct Connect permette agli utenti di sfruttare le capacità avanzate di pushdown logico insieme alle capacità analitiche di Power BI.  Con Direct Connect le query vengono restituite ad Azure SQL Data Warehouse in tempo reale durante l'esplorazione dei dati.  Unitamente alla scalabilità di SQL Data Warehouse, ciò permette agli utenti di creare report dinamici in pochi minuti su terabyte di dati.  L'introduzione del pulsante Apri in Power BI permette agli utenti di connettere direttamente Power BI al proprio SQL Data Warehouse, senza raccogliere informazioni da altre parti di Azure.

Quando si usa Direct Connect, occorre notare quanto segue:

* Specificare il nome completo del server durante la connessione. Per altri dettagli, vedere più avanti.
* Assicurarsi che le regole del firewall per il database siano configurate su "Consenti l'accesso a Servizi di Azure".
* Ogni azione, ad esempio la selezione di una colonna o l'aggiunta di un filtro, eseguirà direttamente una query nel data warehouse.
* I riquadri vengono aggiornati ogni 15 minuti circa. Non è necessario pianificare l'aggiornamento.
* Non sono disponibili domande e risposte per i set di dati di Direct Connect.
* Le modifiche allo schema non vengono rilevate automaticamente.
* Tutte le query di Direct Connect scadranno dopo 2 minuti

Queste restrizioni e note sono soggette a modifiche nel corso del miglioramento delle esperienze. I passaggi per la connessione sono illustrati nel dettaglio più avanti.  

## <a name="using-the-open-in-power-bi-button"></a>Uso del pulsante "Apri in Power BI"
Il modo più semplice per spostarsi tra SQL Data Warehouse e Power BI consiste nell'usare il pulsante Apri in Power BI. Questo pulsante permette di creare con facilità nuovi dashboard in Power BI.  

1. Per iniziare, passare all'istanza di SQL Data Warehouse nel portale di Azure classico.
2. Fare clic sul pulsante Apri in Power BI.
3. Se non è possibile accedere direttamente o se non si ha un account di Power BI, sarà necessario effettuare l'accesso.  
4. Si verrà indirizzati alla pagina di connessione di SQL Data Warehouse, con le informazioni di SQL Data Warehouse pre-popolate.
5. Dopo l'immissione delle credenziali, si sarà completamente connessi a SQL Data Warehouse.

## <a name="connecting-through-the-power-bi-portal"></a>Connessione tramite il portale di Power BI
Oltre a usare il pulsante Apri in Power BI, gli utenti possono connettersi a SQL Data Warehouse anche tramite il portale di Power BI.

1. Fare clic su ’Recupera dati’ nella parte inferiore del pannello di navigazione.
2. Selezionare 'Database'.
3. Una volta nella pagina database selezionare 'SQL Azure Data Warehouse' e poi fare clic su ’Connetti’.
4. Immettere le informazioni di connessione necessarie.  Il nome del server e il nome del database sono disponibili nel portale di Azure.
5. Si verrà indirizzati di nuovo alla pagina principale di Power BI e dopo che la connessione viene stabilita, verrà visualizzata una nuova voce in 'set di dati con il nome dell'istanza.  
6. È possibile fare clic sul nuovo set di dati per esplorare tutte le tabelle e le visualizzazioni del database. Se si seleziona una colonna, una query verrà restituita all'origine, creando dinamicamente l'oggetto visivo. Gli oggetti visivi possono essere salvati in un nuovo report e aggiunti nuovamente al dashboard.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
