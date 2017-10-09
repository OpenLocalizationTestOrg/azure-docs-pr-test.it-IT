
1. <span data-ttu-id="df45f-101">privilegi tooescalate, tipo:</span><span class="sxs-lookup"><span data-stu-id="df45f-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="df45f-102">Immettere la password.</span><span class="sxs-lookup"><span data-stu-id="df45f-102">Enter your password.</span></span>
2. <span data-ttu-id="df45f-103">tooinstall Server di MySQL Community edition, digitare:</span><span class="sxs-lookup"><span data-stu-id="df45f-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="df45f-104">Attendere fino al termine del download e dell'installazione di MySQL.</span><span class="sxs-lookup"><span data-stu-id="df45f-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="df45f-105">tooset MySQL toostart sistema hello all'avvio, digitare:</span><span class="sxs-lookup"><span data-stu-id="df45f-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="df45f-106">Avviare manualmente il daemon di MySQL hello (mysqld) con questo comando:</span><span class="sxs-lookup"><span data-stu-id="df45f-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="df45f-107">stato hello toocheck di hello daemon MySQL, digitare:</span><span class="sxs-lookup"><span data-stu-id="df45f-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="df45f-108">hello toostop daemon MySQL, digitare:</span><span class="sxs-lookup"><span data-stu-id="df45f-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="df45f-109">Dopo l'installazione, la password radice di MySQL hello è vuota per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="df45f-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="df45f-110">È consigliabile eseguire **mysql\_secure\_installation**, uno script per la protezione di MySQL.</span><span class="sxs-lookup"><span data-stu-id="df45f-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="df45f-111">script Hello richiede la password radice di MySQL hello toochange, rimuovere gli account utente anonimo, disabilitare gli account di accesso remoto radice, rimuovere i database di test e ricaricare tabella privilegi hello.</span><span class="sxs-lookup"><span data-stu-id="df45f-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="df45f-112">È consigliabile rispondere Sì tooall di queste opzioni e modificare la password radice hello.</span><span class="sxs-lookup"><span data-stu-id="df45f-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="df45f-113">Digitare lo script hello toorun script di installazione di MySQL:</span><span class="sxs-lookup"><span data-stu-id="df45f-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="df45f-114">Accedi tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="df45f-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="df45f-115">Immettere la password radice hello MySQL (che è stato modificato nel passaggio precedente hello) e verrà visualizzata con un prompt dei comandi in cui è possibile emettere toointeract istruzioni SQL con database hello.</span><span class="sxs-lookup"><span data-stu-id="df45f-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="df45f-116">toocreate un nuovo utente di MySQL, eseguire il seguente hello hello **mysql >** prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="df45f-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="df45f-117">Si noti che i punti e virgola di hello (;) alla fine hello hello sono fondamentali per la chiusura di comandi hello righe.</span><span class="sxs-lookup"><span data-stu-id="df45f-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="df45f-118">toocreate hello un database e concedere `mysqluser` autorizzazioni su di esso, hello problema seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="df45f-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="df45f-119">Si noti che i nomi di database utente e password vengono utilizzate solo per gli script di connessione database toohello.</span><span class="sxs-lookup"><span data-stu-id="df45f-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="df45f-120">I nomi di account utente di database non rappresentano necessariamente gli account utente effettivo nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="df45f-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="df45f-121">toolog in da un altro computer, digitare:</span><span class="sxs-lookup"><span data-stu-id="df45f-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="df45f-122">dove `ip-address` è hello l'indirizzo IP del computer di hello da cui verrà effettuata la connessione tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="df45f-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="df45f-123">hello tooexit utilità di amministrazione di database MySQL, digitare:</span><span class="sxs-lookup"><span data-stu-id="df45f-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="df45f-124">Aggiungere un endpoint</span><span class="sxs-lookup"><span data-stu-id="df45f-124">Add an endpoint</span></span>
1. <span data-ttu-id="df45f-125">Dopo l'installazione di MySQL, è necessario in modalità remota tooconfigure un tooaccess endpoint MySQL.</span><span class="sxs-lookup"><span data-stu-id="df45f-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="df45f-126">Accedi toohello [portale di Azure classico][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="df45f-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="df45f-127">Fare clic su **macchine virtuali**, fare clic sul nome della nuova macchina virtuale hello e quindi fare clic su **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="df45f-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="df45f-128">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="df45f-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="df45f-129">Aggiungere un endpoint denominato "MySQL" con protocollo **TCP**, e **pubblica** e **privata** porte set troppo "3306".</span><span class="sxs-lookup"><span data-stu-id="df45f-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="df45f-130">tooremotely connessione macchina virtuale toohello dal computer, tipo:</span><span class="sxs-lookup"><span data-stu-id="df45f-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="df45f-131">Ad esempio, utilizza una macchina virtuale hello che è create in questa esercitazione, digitare questo comando:</span><span class="sxs-lookup"><span data-stu-id="df45f-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
