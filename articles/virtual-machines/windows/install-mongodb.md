---
title: Installare MongoDB in una VM Windows in Azure | Documentazione Microsoft
description: Informazioni su come installare MongoDB in una VM di Azure creata con il modello di distribuzione Resource Manager che esegue Windows Server 2012 R2.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: db1a550b9273925b304fe4280f2a1b0e115f856d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="91c80-103">Installare e configurare MongoDB in una VM Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="91c80-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="91c80-104">[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="91c80-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="91c80-105">In questo articolo viene illustrata la procedura di installazione e configurazione di MongoDB in una macchina virtuale (VM) Windows Server 2012 R2 in Azure.</span><span class="sxs-lookup"><span data-stu-id="91c80-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="91c80-106">È anche possibile [installare MongoDB in una VM Linux in Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="91c80-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91c80-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="91c80-107">Prerequisites</span></span>
<span data-ttu-id="91c80-108">Prima di installare e configurare MongoDB, è necessario creare una VM e, idealmente, aggiungere un disco dati.</span><span class="sxs-lookup"><span data-stu-id="91c80-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span></span> <span data-ttu-id="91c80-109">Vedere gli articoli seguenti per creare una VM e aggiungere un disco dati:</span><span class="sxs-lookup"><span data-stu-id="91c80-109">See the following articles to create a VM and add a data disk:</span></span>

* <span data-ttu-id="91c80-110">Creare una macchina virtuale Windows Server usando [il portale di Azure](quick-create-portal.md) o [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="91c80-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="91c80-111">Collegare un disco dati a una macchina virtuale Windows Server usando [il portale di Azure](attach-managed-disk-portal.md) o [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="91c80-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="91c80-112">Per iniziare a installare e configurare MongoDB, [accedere a una VM Windows Server](connect-logon.md) tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="91c80-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="91c80-113">Installare MongoDB</span><span class="sxs-lookup"><span data-stu-id="91c80-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91c80-114">Le funzionalità di sicurezza MongoDB, ad esempio l'autenticazione e l'associazione di indirizzi IP, non sono abilitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="91c80-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="91c80-115">Dovranno essere abilitate prima di distribuire MongoDB in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="91c80-115">Security features should be enabled before deploying MongoDB to a production environment.</span></span> <span data-ttu-id="91c80-116">Per altre informazioni, vedere [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication) (Sicurezza e autenticazione di MongoDB).</span><span class="sxs-lookup"><span data-stu-id="91c80-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="91c80-117">Dopo avere eseguito la connessione alla VM tramite Desktop remoto, aprire Internet Explorer dal menu **Start** della VM.</span><span class="sxs-lookup"><span data-stu-id="91c80-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the **Start** menu on the VM.</span></span>
2. <span data-ttu-id="91c80-118">All'apertura di Internet Explorer, selezionare **Usa impostazioni di sicurezza, privacy e compatibilità consigliate** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="91c80-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="91c80-119">La configurazione di protezione avanzata di Internet Explorer è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="91c80-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="91c80-120">Aggiungere il sito Web di MongoDB all'elenco dei siti consentiti:</span><span class="sxs-lookup"><span data-stu-id="91c80-120">Add the MongoDB website to the list of allowed sites:</span></span>
   
   * <span data-ttu-id="91c80-121">Nell'angolo superiore destro fare clic sull'icona **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="91c80-121">Select the **Tools** icon in the upper-right corner.</span></span>
   * <span data-ttu-id="91c80-122">In **Opzioni Internet** selezionare la scheda **Sicurezza**, quindi l'icona **Siti attendibili**.</span><span class="sxs-lookup"><span data-stu-id="91c80-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="91c80-123">Fare clic sul pulsante **Siti**.</span><span class="sxs-lookup"><span data-stu-id="91c80-123">Click the **Sites** button.</span></span> <span data-ttu-id="91c80-124">Aggiungere *https://\*.mongodb.org* all'elenco dei siti attendibili, quindi chiudere la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="91c80-124">Add *https://\*.mongodb.org* to the list of trusted sites, and then close the dialog box.</span></span>
     
     ![Configurare le impostazioni di sicurezza di Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="91c80-126">Accedere alla pagina dei [download di MongoDB](http://www.mongodb.org/downloads) (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="91c80-126">Browse to the [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="91c80-127">Se necessario, selezionare l'edizione **Community Server** e quindi l'ultima versione stabile corrente per Windows Server 2008 R2 a 64 bit e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="91c80-127">If needed, select the **Community Server** edition and then select the latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="91c80-128">Per scaricare il programma di installazione, fare clic su **DOWNLOAD (msi)**.</span><span class="sxs-lookup"><span data-stu-id="91c80-128">To download the installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Scaricare il programma di installazione di MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="91c80-130">Eseguire il programma di installazione al termine del download.</span><span class="sxs-lookup"><span data-stu-id="91c80-130">Run the installer after the download is complete.</span></span>
6. <span data-ttu-id="91c80-131">Leggere e accettare il contratto di licenza.</span><span class="sxs-lookup"><span data-stu-id="91c80-131">Read and accept the license agreement.</span></span> <span data-ttu-id="91c80-132">Quando richiesto, selezionare **Completa** per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="91c80-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="91c80-133">Nella schermata finale fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="91c80-133">On the final screen, click **Install**.</span></span>

## <a name="configure-the-vm-and-mongodb"></a><span data-ttu-id="91c80-134">Configurare la VM e MongoDB</span><span class="sxs-lookup"><span data-stu-id="91c80-134">Configure the VM and MongoDB</span></span>
1. <span data-ttu-id="91c80-135">Le variabili di percorso non vengono aggiornate dal programma di installazione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-135">The path variables are not updated by the MongoDB installer.</span></span> <span data-ttu-id="91c80-136">Senza il percorso `bin` di MongoDB nella variabile di percorso, è necessario specificare il percorso completo ogni volta che si usa un file eseguibile di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-136">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="91c80-137">Per aggiungere il percorso alla variabile:</span><span class="sxs-lookup"><span data-stu-id="91c80-137">To add the location to your path variable:</span></span>
   
   * <span data-ttu-id="91c80-138">Fare clic con il pulsante destro del mouse sul menu **Start** e selezionare **Sistema**.</span><span class="sxs-lookup"><span data-stu-id="91c80-138">Right-click the **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="91c80-139">Fare clic sulla scheda **Impostazioni di sistema avanzate**, quindi su **Variabili d'ambiente**.</span><span class="sxs-lookup"><span data-stu-id="91c80-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="91c80-140">In **Variabili di sistema** selezionare **Percorso**, quindi fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="91c80-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configurare le variabili di PERCORSO](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="91c80-142">Aggiungere il percorso alla cartella `bin` di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-142">Add the path to your MongoDB `bin` folder.</span></span> <span data-ttu-id="91c80-143">MongoDB viene in genere installato in *C:\Programmi\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="91c80-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="91c80-144">Verificare il percorso di installazione nella VM.</span><span class="sxs-lookup"><span data-stu-id="91c80-144">Verify the installation path on your VM.</span></span> <span data-ttu-id="91c80-145">Nell'esempio seguente viene aggiunto il percorso di installazione predefinito di MongoDB alla variabile `PATH`:</span><span class="sxs-lookup"><span data-stu-id="91c80-145">The following example adds the default MongoDB install location to the `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="91c80-146">Assicurarsi di aggiungere il punto e virgola iniziale (`;`) per indicare che si sta aggiungendo un percorso alla variabile `PATH`.</span><span class="sxs-lookup"><span data-stu-id="91c80-146">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span></span>

2. <span data-ttu-id="91c80-147">Creare le directory di log e dati di MongoDB nel disco dati.</span><span class="sxs-lookup"><span data-stu-id="91c80-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="91c80-148">Nel menu **Start** selezionare **Prompt dei comandi**.</span><span class="sxs-lookup"><span data-stu-id="91c80-148">From the **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="91c80-149">Nell'esempio seguente vengono create le directory nell'unità F:</span><span class="sxs-lookup"><span data-stu-id="91c80-149">The following examples create the directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="91c80-150">Avviare un'istanza di MongoDB con il comando seguente, modificando di conseguenza il percorso alle directory di log e dati:</span><span class="sxs-lookup"><span data-stu-id="91c80-150">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="91c80-151">Possono essere necessari diversi minuti per l'allocazione dei file journal di MongoDB e l'inizio dell'attesa delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="91c80-151">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span></span> <span data-ttu-id="91c80-152">Tutti i messaggi di log vengono indirizzati al file *F:\MongoLogs\mongolog.log* non appena il server `mongod.exe` viene avviato e vengono allocati i file journal.</span><span class="sxs-lookup"><span data-stu-id="91c80-152">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="91c80-153">Il prompt dei comandi continua con questa attività durante l'esecuzione dell'istanza di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-153">The command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="91c80-154">Lasciare aperta la finestra del prompt dei comandi per continuare l'esecuzione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-154">Leave the command prompt window open to continue running MongoDB.</span></span> <span data-ttu-id="91c80-155">In alternativa, installare MongoDB come servizio, come descritto nei dettagli nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="91c80-155">Or, install MongoDB as service, as detailed in the next step.</span></span>

4. <span data-ttu-id="91c80-156">Per un'esperienza più affidabile con MongoDB, installare `mongod.exe` come servizio.</span><span class="sxs-lookup"><span data-stu-id="91c80-156">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span></span> <span data-ttu-id="91c80-157">Cerare un servizio significa che non è necessario lasciare in esecuzione un prompt dei comandi ogni volta che si desidera usare MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-157">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span></span> <span data-ttu-id="91c80-158">Creare il servizio come indicato di seguito, modificando di conseguenza il percorso alle directory di log e dati:</span><span class="sxs-lookup"><span data-stu-id="91c80-158">Create the service as follows, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="91c80-159">Il comando precedente crea un servizio chiamato MongoDB con la descrizione "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="91c80-159">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="91c80-160">Vengono specificati anche i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="91c80-160">The following parameters are also specified:</span></span>
   
   * <span data-ttu-id="91c80-161">L'opzione `--dbpath` specifica il percorso della directory dei dati.</span><span class="sxs-lookup"><span data-stu-id="91c80-161">The `--dbpath` option specifies the location of the data directory.</span></span>
   * <span data-ttu-id="91c80-162">Per specificare un file di log è necessario usare l'opzione `--logpath`, perché il servizio in esecuzione non ha una finestra di comando in cui visualizzare l'output.</span><span class="sxs-lookup"><span data-stu-id="91c80-162">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span></span>
   * <span data-ttu-id="91c80-163">L'opzione `--logappend` specifica che a seguito di un riavvio del servizio l'output viene aggiunto al file di log esistente.</span><span class="sxs-lookup"><span data-stu-id="91c80-163">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>
   
   <span data-ttu-id="91c80-164">Per avviare il servizio MongoDB, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="91c80-164">To start the MongoDB service, run the following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="91c80-165">Per altre informazioni sulla creazione del servizio di MongoDB, vedere [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service) (Configurare un servizio Windows per MongoDB).</span><span class="sxs-lookup"><span data-stu-id="91c80-165">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-the-mongodb-instance"></a><span data-ttu-id="91c80-166">Testare l'istanza di MongoDB</span><span class="sxs-lookup"><span data-stu-id="91c80-166">Test the MongoDB instance</span></span>
<span data-ttu-id="91c80-167">Con MongoDB in esecuzione come istanza singola o installato come servizio, è possibile avviare la creazione e l'uso dei database.</span><span class="sxs-lookup"><span data-stu-id="91c80-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="91c80-168">Per avviare la shell di amministrazione di MongoDB, aprire un'altra finestra del prompt dei comandi dal menu **Start** e immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="91c80-168">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span></span>

```
mongo  
```

<span data-ttu-id="91c80-169">È possibile elencare i database con il comando `db`.</span><span class="sxs-lookup"><span data-stu-id="91c80-169">You can list the databases with the `db` command.</span></span> <span data-ttu-id="91c80-170">Inserire alcuni dati come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91c80-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="91c80-171">Cercare i dati come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91c80-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="91c80-172">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="91c80-172">The output is similar to the following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="91c80-173">Uscire dalla console `mongo` come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91c80-173">Exit the `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="91c80-174">Configurare le regole del firewall e del gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="91c80-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="91c80-175">Ora che MongoDB è stato installato ed è in esecuzione, aprire una porta in Windows Firewall per poter eseguire la connessione remota a MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span> <span data-ttu-id="91c80-176">Per creare una nuova regola in ingresso per consentire la porta TCP 27017, aprire un prompt amministrativo di PowerShell e immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="91c80-176">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="91c80-177">È anche possibile creare la regola usando lo strumento grafico di gestione **Windows Firewall con sicurezza avanzata**.</span><span class="sxs-lookup"><span data-stu-id="91c80-177">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="91c80-178">Creare una nuova regola in ingresso per consentire la porta TCP 27017.</span><span class="sxs-lookup"><span data-stu-id="91c80-178">Create a new inbound rule to allow TCP port 27017.</span></span>

<span data-ttu-id="91c80-179">Se necessario, creare una regola del gruppo di sicurezza di rete per consentire l'accesso a MongoDB all'esterno della subnet di rete virtuale di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="91c80-179">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span></span> <span data-ttu-id="91c80-180">È possibile creare le regole del gruppo di sicurezza di rete tramite il [portale di Azure](nsg-quickstart-portal.md) o [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="91c80-180">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="91c80-181">Come con le regole di Windows Firewall, consentire la porta TCP 27017 per l'interfaccia di rete virtuale della VM di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-181">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="91c80-182">La porta TPC 27017 è la porta predefinita usata da MongoDB.</span><span class="sxs-lookup"><span data-stu-id="91c80-182">TCP port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="91c80-183">È possibile modificare la porta usando il parametro `--port` quando `mongod.exe` viene avviato manualmente o da un servizio.</span><span class="sxs-lookup"><span data-stu-id="91c80-183">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="91c80-184">Se si modifica la porta, assicurarsi di aggiornare le regole di Windows Firewall e del gruppo di sicurezza di rete nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="91c80-184">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="91c80-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="91c80-185">Next steps</span></span>
<span data-ttu-id="91c80-186">In questa esercitazione è stato illustrato come installare e configurare MongoDB nella VM Windows.</span><span class="sxs-lookup"><span data-stu-id="91c80-186">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="91c80-187">È ora possibile accedere a MongoDB nella VM basata su Windows, seguendo gli argomenti avanzati illustrati nella [documentazione di MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="91c80-187">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

