---
title: in Azure SQL Data Warehouse aaaAuditing | Documenti Microsoft
description: Introduzione al servizio di controllo di Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Servizio di controllo di Azure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Controllo](sql-data-warehouse-auditing-overview.md)
> * [Introduzione al rilevamento delle minacce](sql-data-warehouse-security-threat-detection.md)
> 
> 

Il controllo di SQL Data Warehouse consente toorecord eventi nel Registro di controllo tooan database nell'account di archiviazione di Azure. Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza. La funzionalità di controllo di SQL Data Warehouse si integra inoltre con Microsoft Power BI per l'esecuzione di analisi e report drill-down.

Gli strumenti di controllo abilitano e semplificare la conformità toocompliance standard, ma non garantiscono la conformità. Per ulteriori informazioni su Azure programmi tale conformità agli standard di supporto, vedere hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.

* [Nozioni di base sul controllo del database]
* [Configurare il controllo per il database]
* [Analizzare i log di controllo e i report]

## <a id="subheading-1"></a>Nozioni di base sul controllo del database di SQL Data Warehouse
Il controllo del database SQL Data Warehouse consente di:

* **Conservare** un audit trail di eventi selezionati. È possibile definire le categorie di database azioni toobe controllato.
* **Creare report** sulle attività del database. È possibile utilizzare i report preconfigurati e tooget un dashboard iniziare rapidamente con attività e la notifica degli eventi.
* **Analizzare** i report. È possibile individuare eventi sospetti, attività insolite e tendenze.

È possibile configurare il controllo per hello seguenti categorie di eventi:

**Normale SQL** e **SQL con parametri** per cui hello i log di controllo raccolti sono classificati come  

* **Accesso toodata**
* **Modifiche dello schema (DDL)**
* **Modifiche dei dati (DML)**
* **Account, ruoli e autorizzazioni (DCL)**
* **Stored procedure**, **accesso** e **gestione delle transazioni**.

Per ogni categoria di eventi, il controllo delle operazioni **riuscite** e **non riuscite** viene configurato separatamente.

Per ulteriori informazioni sulle attività di hello e gli eventi controllati, vedere hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">riferimento di formato di Log di controllo (download di file doc)</a>.

I log di controllo vengono archiviati nell'account di archiviazione di Azure. È possibile definire un periodo di conservazione del log di controllo.

Un criterio di controllo può essere definito per un database specifico o come criterio server predefinito. Un criterio di controllo del server predefinito si applica tooall database in un server, che non dispongono di un override database controllo definiti criteri specifici.

Prima di impostare il controllo, verificare che si stia usando un [client di livello inferiore](sql-data-warehouse-auditing-downlevel-clients.md).

## <a id="subheading-2"></a>Configurare il controllo per il database
1. Avviare hello <a href="https://portal.azure.com" target="_blank">portale di Azure</a>.
2. Passare toohello **impostazioni** blade di hello desiderato tooaudit SQL Data Warehouse. In hello **impostazioni** pannello seleziona **rilevamento controllo & minaccia**.
   
    ![][1]
3. Successivamente, abilitare il controllo, fare clic su hello **ON** pulsante.
   
    ![][3]
4. Nel Pannello di configurazione di controllo di hello, selezionare **dettagli archiviazione** Pannello di controllo log archiviazione tooopen hello. Selezionare account di archiviazione di Azure in cui verranno salvati i log hello e hello periodo di memorizzazione. 
>[!TIP]
>Hello utilizzare stesso account di archiviazione per tutti i hello tooget database controllati meglio hello preconfigurato report modelli.
   
    ![][4]
5. Fare clic su hello **OK** configurazione di pulsante toosave hello archiviazione dei dettagli.
6. In **registrazione dall'evento**, fare clic su **successo** e **errore** toolog tutti gli eventi, oppure scegliere singole categorie di eventi.
7. Se si configura servizio di controllo per un database, potrebbe essere una stringa di connessione hello tooalter di tooensure il client controllo dei dati viene acquisito in modo corretto. Controllare hello [modificare nome FDQN di Server nella stringa di connessione hello](sql-data-warehouse-auditing-downlevel-clients.md) argomento per le connessioni client di livello inferiore.
8. Fare clic su **OK**.

## <a id="subheading-3"></a>Analizzare i log di controllo e i report
I log di controllo vengono aggregati in una raccolta di tabelle di archivio con un **SQLDBAuditLogs** prefisso in hello account di archiviazione di Azure si è scelto durante l'installazione. È possibile visualizzare i file di log con uno strumento come <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Esplora archivi di Azure</a>.

Un modello di report preconfigurati dashboard è disponibile come una <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">scaricabile foglio di calcolo Excel</a> toohelp per analizzare rapidamente i dati di log. toouse hello modello sul seguente modello i log di controllo, è necessario in Excel 2013 o versioni successive e Power Query, che è possibile scaricare <a href="http://www.microsoft.com/download/details.aspx?id=39379">qui</a>.

modello Hello contiene dati di esempio fittizio ed è possibile impostare Power Query tooimport il log di controllo direttamente dall'account di archiviazione di Azure.

## <a id="subheading-4"></a>Rigenerazione delle chiavi di archiviazione
Nell'ambiente di produzione, si è probabilmente toorefresh lo spazio di archiviazione chiavi periodicamente. Durante l'aggiornamento delle chiavi, è necessario criteri hello toosave. il processo di Hello è come segue:

1. In hello controllo pannello configurazione (descritto in precedenza nel programma di installazione hello controllo sezione) passare hello **chiave di accesso di archiviazione** da *primario* troppo*secondario* e  **SALVARE**.

   ![][4]
2. Pannello di configurazione di archiviazione di passare toohello e **rigenerare** hello *chiave di accesso primaria*.
3. Tornare indietro toohello controllo pannello configurazione hello commutatore **chiave di accesso di archiviazione** da *secondario* troppo*primario* e premere **salvare**.
4. Tornare indietro archiviazione toohello dell'interfaccia utente e **rigenerare** hello *chiave di accesso secondaria* (per la preparazione di hello chiavi successive ciclo di aggiornamento.

## <a id="subheading-5"></a>Automazione (API REST/PowerShell)
È inoltre possibile configurare il controllo in Azure SQL Data Warehouse utilizzando i seguenti strumenti di automazione hello:

* **Cmdlet di PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[Nozioni di base sul controllo del database]: #subheading-1
[Configurare il controllo per il database]: #subheading-2
[Analizzare i log di controllo e i report]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy