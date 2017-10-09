---
title: aaaPorts oltre 1433 per il Database SQL | Documenti Microsoft
description: Le connessioni client da ADO.NET tooAzure Database SQL a volte ignorare il proxy di hello e interagiscono direttamente con il database di hello. Le porte diverse da 1433 diventano importanti.
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a>Porte successive alla 1433 per ADO.NET 4.5
Questo argomento descrive il comportamento di connessione di hello Database SQL di Azure per i client che usano ADO.NET 4.5 o versione successiva. 

> [!IMPORTANT]
> Per informazioni sull'architettura di connettività, vedere [Architettura della connettività del database SQL di Azure](sql-database-connectivity-architecture.md).
>

## <a name="outside-vs-inside"></a>Esterno rispetto all'interno
Per le connessioni tooAzure Database SQL, è necessario innanzitutto chiedere se viene eseguito il programma client *esterno* o *all'interno di* limiti di hello cloud di Azure. nelle sottosezioni Hello illustrano due scenari comuni.

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*Esterno:* il client è in esecuzione nel computer desktop
La porta 1433 è hello solo la porta che deve essere aperta nel computer desktop che ospita l'applicazione client di Database SQL.

#### <a name="inside-client-runs-on-azure"></a>*All'interno:* il client è in esecuzione in Azure
Quando il client viene eseguita all'interno dei confini di hello cloud di Azure, viene utilizzato è possibile chiamare un *route diretta* toointeract con il server di Database SQL di hello. Dopo aver stabilita una connessione, altre interazioni tra client hello e database non implicano alcun proxy middleware.

sequenza di Hello è come segue:

1. ADO.NET 4.5 (o versioni successive) avvia una breve interazione con hello cloud di Azure e riceve un numero di porta identificato in modo dinamico.
   
   * numero di porta Hello identificato in modo dinamico è compreso nell'intervallo di hello di 11000 11999 o 14000 14999.
2. ADO.NET si connette quindi il server di Database SQL toohello direttamente, con nessuna middleware tra.
3. Le query vengono inviate direttamente toohello database e i risultati vengono restituiti toohello client direttamente.

Verificare che tale porta hello intervalli di 11000 11999 e 14000-14999 nel computer client di Azure rimangono disponibili per le interazioni client ADO.NET 4.5 con il Database SQL.

* In particolare, le porte nell'intervallo di hello devono rimanere libere da eventuali altri blocchi in uscita.
* Nella macchina virtuale di Azure, hello **Windows Firewall con sicurezza avanzata** controlli hello impostazioni della porta.
  
  * È possibile utilizzare hello [interfaccia utente del firewall](http://msdn.microsoft.com/library/cc646023.aspx) tooadd una regola per cui si specifica hello **TCP** come protocollo insieme a un intervallo di porte con sintassi hello **11000 11999**.

## <a name="version-clarifications"></a>Chiarimenti sulla versione
In questa sezione illustra i moniker hello che fanno riferimento le versioni tooproduct. Sono inoltre indicate alcune associazioni di versioni tra prodotti.

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 supporta il protocollo TDS 7.3 hello, ma non 7.4.
* ADO.NET 4.5 e versioni successive supporta il protocollo TDS 7.4 hello.

## <a name="related-links"></a>Collegamenti correlati
* ADO.NET 4.6 è stato rilasciato il 20 luglio 2015. È disponibile un annuncio sul blog del team di .NET hello [qui](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).
* ADO.NET 4.5 è stato rilasciato il 15 agosto 2012. È disponibile un annuncio sul blog del team di .NET hello [qui](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).
  
  * È disponibile un post di blog su ADO.NET 4.5.1 [qui](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).
* [Elenco versioni del protocollo TDS](http://www.freetds.org/userguide/tdshistory.htm)
* [Panoramica dello sviluppo di database SQL](sql-database-develop-overview.md)
* [Firewall del database SQL di Azure](sql-database-firewall-configure.md)
* [Procedura: configurare le impostazioni del firewall su Database SQL](sql-database-configure-firewall-settings.md)

