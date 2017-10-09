
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="056f8-101">Creare una regola del firewall a livello di server nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="056f8-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="056f8-102">Nel Pannello di server SQL hello, in impostazioni, fare clic su **Firewall** tooopen hello Firewall pannello server SQL hello.</span><span class="sxs-lookup"><span data-stu-id="056f8-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="056f8-103">Esaminare l'indirizzo IP del client hello visualizzata e confermare che questo è l'indirizzo IP in Internet tramite un browser qualsiasi hello (chiedere "che cos'è l'indirizzo IP).</span><span class="sxs-lookup"><span data-stu-id="056f8-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="056f8-104">Talvolta non corrispondono per varie ragioni.</span><span class="sxs-lookup"><span data-stu-id="056f8-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="056f8-105">Supponendo che gli indirizzi IP hello corrispondono, fare clic su **Aggiungi indirizzo IP del client** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="056f8-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![Aggiungi IP client](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="056f8-107">È possibile aprire il firewall di Database di SQL hello in hello server tooa unico indirizzo IP o un intero intervallo di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="056f8-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="056f8-108">Apertura hello firewall consente agli amministratori SQL e gli utenti toologin tooany database hello toowhich server hanno credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="056f8-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="056f8-109">Fare clic su **salvare** hello toosave barra degli strumenti la regola del firewall a livello di server e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="056f8-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![Aggiungi IP client](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="056f8-111">Per un'esercitazione, vedere [Esercitazione sul database SQL: creare un server, una regola del firewall a livello di server, un database di esempio, una regola del firewall a livello di database ed eseguire la connessione ad SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="056f8-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
