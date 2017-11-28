
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, the following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="e5e21-101">Creare una regola del firewall a livello di server nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e5e21-101">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="e5e21-102">Nel pannello di SQL Server, in Impostazioni, fare clic su **Firewall** per aprire il pannello del firewall per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e5e21-102">On the SQL server blade, under Settings, click **Firewall** to open the Firewall blade for the SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="e5e21-103">Verificare la presenza dell'indirizzo IP del client e che questo sia l'indirizzo IP Internet che usa un browser di propria scelta (chiedere "qual è l'indirizzo IP in uso").</span><span class="sxs-lookup"><span data-stu-id="e5e21-103">Review the client IP address displayed and validate that this is your IP address on the Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="e5e21-104">Talvolta non corrispondono per varie ragioni.</span><span class="sxs-lookup"><span data-stu-id="e5e21-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="e5e21-105">Supponendo che gli indirizzi IP corrispondano, fare clic su **Aggiungi IP client** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="e5e21-105">Assuming that the IP addresses match, click **Add client IP** on the toolbar.</span></span>

    ![Aggiungi IP client](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="e5e21-107">È possibile aprire il firewall del database SQL nel server a un singolo indirizzo IP o a un intero intervallo di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="e5e21-107">You can open the SQL Database firewall on the server to a single IP address or an entire range of addresses.</span></span> <span data-ttu-id="e5e21-108">L'apertura del firewall consente agli amministratori SQL e agli utenti di accedere a qualsiasi database nel server per cui hanno credenziali valide.</span><span class="sxs-lookup"><span data-stu-id="e5e21-108">Opening the firewall enables SQL administrators and users to login to any database on the server to which they have valid credentials.</span></span>
    >

4. <span data-ttu-id="e5e21-109">Fare clic su **Salva** sulla barra degli strumenti per salvare questa regola del firewall a livello di server e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5e21-109">Click **Save** on the toolbar to save this server-level firewall rule and then click **OK**.</span></span>

    ![Aggiungi IP client](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="e5e21-111">Per un'esercitazione, vedere [Esercitazione sul database SQL: creare un server, una regola del firewall a livello di server, un database di esempio, una regola del firewall a livello di database ed eseguire la connessione ad SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e5e21-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
