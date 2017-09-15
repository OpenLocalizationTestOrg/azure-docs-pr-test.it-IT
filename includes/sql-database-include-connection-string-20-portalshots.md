
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="eeceb-101">Ottenere la stringa di connessione dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eeceb-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="eeceb-102">Usare il [portale di Azure](https://portal.azure.com/) per ottenere la stringa di connessione necessaria al programma client per interagire con il database SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="eeceb-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span> 

1. <span data-ttu-id="eeceb-103">Fare clic su **ESPLORA** > **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="eeceb-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="eeceb-104">Immettere il nome del database nella casella di testo filtro vicino alla parte superiore sinistra del pannello **Database SQL** .</span><span class="sxs-lookup"><span data-stu-id="eeceb-104">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
3. <span data-ttu-id="eeceb-105">Fare clic sulla riga per il database.</span><span class="sxs-lookup"><span data-stu-id="eeceb-105">Click the row for your database.</span></span>
4. <span data-ttu-id="eeceb-106">Quando viene visualizzato il pannello del database, è possibile scegliere i controlli di riduzione a icona standard per comprimere i pannelli usati per la ricerca e il filtro del database per una visualizzazione più chiara.</span><span class="sxs-lookup"><span data-stu-id="eeceb-106">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span> 
   
    ![Filtro per isolare il database][10-FilterDatabase]
5. <span data-ttu-id="eeceb-108">Nel pannello del database, fare clic su **Mostra stringhe di connessione di database**.</span><span class="sxs-lookup"><span data-stu-id="eeceb-108">On the blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="eeceb-109">Se si prevede di utilizzare la libreria di connessione ADO.NET, copiare la stringa di etichetta **ADO**.</span><span class="sxs-lookup"><span data-stu-id="eeceb-109">If you intend to use the ADO.NET connection library, copy the string labeled **ADO**.</span></span> 
   
    ![Copiare la stringa di connessione ADO per il database][20-CopyAdoConnectionString]
7. <span data-ttu-id="eeceb-111">In un formato o un altro, incollare le informazioni sulla stringa di connessione nel codice del programma client.</span><span class="sxs-lookup"><span data-stu-id="eeceb-111">In one format or another, paste the connection string information into your client program code.</span></span>

<span data-ttu-id="eeceb-112">Per altre informazioni, vedere il blog sul </span><span class="sxs-lookup"><span data-stu-id="eeceb-112">For more information, see:</span></span><br/><span data-ttu-id="eeceb-113">[Stringhe di connessione e file di configurazione](http://msdn.microsoft.com/library/ms254494.aspx).</span><span class="sxs-lookup"><span data-stu-id="eeceb-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
