---
title: aaaGet avviato al controllo del database SQL di Azure | Documenti Microsoft
description: Introduzione al servizio di controllo del database SQL di Azure
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a>Introduzione al controllo del database SQL
Controllo del database SQL Azure tiene traccia degli eventi di database e li scrive i log di controllo tooan nell'account di archiviazione di Azure. Inoltre, il servizio di controllo:

* Consente di gestire la conformità alle normative, ottenere informazioni sull'attività del database e rilevare discrepanze e anomalie che potrebbero indicare problemi aziendali o possibili violazioni della sicurezza.

* Abilita e facilita norme toocompliance la conformità, anche se non garantisce la conformità. Per ulteriori informazioni su Azure programmi tale conformità agli standard di supporto, vedere hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).


## <a id="subheading-1"></a>Panoramica del servizio di controllo del database SQL di Azure
È possibile usare il servizio di controllo del database SQL per eseguire le operazioni seguenti:


* **Conservare** un audit trail di eventi selezionati. È possibile definire le categorie di database azioni toobe controllato.
* **Creare report** sulle attività del database. È possibile utilizzare i report preconfigurati e tooget un dashboard iniziare rapidamente con attività e la notifica degli eventi.
* **Analizzare** i report. È possibile individuare eventi sospetti, attività insolite e tendenze.

È possibile configurare il controllo per diversi tipi di categorie di eventi, come illustrato in hello [impostare il controllo per il database](#subheading-2) sezione.

I log di controllo vengono scritti nell'archiviazione Blob tooAzure nella sottoscrizione di Azure.


## <a id="subheading-8"></a>Definire criteri di controllo a livello di server o a livello di database

I criteri di controllo possono essere definiti per un database specifico o come criteri server predefiniti:

* Un criterio server applica tooall esistenti e nuovi database creati nel server di hello.

* Se *è abilitato il controllo blob server*, si *applica sempre toohello database* (vale a dire database hello verrà controllati), indipendentemente dal database hello le impostazioni di controllo.

* Abilitare il controllo sul database hello, in aggiunta tooenabling nel server di hello, blob verrà *non* eseguire l'override o modificare le impostazioni di hello del controllo di hello server blob. I due controlli coesisteranno. In altre parole, il database di hello verrà controllato due volte in parallelo (una volta dal criterio di server hello e una volta dai criteri database hello).

   > [!NOTE]
   > È consigliabile evitare di abilitare contemporaneamente il controllo BLOB del server e il controllo BLOB del database ad eccezione dei casi seguenti:
    > * Si desidera un altro toouse *account di archiviazione* o *periodo di memorizzazione* per un database specifico.
    > * Si desidera tooaudit evento tipi o categorie per un database specifico che differiscono dai tipi di evento o alle categorie che vengono controllate per rest hello database hello hello server. Ad esempio, potrebbe essere inserimenti nella tabella che devono toobe controllati solo per un database specifico.
   > 
   > In caso contrario, è consigliabile abilitare il servizio controllo blob solo a livello di server e lasciare controllo a livello di database hello disabilitato per tutti i database.


## <a id="subheading-2"></a>Configurare il controllo per il database
Hello nella sezione seguente descrive hello configurazione di controllo utilizzando hello portale di Azure.

1. Passare toohello [portale di Azure](https://portal.azure.com).
2. Passare toohello **impostazioni** blade di hello SQL database di SQL server si desidera tooaudit. In hello **impostazioni** pannello seleziona **rilevamento controllo & minaccia**.

    <a id="auditing-screenshot"></a>![Riquadro di spostamento][1]
3. Se si preferisce tooset un criterio di controllo server (che verranno applicati tooall esistenti e nuovi database creati in questo server), è possibile selezionare hello **visualizzare impostazioni del server** collegamento nel Pannello di controllo database hello. È possibile visualizzare o modificare le impostazioni di controllo server hello.

    ![Riquadro di spostamento][2]
4. Se si preferisce tooenable blob controllo a livello di database hello (in aggiunta tooor anziché il controllo a livello di server), per **controllo**selezionare **ON**e per **il controllo tipo** , selezionare **Blob**.

    Se il servizio controllo blob server è abilitato, controllo database configurato hello esisterà in modo affiancato con controllo del blob hello server.  

    ![Riquadro di spostamento][3]
5. hello tooopen **Audit Log archiviazione** pannello seleziona **dettagli archiviazione**. Selezionare l'account di archiviazione di Azure hello in cui verranno salvati i log e quindi selezionare il periodo di memorizzazione hello, dopo il quale hello verranno eliminati i log precedenti. Fare quindi clic su **OK**. 
   >[!TIP] 
   >hello tooget meglio modelli report controllo hello, utilizzare hello stesso account di archiviazione per tutti i database controllati. 

    <a id="storage-screenshot"></a>![Riquadro di spostamento][4]
6. Se si desidera che gli eventi controllato hello toocustomize, è possibile eseguire questa operazione tramite PowerShell o hello API REST. Per ulteriori informazioni, vedere hello [automazione (API REST di PowerShell /)](#subheading-7) sezione.
7. Dopo aver configurato le impostazioni di controllo, è possibile attivare la nuova funzionalità di rilevamento minacce hello e configurare gli avvisi di sicurezza tooreceive messaggi di posta elettronica. Quando si usa il rilevamento delle minacce, si ricevono avvisi proattivi sulle attività di database anomale che possono indicare potenziali minacce per la sicurezza. Per altri dettagli, vedere l'[introduzione al rilevamento delle minacce](sql-database-threat-detection-get-started.md).
8. Fare clic su **Salva**.





## <a id="subheading-3"></a>Analizzare i log di controllo e i report
I log di controllo vengono aggregati in hello account di archiviazione di Azure si è scelto durante l'installazione. È possibile esplorare i log di controllo con uno strumento come [Azure Storage Explorer](http://storageexplorer.com/).

I log del controllo BLOB vengono salvati come raccolta di file BLOB in un contenitore denominato **sqldbauditlogs**.

Per ulteriori informazioni sulla gerarchia hello della cartella di archiviazione dei registri di controllo di hello blob, convenzioni di denominazione dei blob e il formato di log, vedere hello [Blob Audit Log formato riferimento (download di file con estensione docx)](https://go.microsoft.com/fwlink/?linkid=829599).

Esistono diversi metodi che è possibile utilizzare i blob tooview i registri di controllo:

* Hello utilizzare [portale di Azure](https://portal.azure.com).  Database rilevanti hello aperto. Hello in cima del database hello **rilevamento controllo & minaccia** pannello, fare clic su **Visualizza log di controllo**.

    ![Riquadro di spostamento][7]

    Un **record di controllo** apre pannello, da cui sarà in grado di tooview hello registri.

    - È possibile visualizzare date specifiche facendo clic su **filtro** nella parte superiore di hello di hello **record di controllo** blade.
    - È possibile passare dai record di controllo creati dai criteri del server a quelli creati dai criteri del database e viceversa.

       ![Riquadro di spostamento][8]

* Utilizzare la funzione di sistema hello **Sys. fn_get_audit_file** (T-SQL) tooreturn hello controllo dati di log in formato tabulare. Per ulteriori informazioni sull'utilizzo di questa funzione, vedere hello [documentazione Sys. fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).


* Usare **Unisci file di controllo** in SQL Server Management Studio (a partire da SSMS 17):  
    1. Scegliere dal menu SSMS hello **File** > **aprire** > **i file di controllo di tipo Merge**.

        ![Riquadro di spostamento][9]
    2. Hello **aggiungere i file di controllo** verrà visualizzata la finestra di dialogo. Selezionare una delle hello **Aggiungi** opzioni per scegliere se i file di controllo toomerge da una variabile locale del disco o importarli da archiviazione di Azure (si sarà necessario tooprovide i chiave dell'account e i dettagli di archiviazione di Azure).

    3. Dopo essere stati aggiunti tutti i file toomerge, fare clic su **OK** toocomplete l'operazione di unione hello.

    4. Consente di aprire file sottoposto a merge Hello in SSMS, in cui è possibile visualizzare e analizzarli, nonché di esportazione è tooan XEL o CSV file o tooa della tabella.

* Hello utilizzare [sincronizzazione applicazione](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) che è stata creata. In esecuzione in Azure e prevede l'utilizzo di Operations Management Suite (OMS) Log Analitica pubblica API toopush SQL i log di controllo in OMS. applicazione di sincronizzazione Hello indirizza i log di controllo SQL nel Analitica di Log di OMS per l'utilizzo tramite il dashboard di OMS Log Analitica hello. 

* Usare Power BI. È possibile visualizzare e analizzare i dati dei log di controllo in Power BI. Per altre informazioni, vedere il post di blog su [Power BI e l'accesso a un modello scaricabile](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).

* Scaricare i file di log dal contenitore blob di archiviazione di Azure tramite il portale di hello o tramite uno strumento come [Azure Storage Explorer](http://storageexplorer.com/).
    * Dopo avere scaricato un file di log in locale, è possibile fare doppio clic su tooopen file hello, visualizzare e analizzare i log di hello in SSMS.
    * È anche possibile scaricare più file contemporaneamente tramite Azure Storage Explorer. Fare doppio clic su una sottocartella specifica (ad esempio, una sottocartella che include tutti i file di log per una data specifica) e selezionare **salvare come** toosave in una cartella locale.

* Altri metodi:
   * Dopo aver scaricato diversi file (o una sottocartella che include i file di log per un giorno intero, come descritto nella precedente hello in questo elenco), è possibile unirli in locale come descritto nelle istruzioni di file di controllo Merge SQL Server Management Studio hello descritte in precedenza.

   * Visualizzare i log del controllo BLOB a livello di codice:

     * Hello utilizzare [lettore di eventi estesi](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) libreria c#.
     * [Eseguire query sui file di eventi estesi](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) con PowerShell.




## <a id="subheading-5"></a>Procedure nell'ambiente di produzione
<!--hello description in this section refers toopreceding screen captures.-->

### <a id="subheading-6">Controllo dei database con replica geografica</a>
Quando si utilizzano il database di replica geografica, è possibile tooset il controllo sul database primario hello, database secondario hello o entrambi, in base al tipo di controllo hello.

Seguire queste istruzioni (tenere presente che il servizio controllo blob può essere attivato o disattivata solo dal database primario di hello le impostazioni di controllo):

* **Database primario**. Attivare il controllo di blob, nel server di hello o per hello database, come descritto in hello [impostare il controllo per il database](#subheading-2) sezione.
* **Database secondario**. Attivare il controllo di blob nel database primario hello, come descritto in hello [impostare il controllo per il database](#subheading-2) sezione. 
   * BLOB deve essere abilitato il controllo su hello *database primario stesso*, non il server hello.
   * Dopo che il servizio controllo blob è abilitato sul database primario hello, anche diventare abilitato nel database secondario hello.

     >[!IMPORTANT]
     >Per impostazione predefinita, le impostazioni di archiviazione hello per database secondario hello sarà toothose identici del database primario hello, causando il traffico tra internazionali. È possibile evitare questo problema abilitando il servizio controllo blob nel server secondario hello e configurazione dell'archiviazione locale nelle impostazioni di archiviazione di hello server secondario. Questo percorso sostituirà il percorso di archiviazione hello per database secondario hello e il risultato in ogni database in cui salvare l'archiviazione toolocal i registri di controllo.  
<br>

### <a id="subheading-6">Rigenerazione delle chiavi di archiviazione</a>
Nell'ambiente di produzione, si è probabilmente toorefresh lo spazio di archiviazione chiavi periodicamente. Durante l'aggiornamento delle chiavi, è necessario il criterio di controllo hello tooresave. il processo di Hello è come segue:

1. Aprire hello **dettagli archiviazione** blade. In hello **chiave di accesso di archiviazione** , quindi selezionare **secondario**, fare clic su **OK**. Quindi fare clic su **salvare** nella parte superiore di hello di hello controllo pannello di configurazione.

    ![Riquadro di spostamento][5]
2. Andare a pannello di configurazione di archiviazione toohello e rigenerare la chiave di accesso primaria hello.

    ![Riquadro di spostamento][6]
3. Tornare indietro toohello Pannello di configurazione di controllo, passare hello archiviazione chiave di accesso secondario tooprimary e quindi fare clic su **OK**. Quindi fare clic su **salvare** nella parte superiore di hello di hello controllo pannello di configurazione.
4. Tornare al pannello di configurazione di archiviazione toohello e chiave di accesso secondaria hello rigenerare (in preparazione per il ciclo di aggiornamento della chiave di hello Avanti).

## <a id="subheading-7"></a>Automazione (API REST/PowerShell)
È inoltre possibile configurare il controllo nel Database di SQL Azure utilizzando i seguenti strumenti di automazione hello:

* **Cmdlet di PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

   Per un esempio di script, vedere [Configurare il controllo del database SQL e il rilevamento delle minacce usando PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

* **API REST per il controllo BLOB**:

   * [Creare o aggiornare i criteri controllo BLOB del database](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [Creare o aggiornare i criteri controllo BLOB del server](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [Ottenere i criteri controllo BLOB del database](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [Ottenere i criteri controllo BLOB del server](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [Ottenere il risultato dell'operazione di controllo BLOB del server](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
