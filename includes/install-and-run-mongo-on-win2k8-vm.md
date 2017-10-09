<span data-ttu-id="4ab04-101">Seguire questi passaggi tooinstall ed eseguire MongoDB in una macchina virtuale che esegue Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4ab04-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ab04-102">Le funzionalità di sicurezza MongoDB, ad esempio l'autenticazione e l'associazione di indirizzi IP, non sono abilitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4ab04-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="4ab04-103">Funzionalità di sicurezza devono essere abilitate prima di distribuire l'ambiente di produzione tooa MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4ab04-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="4ab04-104">Per altre informazioni, vedere [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication)Sicurezza e autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4ab04-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="4ab04-105">Dopo aver collegato toohello virtual machine tramite Desktop remoto, aprire Internet Explorer da hello **avviare** menu nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="4ab04-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="4ab04-106">Seleziona hello **strumenti** pulsante nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="4ab04-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="4ab04-107">In **Opzioni Internet**selezionare hello **sicurezza** scheda e quindi selezionare hello **siti attendibili** icona e infine fare clic su hello **siti** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4ab04-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="4ab04-108">Aggiungere *https://\*. mongodb.org* toohello elenco dei siti attendibili.</span><span class="sxs-lookup"><span data-stu-id="4ab04-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="4ab04-109">Andare troppo[Scarica - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="4ab04-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="4ab04-110">Trovare hello **versione stabile corrente** di **Server Community**selezionare hello più recente **64-bit** versione nella colonna di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4ab04-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="4ab04-111">Scaricare, quindi eseguire il programma di installazione di hello MSI.</span><span class="sxs-lookup"><span data-stu-id="4ab04-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="4ab04-112">MongoDB viene in genere installato in C:\Programmi\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4ab04-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="4ab04-113">Cercare le variabili di ambiente nel desktop hello e aggiungere il componente toohello percorso variabile del percorso dei file binari hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4ab04-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="4ab04-114">Ad esempio, si potrebbero individuare i file binari di hello in c:\Programmi\Microsoft Files\MongoDB\Server\3.4\bin nel computer.</span><span class="sxs-lookup"><span data-stu-id="4ab04-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="4ab04-115">Creare le directory di dati e di log di MongoDB nel disco dati hello (ad esempio unità **f:**) è stato creato in hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="4ab04-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="4ab04-116">Da **avviare**selezionare **prompt dei comandi** tooopen una finestra del prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4ab04-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="4ab04-117">Digitare:</span><span class="sxs-lookup"><span data-stu-id="4ab04-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="4ab04-118">database hello toorun, eseguire:</span><span class="sxs-lookup"><span data-stu-id="4ab04-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="4ab04-119">Tutti i messaggi di log sono diretto toohello *F:\MongoLogs\mongolog.log* file mongod.exe server viene avviato e prealloca una quantità file journal.</span><span class="sxs-lookup"><span data-stu-id="4ab04-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="4ab04-120">Può richiedere alcuni minuti per MongoDB toopreallocate file journal hello e avvia l'ascolto delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="4ab04-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="4ab04-121">prompt dei comandi di Hello rimane attivo per l'attività mentre è in esecuzione l'istanza di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4ab04-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="4ab04-122">hello toostart shell amministrativa MongoDB, aprire un'altra finestra di comando da **avviare** e hello tipo seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="4ab04-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="4ab04-123">Hello database viene creato da insert hello.</span><span class="sxs-lookup"><span data-stu-id="4ab04-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="4ab04-124">In alternativa, è possibile installare mongod.exe come servizio:</span><span class="sxs-lookup"><span data-stu-id="4ab04-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="4ab04-125">Viene installato un servizio denominato MongoDB con la descrizione "MongoDB".</span><span class="sxs-lookup"><span data-stu-id="4ab04-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="4ab04-126">Hello `--logpath` opzione deve essere toospecify utilizzato un file di log, poiché hello servizio non dispone di un output toodisplay finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="4ab04-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="4ab04-127">Hello `--logappend` opzione specifica che un riavvio del servizio hello provoca output tooappend toohello file di log esistente.</span><span class="sxs-lookup"><span data-stu-id="4ab04-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="4ab04-128">Hello `--dbpath` opzione specifica hello percorso della directory di dati hello.</span><span class="sxs-lookup"><span data-stu-id="4ab04-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="4ab04-129">Per altre opzioni della riga di comando relative ai servizi, vedere le [opzioni della riga di comando relative ai servizi][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="4ab04-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="4ab04-130">servizio hello toostart, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4ab04-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="4ab04-131">Ora che MongoDB sia installato e in esecuzione, è necessario tooopen una porta in Windows Firewall in modo è possibile connettersi in remoto tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="4ab04-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="4ab04-132">Da hello **avviare** dal menu **strumenti di amministrazione** e quindi **Windows Firewall con sicurezza avanzata**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="4ab04-133">a) nel riquadro sinistro hello selezionare **regole connessioni in entrata**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="4ab04-134">In hello **azioni** riquadro a destra, hello seleziona **nuova regola...** .</span><span class="sxs-lookup"><span data-stu-id="4ab04-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Windows Firewall][Image1]

    <span data-ttu-id="4ab04-136">b) in hello **in ingresso Creazione guidata nuova regola**selezionare **porta** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows Firewall][Image2]

    <span data-ttu-id="4ab04-138">c) Selezionare **TCP** e quindi **Porte locali specifiche**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="4ab04-139">Specificare una porta di "27017" (porta predefinita hello MongoDB in ascolto) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows Firewall][Image3]

    <span data-ttu-id="4ab04-141">d) selezionare **Consenti connessione hello** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Windows Firewall][Image4]

    <span data-ttu-id="4ab04-143">e) Fare di nuovo clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-143">e) Click **Next** again.</span></span>

    ![Windows Firewall][Image5]

    <span data-ttu-id="4ab04-145">f) consente di specificare un nome per la regola di hello, ad esempio "MongoPort", quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows Firewall][Image6]

12. <span data-ttu-id="4ab04-147">Se un endpoint non è stata configurata per MongoDB al momento della creazione macchina virtuale hello, è possibile farlo ora.</span><span class="sxs-lookup"><span data-stu-id="4ab04-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="4ab04-148">È necessario regola del firewall hello sia hello endpoint toobe tooconnect in grado di tooMongoDB in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="4ab04-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="4ab04-149">Nel portale di Azure hello, fare clic su **macchine virtuali (classico)**, fare clic sul nome della nuova macchina virtuale hello e quindi fare clic su **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Endpoint][Image7]

13. <span data-ttu-id="4ab04-151">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4ab04-151">Click **Add**.</span></span>

14. <span data-ttu-id="4ab04-152">Aggiungere un endpoint con nome "Mongo", protocollo **TCP**ed entrambi **pubblica** e **privata** porte set troppo "27017".</span><span class="sxs-lookup"><span data-stu-id="4ab04-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="4ab04-153">Apertura di questa porta consente toobe MongoDB accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="4ab04-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Endpoint][Image9]

> [!NOTE]
> <span data-ttu-id="4ab04-155">porta Hello 27017 è utilizzata da MongoDB la porta predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="4ab04-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="4ab04-156">È possibile modificare la porta predefinita specificando hello `--port` parametro durante l'avvio hello mongod.exe server.</span><span class="sxs-lookup"><span data-stu-id="4ab04-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="4ab04-157">Rendere toogive che hello stesso numero di porta nel firewall hello e hello l'endpoint "Mongo" hello istruzioni precedente.</span><span class="sxs-lookup"><span data-stu-id="4ab04-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
