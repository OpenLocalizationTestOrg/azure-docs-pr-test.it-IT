---
title: origini aaaData supportate in Azure Analysis Services | Documenti Microsoft
description: Descrive le origini dati supportate per i modelli di dati di Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Origini dati supportate in Azure Analysis Services
Server Azure di Analysis Services supporta origini toodata connessione cloud hello e locale nell'organizzazione. Origini dati supportate aggiuntivi vengono aggiunti tutti i tempi di hello. Ricontrollare spesso. 

Hello seguenti origini dati è attualmente supportata:

| Cloud  |
|---|
| Archiviazione BLOB di Azure*  |
| Database SQL di Azure  |
| Azure Data Warehouse |


| Locale  |   |   |   |
|---|---|---|---|
| Database di Access  | Cartella* | Oracle Database  | Database Teradata |
| Active Directory*  | Documento JSON*  | Database PostgreSQL*  |Tabella XML* |
| Analysis Services  | Righe da file binario*  | SAP HANA*  |
| Piattaforma di strumenti analitici  | MySQL Database  | SAP Business Warehouse*  | |
| Dynamics CRM*  | Feed OData*  | SharePoint*  |
| Cartella di lavoro di Excel  | Query ODBC  | Database SQL  |
| Exchange*  | OLE DB  | Database di Sybase  |

\* Solo modelli tabulari 1400. 

> [!IMPORTANT]
> Connessione dati locale tooon origini richiedono un [gateway dati locale](analysis-services-gateway.md) installato in un computer nell'ambiente in uso.

## <a name="data-providers"></a>Provider di dati

Modelli di dati in Azure Analysis Services, potrebbero essere diversi provider di dati durante la connessione a origini dati toocertain. In alcuni casi, i modelli tabulari la connessione a origini di toodata utilizzando provider nativi, ad esempio SQL Server Native Client (SQLNCLI11) possono restituire un errore.

Per i modelli di dati che si connettono tooa i dati nel cloud di origine, ad esempio Database SQL di Azure, se si utilizza il provider nativo diverso da SQLOLEDB, venga visualizzato il messaggio di errore: **"hello del provider 'SQLNCLI11.1' non è registrato."** O, se si dispone di DirectQuery connessione locale tooon origini dati del modello se si utilizzano provider nativi venga visualizzato il messaggio di errore: **"Errore durante la creazione di set di righe OLE DB. Sintassi errata vicino a 'LIMIT'"**.

Hello seguenti provider di origine dati è supportato per i modelli di dati DirectQuery o in memoria quando toodata connessione origini in locale o cloud hello:

### <a name="cloud"></a>Cloud
| **Origine dati** | **In-memory** | **DirectQuery** |
|  --- | --- | --- |
| Azure SQL Data Warehouse |Provider di dati .NET Framework per SQL Server |Provider di dati .NET Framework per SQL Server |
| Database SQL di Azure |Provider di dati .NET Framework per SQL Server |Provider di dati .NET Framework per SQL Server | |

### <a name="on-premises-via-gateway"></a>Locale (tramite gateway)
|**Origine dati** | **In-memory** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |Provider di dati .NET Framework per SQL Server |
| SQL Server |Provider Microsoft OLE DB per SQL Server |Provider di dati .NET Framework per SQL Server | |
| SQL Server |Provider di dati .NET Framework per SQL Server |Provider di dati .NET Framework per SQL Server | |
| Oracle |Provider Microsoft OLE DB per Oracle |Provider di dati Oracle per .NET | |
| Oracle |Provider di dati Oracle per .NET |Provider di dati Oracle per .NET | |
| Teradata |Provider OLE DB per Teradata |Provider di dati Teradata per .NET | |
| Teradata |Provider di dati Teradata per .NET |Provider di dati Teradata per .NET | |
| Piattaforma di strumenti analitici |Provider di dati .NET Framework per SQL Server |Provider di dati .NET Framework per SQL Server | |

> [!NOTE]
> Quando si usa il gateway locale, verificare che siano installati provider a 64 bit.
> 
> 

Durante la migrazione di un tooAzure di modello tabulare di SQL Server Analysis Services locale Analysis Services, potrebbe essere provider hello toochange necessarie.

**toospecify un provider di origine dati**

1. In SSDT > **Esplora modelli tabulari** > **Origini dati** fare clic con il pulsante destro del mouse su una connessione a un'origine dati e scegliere **Modifica origine dati**.
2. In **Modifica connessione**, fare clic su **avanzate** finestra delle proprietà avanzate di tooopen hello.
3. In **Set avanzate Properties** > **provider**, quindi selezionare hello provider appropriato.

## <a name="impersonation"></a>Rappresentazione
In alcuni casi, potrebbe essere necessario toospecify un account di rappresentazione diverse. L'account di rappresentazione può essere specificato in SSDT o SSMS.

Per le origini dati locali:

* Se si usa l'autenticazione SQL, la rappresentazione deve essere l'account del servizio.
* Se si usa l'autenticazione di Windows, impostare nome utente/password di Windows. Per SQL Server, l'autenticazione di Windows con un account di rappresentazione specifico è supportata solo per i modelli di dati In-memory.

Per le origini dati cloud:

* Se si usa l'autenticazione SQL, la rappresentazione deve essere l'account del servizio.

## <a name="next-steps"></a>Passaggi successivi
Se si dispone di origini dati locali, hello tooinstall assicurarsi di essere [gateway locale](analysis-services-gateway.md).   
toolearn più sulla gestione dei server in SSDT o SQL Server Management Studio, vedere [gestire il server](analysis-services-manage.md).

