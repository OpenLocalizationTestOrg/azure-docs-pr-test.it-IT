
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="46246-101">Accedi toohello [portale di Azure](https://portal.azure.com/) in http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="46246-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="46246-102">Nel banner sinistro hello, fare clic su **Esplora tutto**.</span><span class="sxs-lookup"><span data-stu-id="46246-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="46246-103">Hello **Sfoglia** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="46246-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="46246-104">Scorrere e fare clic su **Server SQL**.</span><span class="sxs-lookup"><span data-stu-id="46246-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="46246-105">Hello **istanze di SQL Server** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="46246-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Trovare il server di Database SQL di Azure nel portale di hello][b21-FindServerInPortal]
4. <span data-ttu-id="46246-107">Per praticità, fare clic su hello ridurre al minimo il controllo in precedenza hello **Sfoglia** blade.</span><span class="sxs-lookup"><span data-stu-id="46246-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="46246-108">Nella casella di testo filtro hello, iniziare a digitare il nome di hello del server.</span><span class="sxs-lookup"><span data-stu-id="46246-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="46246-109">Viene visualizzata la riga.</span><span class="sxs-lookup"><span data-stu-id="46246-109">Your row is displayed.</span></span>
6. <span data-ttu-id="46246-110">Fare clic sulla riga hello del server.</span><span class="sxs-lookup"><span data-stu-id="46246-110">Click hello row for your server.</span></span> <span data-ttu-id="46246-111">Viene visualizzato un pannello per il server.</span><span class="sxs-lookup"><span data-stu-id="46246-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="46246-112">Nel pannello del server, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="46246-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="46246-113">Hello **impostazioni** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="46246-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="46246-114">Fare clic su **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="46246-114">Click **Firewall**.</span></span> <span data-ttu-id="46246-115">Hello **le impostazioni del Firewall** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="46246-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Fare clic su Impostazioni > Firewall][b31-SettingsFirewallNavig]
9. <span data-ttu-id="46246-117">Fare clic su **aggiungere Client IP**.</span><span class="sxs-lookup"><span data-stu-id="46246-117">Click **Add Client IP**.</span></span> <span data-ttu-id="46246-118">Digitare un nome per la nuova regola nella prima casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="46246-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="46246-119">Tipo di hello basso e alto valori di intervallo hello desiderato di indirizzi IP tooenable.</span><span class="sxs-lookup"><span data-stu-id="46246-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="46246-120">Può essere utile toohave hello basso valore fine con **,0** e alta con hello **.255**.</span><span class="sxs-lookup"><span data-stu-id="46246-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Aggiungere un tooallow intervallo di indirizzi IP][b41-AddRange]
11. <span data-ttu-id="46246-122">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="46246-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
