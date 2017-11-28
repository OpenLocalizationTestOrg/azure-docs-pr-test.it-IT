
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, the following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through the new Azure portal
-->


1. <span data-ttu-id="0b553-101">Accedere al [portale di Azure](https://portal.azure.com/) all'indirizzo http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="0b553-101">Log in to the [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="0b553-102">Nell'intestazione di sinistra, fare clic su **ESPLORA TUTTO**.</span><span class="sxs-lookup"><span data-stu-id="0b553-102">In the left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="0b553-103">Il pannello **Sfoglia** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="0b553-103">The **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="0b553-104">Scorrere e fare clic su **Server SQL**.</span><span class="sxs-lookup"><span data-stu-id="0b553-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="0b553-105">Il pannello **istanze di SQL Server** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="0b553-105">The **SQL servers** blade is displayed.</span></span>
   
    ![Trovare il server di Database SQL di Azure nel portale di][b21-FindServerInPortal]
4. <span data-ttu-id="0b553-107">Per praticità, ridurre a icona i pannelli precedenti nel pannello **Sfoglia** .</span><span class="sxs-lookup"><span data-stu-id="0b553-107">For convenience, click the minimize control on the earlier **Browse** blade.</span></span>
5. <span data-ttu-id="0b553-108">Nella casella di testo di filtro, iniziare a digitare il nome del server.</span><span class="sxs-lookup"><span data-stu-id="0b553-108">In the filter text box, start typing the name of your server.</span></span> <span data-ttu-id="0b553-109">Viene visualizzata la riga.</span><span class="sxs-lookup"><span data-stu-id="0b553-109">Your row is displayed.</span></span>
6. <span data-ttu-id="0b553-110">Fare clic sulla riga per il server.</span><span class="sxs-lookup"><span data-stu-id="0b553-110">Click the row for your server.</span></span> <span data-ttu-id="0b553-111">Viene visualizzato un pannello per il server.</span><span class="sxs-lookup"><span data-stu-id="0b553-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="0b553-112">Nel pannello del server, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0b553-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="0b553-113">Il pannello **impostazioni** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="0b553-113">The **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="0b553-114">Fare clic su **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="0b553-114">Click **Firewall**.</span></span> <span data-ttu-id="0b553-115">Il pannello **Impostazioni del Firewall** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="0b553-115">The **Firewall Settings** blade is displayed.</span></span>
   
    ![Fare clic su Impostazioni > Firewall][b31-SettingsFirewallNavig]
9. <span data-ttu-id="0b553-117">Fare clic su **aggiungere Client IP**.</span><span class="sxs-lookup"><span data-stu-id="0b553-117">Click **Add Client IP**.</span></span> <span data-ttu-id="0b553-118">Digitare un nome per la nuova regola nella prima casella di testo.</span><span class="sxs-lookup"><span data-stu-id="0b553-118">Type in a name for your new rule into the first text box.</span></span>
10. <span data-ttu-id="0b553-119">Digitare i valori di indirizzo IP minimo e massimo per l'intervallo che si desidera abilitare.</span><span class="sxs-lookup"><span data-stu-id="0b553-119">Type in the low and high IP address values for the range you want to enable.</span></span>
    
    * <span data-ttu-id="0b553-120">Può essere utile impostare il valore minimo su **.0** e il massimo su **.255**.</span><span class="sxs-lookup"><span data-stu-id="0b553-120">It can be handy to have the low value end with **.0** and the high with **.255**.</span></span>
    
    ![Aggiungere un intervallo di indirizzi IP per consentire][b41-AddRange]
11. <span data-ttu-id="0b553-122">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="0b553-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
