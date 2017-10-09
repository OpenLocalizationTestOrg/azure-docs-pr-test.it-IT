
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Creare una regola del firewall a livello di server nel portale di Azure hello

1. Nel Pannello di server SQL hello, in impostazioni, fare clic su **Firewall** tooopen hello Firewall pannello server SQL hello.

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. Esaminare l'indirizzo IP del client hello visualizzata e confermare che questo è l'indirizzo IP in Internet tramite un browser qualsiasi hello (chiedere "che cos'è l'indirizzo IP). Talvolta non corrispondono per varie ragioni.

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. Supponendo che gli indirizzi IP hello corrispondono, fare clic su **Aggiungi indirizzo IP del client** sulla barra degli strumenti hello.

    ![Aggiungi IP client](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > È possibile aprire il firewall di Database di SQL hello in hello server tooa unico indirizzo IP o un intero intervallo di indirizzi. Apertura hello firewall consente agli amministratori SQL e gli utenti toologin tooany database hello toowhich server hanno credenziali valide.
    >

4. Fare clic su **salvare** hello toosave barra degli strumenti la regola del firewall a livello di server e quindi fare clic su **OK**.

    ![Aggiungi IP client](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> Per un'esercitazione, vedere [Esercitazione sul database SQL: creare un server, una regola del firewall a livello di server, un database di esempio, una regola del firewall a livello di database ed eseguire la connessione ad SQL Server](../articles/sql-database/sql-database-get-started.md).    
>
