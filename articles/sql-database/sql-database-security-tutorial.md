---
title: aaaSecure il database SQL di Azure | Documenti Microsoft
description: "Informazioni sulle tecniche e funzionalità toosecure del database SQL di Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>Proteggere il database SQL di Azure

Database SQL protegge i dati tramite la limitazione di database di access tooyour utilizzando le regole firewall, richiedere agli utenti tooprove loro identità e autorizzazione toodata tramite appartenenza basata su ruoli e autorizzazioni, nonché tramite i meccanismi di autenticazione la sicurezza a livello di riga e la maschera dati dinamica.

È possibile migliorare la protezione hello del database rispetto a utenti malintenzionati o di accesso non autorizzato con pochi semplici passaggi. In questa esercitazione si apprenderà come: 

> [!div class="checklist"]
> * Impostare le regole firewall di livello server per il server in hello portale di Azure
> * Configurare regole del firewall a livello di database per il database con SQL Server Management Studio
> * La connessione a database tooyour utilizzando una stringa di connessione protetta
> * Gestire l'accesso utente
> * Proteggere i dati con la crittografia
> * Abilitare il controllo del database SQL
> * Abilitare il rilevamento delle minacce per il database SQL

Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, verificare che si dispone hello seguenti:

- Versione più recente di hello installato di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). 
- Installato Microsoft Excel.
- Creato un server SQL di Azure e un database, vedere [creare un database SQL di Azure nel portale di Azure hello](sql-database-get-started-portal.md), [creare un singolo database di SQL Azure mediante Azure CLI hello](sql-database-get-started-cli.md), e [creare un singolo SQL Azure database con PowerShell](sql-database-get-started-powershell.md). 

## <a name="log-in-toohello-azure-portal"></a>Accedi toohello portale di Azure

Accedi toohello [portale di Azure](https://portal.azure.com/).

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Creare una regola del firewall a livello di server nel portale di Azure hello

I database SQL sono protetti da un firewall in Azure. Per impostazione predefinita, tutte le connessioni toohello database e server hello all'interno di server hello vengono rifiutati, ad eccezione delle connessioni da altri servizi di Azure. Per altre informazioni, vedere [Regole firewall a livello di server e di database per il database SQL di Azure](sql-database-firewall-configure.md).

la configurazione più sicura di Hello è tooset 'Consenti l'accesso tooAzure servizi' tooOFF. Se è necessario tooconnect toohello database da un macchina virtuale di Azure o un servizio cloud, è necessario creare un [IP riservato](../virtual-network/virtual-networks-reserved-public-ip.md) e consente solo hello riservato IP indirizzo l'accesso attraverso il firewall hello. 

Seguire questi passaggi toocreate un [regola del firewall a livello di server SQL Database](sql-database-firewall-configure.md) per le connessioni tooallow server da un indirizzo IP specifico. 

> [!NOTE]
> Se è stato creato un database di esempio in Azure utilizzando una delle esercitazioni precedenti hello o Guide rapide e sono l'esecuzione di questa esercitazione su un computer con hello stesso indirizzo IP che si trovava al momento è esaminato in dettaglio le esercitazioni, è possibile ignorare questo passaggio poiché sarà necessario già creato una regola del firewall a livello di server.
>

1. Fare clic su **database SQL** dal database hello dal menu a sinistra hello desideri tooconfigure hello regola firewall per in hello **database SQL** pagina. pagina di panoramica per l'apertura del database, che mostra hello completamente Hello completo del server (ad esempio **mynewserver 20170313.database.windows.net**) e offre opzioni per un'ulteriore configurazione.

      ![Regola del firewall del server](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. Fare clic su **impostare firewall server** sulla barra degli strumenti hello, come illustrato nella figura precedente hello. Hello **le impostazioni del Firewall** verrà visualizzata la pagina per il server di Database SQL di hello. 

3. Fare clic su **Aggiungi indirizzo IP del client** hello barra degli strumenti tooadd hello indirizzo IP pubblico del portale di toohello connesso hello computer con o immettere manualmente regola del firewall hello e quindi fare clic su **salvare**.

      ![Impostare la regola del firewall del server](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. Fare clic su **OK** e quindi fare clic su hello **X** tooclose hello **le impostazioni del Firewall** pagina.

È ora possibile connettersi a database tooany nel server di hello con hello specificato intervallo di indirizzi IP o l'indirizzo IP.

> [!NOTE]
> Il database SQL comunica attraverso la porta 1433. Se si sta tentando di tooconnect da una rete aziendale, può non essere consentito il traffico in uscita sulla porta 1433 dal firewall della rete. In questo caso, non sarà server di Database SQL di Azure in grado di tooconnect tooyour, a meno che il reparto IT consente di aprire la porta 1433.
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>Creare una regola del firewall a livello di database con SQL Server Management Studio

Le regole del firewall a livello di database consentono di impostazioni di firewall diverso toocreate per database diversi all'interno di hello stesso firewall logico di server e toocreate regole che possono essere trasferiti, vale a dire che seguono database hello durante un [failover ](sql-database-geo-replication-overview.md) invece di essere archiviate sul server SQL hello. Le regole del firewall a livello di database possono essere solo configurata utilizzando istruzioni Transact-SQL e solo dopo aver configurato prima regola del firewall di livello server hello. Per altre informazioni, vedere [Regole firewall a livello di server e di database per il database SQL di Azure](sql-database-firewall-configure.md).

Di seguito questi toocreate passaggi una regola del firewall specifico del database.

1. La connessione a database tooyour, ad esempio usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md).

2. In Esplora oggetti fare clic sul database hello da tooadd un firewall della regola e fare clic su **nuova Query**. Query vuota viene visualizzata una finestra che è connesso tooyour database.

3. Nella finestra query hello modificare hello tooyour pubblica indirizzo IP ed eseguire hello seguente query:

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. Sulla barra degli strumenti hello, fare clic su **Execute** regola del firewall toocreate hello.

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>Visualizzare come tooconnect tooyour un'applicazione di database utilizzando una stringa di connessione protetta

tooensure una connessione crittografata protetta tra un'applicazione client e il Database SQL, la stringa di connessione hello è toobe configurato per:

- Richiedere una connessione crittografata, e
- toonot hello un certificato server attendibile. 

Si stabilisce una connessione utilizzando Transport Layer Security (TLS) e si riduce il rischio di hello di attacchi man-in-the-middle. È possibile ottenere stringhe di connessione configurati correttamente per il Database SQL per client supportati i driver da hello portale di Azure come illustrato per ADO.net in questa schermata.

1. Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.

2. In hello **Panoramica** pagina per il database, fare clic su **Mostra le stringhe di connessione di database**.

3. Hello revisione completa **ADO.NET** stringa di connessione.

    ![Stringa di connessione ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>Creazione degli utenti del database

Prima di creare gli utenti, è innanzitutto necessario scegliere uno dei due tipi di autenticazione supportati dal database SQL di Azure: 

**L'autenticazione di SQL**, che utilizza il nome utente e password per gli account di accesso e gli utenti che sono validi solo in hello contesto di un database specifico all'interno di un server logico. 

**Autenticazione di Azure Active Directory**, che usa identità gestite da Azure Active Directory. 

Se si desidera toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate sul Database SQL, deve esistere un popolato Azure Active Directory prima di procedere.

Seguire questi passaggi toocreate un utente tramite l'autenticazione di SQL:

1. La connessione a database tooyour, ad esempio usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md) utilizzando le credenziali di amministratore del server.

2. In Esplora oggetti fare clic sul database hello desiderata tooadd un nuovo utente nella, quindi scegliere **nuova Query**. Query vuota viene visualizzata una finestra che è connesso toohello di database selezionato.

3. Nella finestra query hello immettere hello seguente query:

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. Sulla barra degli strumenti hello, fare clic su **Execute** utente hello toocreate.

5. Per impostazione predefinita, utente hello può connettersi toohello database, ma non dispone di autorizzazioni tooread o scrittura dati. toogrant toohello queste autorizzazioni utente appena creato, eseguire hello seguenti due comandi in una nuova finestra query

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

È migliore toocreate pratica questi account non amministratore in tooyour tooconnect livello di database hello del database a meno che non è necessario tooexecute di attività amministrative quali la creazione di nuovi utenti. Consultare hello [esercitazione di Azure Active Directory](./sql-database-aad-authentication-configure.md) sulla tooauthenticate tramite Azure Active Directory.


## <a name="protect-your-data-with-encryption"></a>Proteggere i dati con la crittografia

Crittografia trasparente dei dati del Database di SQL Azure (TDE) crittografa automaticamente i dati inattivi, senza eventuali modifiche toohello applicazione accesso hello database crittografato. Per i nuovi database creati, la crittografia TDE è attiva per impostazione predefinita. tooenable TDE per il database o tooverify che TDE è attivo, seguire questi passaggi:

1. Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina. 

2. Fare clic su **crittografia dati trasparente** pagina di configurazione di hello tooopen per Transparent Data Encryption.

    ![Transparent Data Encryption](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. Se necessario, impostare **la crittografia dei dati** tooON e fare clic su **salvare**.

il processo di crittografia Hello viene avviato in background hello. È possibile monitorare lo stato di avanzamento hello tramite connessione tooSQL Database [SQL Server Management Studio](./sql-database-connect-query-ssms.md) eseguendo una query sulla colonna encryption_state hello di hello `sys.dm_database_encryption_keys` visualizzazione.

## <a name="enable-sql-database-auditing-if-necessary"></a>Abilitare il controllo del database SQL, se necessario

Controllo del Database SQL Azure tiene traccia degli eventi di database e li scrive i log di controllo tooan nell'account di archiviazione di Azure. Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare potenziali violazioni della sicurezza. Seguire questi toocreate passaggi un criterio di controllo predefinito per il database SQL:

1. Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina. 

2. Nel pannello impostazioni hello, selezionare **controllo e rilevamento minacce**. Si noti che il controllo a livello di server è /bGli e che sia presente un **visualizzare impostazioni del server** collegamento che consente di tooview o modifica le impostazioni controllo hello server da questo contesto.

    ![Pannello di controllo](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. Se si preferisce tooenable un controllo tipo (percorso o?) diverso da hello uno specificato a livello di server hello, attivare **ON** controllo, scegliere hello **Blob** tipo di controllo. Se il servizio controllo Blob server è abilitato, controllo del database configurate hello esisterà in modo affiancato con controllo del Blob hello server.

    ![Attivare il controllo](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. Selezionare **dettagli archiviazione** hello tooopen Pannello di controllo log di archiviazione. Account di archiviazione di Azure selezionare hello in cui verranno salvati i log e il periodo di memorizzazione hello, dopo il quale hello verranno eliminati i log precedenti, quindi fare clic su **OK** nella parte inferiore di hello. 

   > [!TIP]
   > Utilizzare hello stesso account di archiviazione per tutti i hello di tooget database controllati meglio hello controllo modelli di report.
   > 

5. Fare clic su **Salva**.

> [!IMPORTANT]
> Se si desidera che gli eventi controllato hello toocustomize, è possibile farlo tramite PowerShell o l'API REST, vedere hello [automazione (PowerShell / API REST)](sql-database-auditing.md#subheading-7) sezione per ulteriori dettagli.
>

## <a name="enable-sql-database-threat-detection"></a>Abilitare il rilevamento delle minacce per il database SQL

Rilevamento minacce fornisce un nuovo livello di sicurezza, che consente ai clienti toodetect e risposta toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale. Agli utenti di esplorare gli eventi di hello sospette tramite controllo del Database SQL toodetermine se ottenuto tooaccess un tentativo, violazione o sfruttare i dati nel database di hello. Rilevamento minacce rende semplice tooaddress potenziali minacce toohello database di senza necessità di hello toobe un esperto della sicurezza o gestire i sistemi di monitoraggio di sicurezza avanzata.
Ad esempio, la funzionalità di rilevamento delle minacce individua determinate attività anomale nel database che indicano potenziali tentativi di attacco SQL injection. Attacchi SQL injection è uno dei hello Web sicurezza problemi delle applicazioni su Internet, le applicazioni utilizzate tooattack basati sui dati hello. Gli utenti malintenzionati sfruttano applicazione vulnerabilità tooinject dannoso istruzioni SQL in campi di immissione di applicazione, per sugli o la modifica dei dati nel database di hello.

1. Passare a pannello di configurazione toohello di database SQL da toomonitor hello. Nel pannello impostazioni hello, selezionare **controllo e rilevamento minacce**.

    ![Riquadro di spostamento](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. In hello **controllo e rilevamento minacce** configurazione pannello turn **ON** controllo, che visualizza le impostazioni di rilevamento minacce hello.

3. Impostare il rilevamento delle minacce su **SÌ**.

4. Configurare l'elenco di hello di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività del database anomale.

5. Fare clic su **salvare** in hello **rilevamento controllo & minaccia** toosave pannello hello nuovi o aggiornati criteri di rilevamento di controllo e minacce.

    ![Riquadro di spostamento](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    Se vengono rilevate attività anomale del database, si riceverà una notifica tramite posta elettronica. messaggio di posta elettronica Hello verrà fornite informazioni sull'evento sospetti hello inclusi natura hello di attività anomale hello, nome del database, l'ora dell'evento hello nome e il server. Inoltre, verranno fornite informazioni sulle possibili cause e consigliabile tooinvestigate azioni e ridurre database toohello minaccia potenziale di hello. percorso passaggi successiva Hello tramite quali toodo occorre si ricevono un messaggio di posta di questo tipo:

    ![Messaggio di posta elettronica sul rilevamento delle minacce](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. Nel messaggio di posta elettronica di hello, fare clic su hello **Log di controllo di SQL Azure** collegamento, che consente di avviare hello portale di Azure e visualizzare i record di controllo pertinente hello alla ora hello di eventi sospetti hello.

    ![Record di controllo](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. Fare clic su tooview record di controllo hello ulteriori informazioni sulle attività sospette database hello, ad esempio l'istruzione SQL, IP client e motivo di errore.

    ![Dettagli sui record](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. Nel Pannello di controllo Registra hello, fare clic su **Apri in Excel** tooopen preconfigurata che excel tooimport modello e eseguire un'analisi più approfondita del log di controllo hello alla ora hello di eventi sospetti hello.

    > [!NOTE]
    > In Excel 2010 o versioni successive Power Query e hello **combinazione rapida** impostazione è obbligatoria.

    ![Aprire i record in Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. hello tooconfigure **combinazione rapida** impostazione - hello **POWER QUERY** scheda della barra multifunzione selezionare **opzioni** finestra di dialogo Opzioni toodisplay hello. Selezionare hello Privacy sezione e scegliere l'opzione secondo hello - 'Ignora i livelli di Privacy hello e potenziale miglioramento delle prestazioni':

    ![Combinazione rapida di Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. log di controllo SQL tooload, assicurarsi che i parametri di hello nella scheda Impostazioni hello siano impostati correttamente e quindi selezionare barra multifunzione 'Data' hello e fare clic sul pulsante 'Aggiorna tutto' hello.

    ![Parametri di Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. Hello risultati vengono visualizzati in hello **i log di controllo SQL** foglio che consente l'analisi più approfondita di toorun di attività anomale di hello che sono stati rilevati e ridurre l'impatto hello di eventi di protezione hello nell'applicazione.


## <a name="next-steps"></a>Passaggi successivi
È possibile migliorare la protezione hello del database rispetto a utenti malintenzionati o di accesso non autorizzato con pochi semplici passaggi. In questa esercitazione si apprenderà come: 

> [!div class="checklist"]
> * Configurare le regole del firewall per il server e/o il database
> * La connessione a database tooyour utilizzando una stringa di connessione protetta
> * Gestire l'accesso utente
> * Proteggere i dati con la crittografia
> * Abilitare il controllo del database SQL
> * Abilitare il rilevamento delle minacce per il database SQL

> [!div class="nextstepaction"]
>[Migliorare le prestazioni del database SQL](sql-database-performance-tutorial.md)

