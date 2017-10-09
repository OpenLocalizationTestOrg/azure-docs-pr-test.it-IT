## <a name="log-in-toohello-azure-portal"></a>Accedi toohello portale di Azure

Accedi toohello [portale di Azure](https://portal.azure.com/).

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a>Creare un database SQL vuoto utilizzando hello portale di Azure

Un database SQL di Azure viene creato con un set definito di [risorse di calcolo e di archiviazione](../articles/sql-database/sql-database-service-tiers.md). Hello database viene creato all'interno di un [gruppo di risorse](../articles/azure-resource-manager/resource-group-overview.md) e in un [server logico di Database SQL di Azure](../articles/sql-database/sql-database-features.md). 

Seguire questi toocreate passaggi un database SQL vuoto. 

1. Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.

2. Selezionare **database** da hello **New** pagina e selezionare **Database SQL** da hello **database** pagina. 

   ![creare database vuoto](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Compilare il modulo di Database SQL hello con hello le seguenti informazioni, come mostrato nella precedente immagine hello:   

   | Impostazione | Valore consigliato | Descrizione |
   | --------| --------------- | ----------- | 
   | **Database name** (Nome database) | mySampleDatabase | Per i nomi di database validi, vedere [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificatori di database). | 
   | **Sottoscrizione** | Sottoscrizione in uso  | Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni). |
   | **Gruppo di risorse** | myResourceGroup | Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni). |
   | **Select source** (Seleziona origine) | Database vuoto | Indica che deve essere creato un database vuoto. |
   ||||

4. Fare clic su **Server** toocreate e configurare un nuovo server per il nuovo database. Compilare hello **nuovo modulo server** con hello le seguenti informazioni: 

   | Impostazione | Valore consigliato | Descrizione |
   | --------| --------------- | ----------- | 
   | **Server name** (Nome server) | Qualsiasi nome univoco globale. | Per i nomi di server validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni). | 
   | **Nome di accesso amministratore server** | Qualsiasi nome valido. | Per i nomi di accesso validi, vedere [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificatori di database).|
   | **Password** | Qualsiasi password valida. | La password deve contenere almeno otto caratteri e deve contenere caratteri di tre delle seguenti categorie di hello: lettere maiuscole, lettere minuscole, numeri e caratteri non alfanumerici. |
   | **Posizione** | Qualsiasi posizione valida. | Per informazioni sulle aree, vedere [Aree di Azure](https://azure.microsoft.com/regions/). |
   ||||

   ![Creare il server di database](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. Fare clic su **Seleziona**.

6. Fare clic su **tariffario** toospecify hello servizio livello di prestazioni e per il nuovo database. Per esercitazione selezionare **20 DTU** e **250** GB di memoria.

   ![Creare il database s1](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Fare clic su **Apply**.  

8. Selezionare un **delle regole di confronto** per database vuoto di hello (per questa esercitazione, hello Usa il valore predefinito). Per altre informazioni sulle regole di confronto, vedere [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations) (Regole di confronto)

9. Fare clic su **crea** database hello tooprovision. Provisioning richiede circa un minuto e mezzo di toocomplete. 

10. Sulla barra degli strumenti hello, fare clic su **notifiche** toomonitor processo di distribuzione hello.

   ![notifica](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a>Creare una regola firewall di livello server tramite hello portale di Azure

Hello servizio Database SQL consente di creare un firewall a livello di server hello. Inizialmente hello firewall impedisce il strumenti esterni e le applicazioni si connettano toohello server o database tooany hello server. Dopo aver creata una regola del firewall tooopen specifici indirizzi IP, sono consentite connessioni. Seguire questi passaggi toocreate un [regola del firewall a livello di server SQL Database](../articles/sql-database/sql-database-firewall-configure.md) per l'indirizzo IP del client e tooenable connettività esterna tramite firewall del Database SQL hello per solo l'indirizzo IP. 


> [!NOTE]
> Il database SQL di Azure comunica sulla porta 1433. È possibile connettersi tooSQL Database solo dopo che il firewall di hello della rete consenta il traffico in uscita attraverso la porta 1433.


1. Al termine della distribuzione di hello, fare clic su **database SQL** dal menu a sinistra di hello e quindi fare clic su **mySampleDatabase** su hello **database SQL** pagina. pagina di panoramica per l'apertura del database, che mostra hello completamente Hello completo del server (ad esempio **mynewserver20170313.database.windows.net**) e offre opzioni per un'ulteriore configurazione. Copiare il nome completo del server per usarlo in seguito.

   > [!IMPORTANT]
   > È necessario il server di tooyour tooconnect nome completo del server e i relativi database nelle successive guide introduttive.
   > 

   ![Nome del server](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. Fare clic su **impostare firewall server** sulla barra degli strumenti hello, come illustrato nella figura precedente hello. Hello **le impostazioni del Firewall** verrà visualizzata la pagina per il server di Database SQL di hello. 

   ![Regola del firewall del server](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Fare clic su **Aggiungi indirizzo IP del client** su hello barra degli strumenti tooadd il corrente l'indirizzo IP di tooa nuova regola del firewall. Una regola del firewall può aprire la porta 1433 per un indirizzo IP singolo o un intervallo di indirizzi IP.

4. Fare clic su **Salva**. Una regola del firewall a livello di server viene creata per l'indirizzo IP corrente, aprire la porta 1433 sul server logico hello.

   ![Impostare la regola del firewall del server](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Fare clic su **OK** e quindi chiudere hello **le impostazioni del Firewall** pagina.

È ora possibile connettersi toohello server di Database SQL di Azure e i relativi database tramite uno strumento, ad esempio SQL Server Management Studio (SSMS). connessione Hello è da questo indirizzo IP e viene utilizzato l'account amministratore di server hello creato in precedenza.


> [!IMPORTANT]
> Per impostazione predefinita, l'accesso attraverso il firewall di Database SQL hello è abilitato per tutti i servizi di Azure. Fare clic su **OFF** su toodisable questa pagina per tutti i servizi di Azure.


## <a name="get-connection-string-values-using-hello-azure-portal"></a>Ottenere i valori di stringa di connessione utilizzando hello portale di Azure

Ottenere hello nome completo del server per il server di Database SQL di Azure nel portale di Azure hello. Utilizzare hello server completo tooconnect tooyour server dei nomi utilizzando SQL Server Management Studio.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).

2. Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina. 

3. In hello **Essentials** riquadro hello pagina del portale Azure per il database, individuare e copiare hello **nome Server**.

   ![informazioni di connessione](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
