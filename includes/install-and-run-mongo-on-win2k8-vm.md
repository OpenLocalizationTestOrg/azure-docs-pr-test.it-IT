<span data-ttu-id="ef774-101">Seguire questa procedura per installare ed eseguire MongoDB in una macchina virtuale che esegue Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ef774-101">Follow these steps to install and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef774-102">Le funzionalità di sicurezza MongoDB, ad esempio l'autenticazione e l'associazione di indirizzi IP, non sono abilitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ef774-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="ef774-103">Dovranno essere abilitate prima di distribuire MongoDB in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ef774-103">Security features should be enabled before deploying MongoDB to a production environment.</span></span>  <span data-ttu-id="ef774-104">Per altre informazioni, vedere [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication)Sicurezza e autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ef774-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="ef774-105">Dopo avere eseguito la connessione alla macchina virtuale tramite Desktop remoto, aprire Internet Explorer dal menu **Start** sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ef774-105">After you've connected to the virtual machine using Remote Desktop, open Internet Explorer from the **Start** menu on the virtual machine.</span></span>
2. <span data-ttu-id="ef774-106">Nell'angolo superiore destro fare clic sul pulsante **Strumenti** .</span><span class="sxs-lookup"><span data-stu-id="ef774-106">Select the **Tools** button in the upper right corner.</span></span>  <span data-ttu-id="ef774-107">In **Opzioni Internet** selezionare la scheda **Sicurezza**, quindi l'icona **Siti attendibili** e infine fare clic sul pulsante **Siti**.</span><span class="sxs-lookup"><span data-stu-id="ef774-107">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon, and finally click the **Sites** button.</span></span> <span data-ttu-id="ef774-108">Aggiungere *https://\*.mongodb.org* all'elenco dei siti attendibili.</span><span class="sxs-lookup"><span data-stu-id="ef774-108">Add *https://\*.mongodb.org* to the list of trusted sites.</span></span>
3. <span data-ttu-id="ef774-109">Passare alla pagina [MongoDB Download Center](https://www.mongodb.com/download-center#community) (Area download di MongoDB).</span><span class="sxs-lookup"><span data-stu-id="ef774-109">Go to [Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="ef774-110">Trovare la **versione stabile corrente** di **Community Server**selezionare la versione più recente a **64 bit** nella colonna di Windows.</span><span class="sxs-lookup"><span data-stu-id="ef774-110">Find the **Current Stable Release** of **Community Server**, select the latest **64-bit** version in the Windows column.</span></span> <span data-ttu-id="ef774-111">Scaricare ed eseguire il programma di installazione MSI.</span><span class="sxs-lookup"><span data-stu-id="ef774-111">Download, then run the MSI installer.</span></span>
5. <span data-ttu-id="ef774-112">MongoDB viene in genere installato in C:\Programmi\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ef774-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="ef774-113">Cercare le variabili di ambiente sul desktop e aggiungere il percorso di file binari MongoDB alla variabile PATH.</span><span class="sxs-lookup"><span data-stu-id="ef774-113">Search for Environment Variables on the desktop and add the MongoDB binaries path to the PATH variable.</span></span> <span data-ttu-id="ef774-114">I file binari potrebbero essere ad esempio disponibili nel percorso C:\Program Files\MongoDB\Server\3.4\bin del computer.</span><span class="sxs-lookup"><span data-stu-id="ef774-114">For example, you might find the binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="ef774-115">Creare le directory dei dati e dei log di MongoDB nel disco dati, ad esempio l'unità **F:**, creato nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="ef774-115">Create MongoDB data and log directories in the data disk (such as drive **F:**) you created in the preceding steps.</span></span> <span data-ttu-id="ef774-116">Dal menu **Start** scegliere **Prompt dei comandi** per aprire una finestra del prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="ef774-116">From **Start**, select **Command Prompt** to open a command prompt window.</span></span>  <span data-ttu-id="ef774-117">Digitare:</span><span class="sxs-lookup"><span data-stu-id="ef774-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="ef774-118">Per eseguire il database:</span><span class="sxs-lookup"><span data-stu-id="ef774-118">To run the database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="ef774-119">Tutti i messaggi di log vengono indirizzati al file *F:\MongoLogs\mongolog.log* non appena il server mongod.exe viene avviato e vengono preallocati i file journal.</span><span class="sxs-lookup"><span data-stu-id="ef774-119">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="ef774-120">Possono essere necessari diversi minuti per la preallocazione dei file journal di MongoDB e l'inizio dell'attesa delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="ef774-120">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span></span> <span data-ttu-id="ef774-121">Il prompt dei comandi continua con questa attività durante l'esecuzione dell'istanza di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ef774-121">The command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="ef774-122">Per avviare la shell di amministrazione di MongoDB, aprire un'altra finestra del prompt dei comandi dal menu **Start** e digitare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef774-122">To start the MongoDB administrative shell, open another command window from **Start** and type the following commands:</span></span>

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

    <span data-ttu-id="ef774-123">Il database viene creato dall'istruzione insert.</span><span class="sxs-lookup"><span data-stu-id="ef774-123">The database is created by the insert.</span></span>
9. <span data-ttu-id="ef774-124">In alternativa, è possibile installare mongod.exe come servizio:</span><span class="sxs-lookup"><span data-stu-id="ef774-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="ef774-125">Viene installato un servizio denominato MongoDB con la descrizione "MongoDB".</span><span class="sxs-lookup"><span data-stu-id="ef774-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="ef774-126">Per specificare un file di log è necessario usare l'opzione `--logpath`, perché il servizio in esecuzione non ha una finestra di comando in cui visualizzare l'output.</span><span class="sxs-lookup"><span data-stu-id="ef774-126">The `--logpath` option must be used to specify a log file, since the running service does not have a command window to display output.</span></span>  <span data-ttu-id="ef774-127">L'opzione `--logappend` specifica che a seguito di un riavvio del servizio l'output viene aggiunto al file di log esistente.</span><span class="sxs-lookup"><span data-stu-id="ef774-127">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>  <span data-ttu-id="ef774-128">L'opzione `--dbpath` specifica il percorso della directory dei dati.</span><span class="sxs-lookup"><span data-stu-id="ef774-128">The `--dbpath` option specifies the location of the data directory.</span></span> <span data-ttu-id="ef774-129">Per altre opzioni della riga di comando relative ai servizi, vedere le [opzioni della riga di comando relative ai servizi][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="ef774-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="ef774-130">Per avviare il servizio, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="ef774-130">To start the service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="ef774-131">Ora che MongoDB è stato installato ed è in esecuzione, è necessario aprire una porta in Windows Firewall per poter eseguire la connessione remota a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ef774-131">Now that MongoDB is installed and running, you need to open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span>  <span data-ttu-id="ef774-132">Dal menu **Start** scegliere **Strumenti di amministrazione** e quindi **Windows Firewall con sicurezza avanzata**.</span><span class="sxs-lookup"><span data-stu-id="ef774-132">From the **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="ef774-133">a) Nel riquadro a sinistra selezionare **Regole connessioni in entrata**.</span><span class="sxs-lookup"><span data-stu-id="ef774-133">a) In the left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="ef774-134">Nel riquadro **Azioni** a destra selezionare **Nuova regola**.</span><span class="sxs-lookup"><span data-stu-id="ef774-134">In the **Actions** pane on the right, select **New Rule...**.</span></span>

    ![Windows Firewall][Image1]

    <span data-ttu-id="ef774-136">b) In **Creazione guidata nuova regola connessioni in entrata** selezionare **Porta** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ef774-136">b) In the **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows Firewall][Image2]

    <span data-ttu-id="ef774-138">c) Selezionare **TCP** e quindi **Porte locali specifiche**.</span><span class="sxs-lookup"><span data-stu-id="ef774-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="ef774-139">Specificare la porta "27017" (ovvero la porta su cui MongoDB rimane in ascolto) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ef774-139">Specify a port of "27017" (the default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows Firewall][Image3]

    <span data-ttu-id="ef774-141">d) Selezionare **Consenti la connessione** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ef774-141">d) Select **Allow the connection** and click **Next**.</span></span>

    ![Windows Firewall][Image4]

    <span data-ttu-id="ef774-143">e) Fare di nuovo clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ef774-143">e) Click **Next** again.</span></span>

    ![Windows Firewall][Image5]

    <span data-ttu-id="ef774-145">f) Specificare un nome per la regola, ad esempio "PortaMongo" e quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="ef774-145">f) Specify a name for the rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows Firewall][Image6]

12. <span data-ttu-id="ef774-147">A questo punto è possibile configurare un endpoint per MongoDB se non è stato già fatto durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ef774-147">If you didn't configure an endpoint for MongoDB when you created the virtual machine, you can do it now.</span></span> <span data-ttu-id="ef774-148">Per la connessione a MongoDB in modalità remota, sono necessari sia la regola firewall che l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="ef774-148">You need both the firewall rule and the endpoint to be able to connect to MongoDB remotely.</span></span>

  <span data-ttu-id="ef774-149">Nel portale di Azure fare clic su **Macchine virtuali (classico)**, quindi sul nome della nuova macchina virtuale e infine su **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="ef774-149">In the Azure portal, click **Virtual Machines (classic)**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Endpoint][Image7]

13. <span data-ttu-id="ef774-151">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ef774-151">Click **Add**.</span></span>

14. <span data-ttu-id="ef774-152">Aggiungere un endpoint denominato "Mongo", con il protocollo **TCP** e con entrambe le porte **pubblica** e **privata** impostate su "27017".</span><span class="sxs-lookup"><span data-stu-id="ef774-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set to "27017".</span></span> <span data-ttu-id="ef774-153">L'apertura di questa porta consente l'accesso in remoto a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ef774-153">Opening this port allows MongoDB to be accessed remotely.</span></span>

    ![Endpoint][Image9]

> [!NOTE]
> <span data-ttu-id="ef774-155">La porta 27017 è la porta predefinita utilizzata da MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ef774-155">The port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="ef774-156">È possibile modificare la porta predefinita specificando il parametro `--port` all'avvio del server mongod.exe.</span><span class="sxs-lookup"><span data-stu-id="ef774-156">You can change this default port by specifying the `--port` parameter when starting the mongod.exe server.</span></span> <span data-ttu-id="ef774-157">Assicurarsi di assegnare lo stesso numero di porta al firewall e all'endpoint "Mongo" nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="ef774-157">Make sure to give the same port number in the firewall and the "Mongo" endpoint in the preceding instructions.</span></span>
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
