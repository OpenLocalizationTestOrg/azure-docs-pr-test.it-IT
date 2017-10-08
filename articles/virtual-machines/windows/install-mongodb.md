---
title: aaaInstall MongoDB in una macchina virtuale Windows in Azure | Documenti Microsoft
description: Informazioni su come creare i tooinstall MongoDB in una macchina virtuale di Azure che esegue Windows Server 2012 R2 con modello di distribuzione di gestione risorse di hello.
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
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="7d96c-103">Installare e configurare MongoDB in una VM Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="7d96c-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="7d96c-104">[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="7d96c-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="7d96c-105">In questo articolo viene illustrata la procedura di installazione e configurazione di MongoDB in una macchina virtuale (VM) Windows Server 2012 R2 in Azure.</span><span class="sxs-lookup"><span data-stu-id="7d96c-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="7d96c-106">È anche possibile [installare MongoDB in una VM Linux in Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="7d96c-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d96c-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7d96c-107">Prerequisites</span></span>
<span data-ttu-id="7d96c-108">Prima di installare e configurare MongoDB, è necessario toocreate una macchina virtuale e, idealmente, aggiungere un tooit disco dati.</span><span class="sxs-lookup"><span data-stu-id="7d96c-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="7d96c-109">Vedere i seguenti articoli toocreate una macchina virtuale hello e aggiungere un disco dati:</span><span class="sxs-lookup"><span data-stu-id="7d96c-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="7d96c-110">Creare una macchina virtuale Windows Server utilizzando [hello Azure portal](quick-create-portal.md) o [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7d96c-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="7d96c-111">Collegare un dati disco tooa macchina virtuale Windows Server tramite [hello Azure portal](attach-managed-disk-portal.md) o [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7d96c-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="7d96c-112">toobegin installazione e configurazione di MongoDB, [accedere tooyour macchina virtuale Windows Server](connect-logon.md) tramite Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="7d96c-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="7d96c-113">Installare MongoDB</span><span class="sxs-lookup"><span data-stu-id="7d96c-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7d96c-114">Le funzionalità di sicurezza MongoDB, ad esempio l'autenticazione e l'associazione di indirizzi IP, non sono abilitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7d96c-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="7d96c-115">Funzionalità di sicurezza devono essere abilitate prima di distribuire l'ambiente di produzione tooa MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d96c-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="7d96c-116">Per altre informazioni, vedere [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication) (Sicurezza e autenticazione di MongoDB).</span><span class="sxs-lookup"><span data-stu-id="7d96c-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="7d96c-117">Dopo aver collegato tooyour macchina virtuale tramite Desktop remoto, aprire Internet Explorer da hello **avviare** menu hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d96c-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="7d96c-118">All'apertura di Internet Explorer, selezionare **Usa impostazioni di sicurezza, privacy e compatibilità consigliate** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d96c-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="7d96c-119">La configurazione di protezione avanzata di Internet Explorer è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7d96c-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="7d96c-120">Aggiungere hello MongoDB toohello l'elenco dei siti dei siti consentiti:</span><span class="sxs-lookup"><span data-stu-id="7d96c-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="7d96c-121">Seleziona hello **strumenti** sull'icona nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="7d96c-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="7d96c-122">In **Opzioni Internet**selezionare hello **sicurezza** scheda e quindi selezionare hello **siti attendibili** icona.</span><span class="sxs-lookup"><span data-stu-id="7d96c-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="7d96c-123">Fare clic su hello **siti** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7d96c-123">Click hello **Sites** button.</span></span> <span data-ttu-id="7d96c-124">Aggiungere *https://\*. mongodb.org* toohello elenco siti attendibili e quindi chiudere hello, finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7d96c-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Configurare le impostazioni di sicurezza di Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="7d96c-126">Sfoglia toohello [MongoDB - Scarica](http://www.mongodb.org/downloads) pagina (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="7d96c-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="7d96c-127">Se necessario, selezionare hello **Server Community** edition e quindi selezionare hello versione più recente corrente stabile per Windows Server 2008 R2 64 bit e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="7d96c-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="7d96c-128">toodownload hello programma di installazione, fare clic su **DOWNLOAD (msi)**.</span><span class="sxs-lookup"><span data-stu-id="7d96c-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Scaricare il programma di installazione di MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="7d96c-130">Eseguire il programma di installazione hello dopo aver completato il download di hello.</span><span class="sxs-lookup"><span data-stu-id="7d96c-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="7d96c-131">Leggere e accettare il contratto di licenza hello.</span><span class="sxs-lookup"><span data-stu-id="7d96c-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="7d96c-132">Quando richiesto, selezionare **Completa** per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="7d96c-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="7d96c-133">Nella schermata finale hello, fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="7d96c-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="7d96c-134">Configurare hello VM e MongoDB</span><span class="sxs-lookup"><span data-stu-id="7d96c-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="7d96c-135">le variabili di percorso Hello non vengono aggiornate dal programma di installazione di hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d96c-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="7d96c-136">Senza hello MongoDB `bin` posizione, la variabile path, è necessario percorso completo di hello toospecify ogni volta che si utilizza un file eseguibile di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d96c-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="7d96c-137">variabile di percorso tooyour posizione hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="7d96c-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="7d96c-138">Pulsante destro del mouse hello **avviare** dal menu **sistema**.</span><span class="sxs-lookup"><span data-stu-id="7d96c-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="7d96c-139">Fare clic sulla scheda **Impostazioni di sistema avanzate**, quindi su **Variabili d'ambiente**.</span><span class="sxs-lookup"><span data-stu-id="7d96c-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="7d96c-140">In **Variabili di sistema** selezionare **Percorso**, quindi fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="7d96c-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configurare le variabili di PERCORSO](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="7d96c-142">Aggiungi percorso di hello tooyour MongoDB `bin` cartella.</span><span class="sxs-lookup"><span data-stu-id="7d96c-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="7d96c-143">MongoDB viene in genere installato in *C:\Programmi\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="7d96c-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="7d96c-144">Verificare il percorso di installazione hello nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d96c-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="7d96c-145">esempio Hello aggiunge hello predefinito MongoDB installazione percorso toohello `PATH` variabile:</span><span class="sxs-lookup"><span data-stu-id="7d96c-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="7d96c-146">Punto e virgola iniziale di hello tooadd assicurarsi di essere (`;`) che si sta aggiungendo un percorso tooyour tooindicate `PATH` variabile.</span><span class="sxs-lookup"><span data-stu-id="7d96c-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="7d96c-147">Creare le directory di log e dati di MongoDB nel disco dati.</span><span class="sxs-lookup"><span data-stu-id="7d96c-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="7d96c-148">Da hello **avviare** dal menu **prompt dei comandi**.</span><span class="sxs-lookup"><span data-stu-id="7d96c-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="7d96c-149">seguono esempi Hello Crea directory hello nell'unità f:</span><span class="sxs-lookup"><span data-stu-id="7d96c-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="7d96c-150">Avviare un'istanza di MongoDB con hello comando seguente, modificare dati tooyour del percorso hello e directory del Registro di conseguenza:</span><span class="sxs-lookup"><span data-stu-id="7d96c-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="7d96c-151">Può richiedere alcuni minuti per MongoDB tooallocate file journal hello e avvia l'ascolto delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="7d96c-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="7d96c-152">Tutti i messaggi di log sono diretto toohello *F:\MongoLogs\mongolog.log* file come `mongod.exe` server verrà avviato e alloca file journal.</span><span class="sxs-lookup"><span data-stu-id="7d96c-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7d96c-153">prompt dei comandi di Hello rimane attivo per l'attività mentre è in esecuzione l'istanza di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d96c-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="7d96c-154">Lasciare hello prompt dei comandi finestra aperta toocontinue sia in esecuzione MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d96c-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="7d96c-155">In alternativa, installare MongoDB come servizio, come descritto nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="7d96c-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="7d96c-156">Per un'esperienza più affidabile di MongoDB, installare hello `mongod.exe` come servizio.</span><span class="sxs-lookup"><span data-stu-id="7d96c-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="7d96c-157">Creazione di un servizio, significa che è necessario tooleave un prompt dei comandi in esecuzione ogni volta che si desidera toouse MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d96c-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="7d96c-158">Creare il servizio hello come indicato di seguito, regolando hello percorso tooyour log directory di dati e di conseguenza:</span><span class="sxs-lookup"><span data-stu-id="7d96c-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="7d96c-159">Hello comando precedente crea un servizio denominato MongoDB, con una descrizione di "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="7d96c-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="7d96c-160">è stata specificata anche Hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="7d96c-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="7d96c-161">Hello `--dbpath` opzione specifica hello percorso della directory di dati hello.</span><span class="sxs-lookup"><span data-stu-id="7d96c-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="7d96c-162">Hello `--logpath` opzione deve essere toospecify utilizzato un file di log, perché servizio in esecuzione hello non dispone di un output toodisplay finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="7d96c-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="7d96c-163">Hello `--logappend` opzione specifica che un riavvio del servizio hello provoca output tooappend toohello file di log esistente.</span><span class="sxs-lookup"><span data-stu-id="7d96c-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="7d96c-164">servizio di MongoDB di hello di toostart, eseguire il comando seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7d96c-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="7d96c-165">Per ulteriori informazioni sulla creazione di hello MongoDB servizio, vedere [configurare un servizio Windows per MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="7d96c-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="7d96c-166">Istanza di prova hello MongoDB</span><span class="sxs-lookup"><span data-stu-id="7d96c-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="7d96c-167">Con MongoDB in esecuzione come istanza singola o installato come servizio, è possibile avviare la creazione e l'uso dei database.</span><span class="sxs-lookup"><span data-stu-id="7d96c-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="7d96c-168">hello toostart shell amministrativa MongoDB, aprire un'altra finestra del prompt dei comandi da hello **avviare** menu, quindi immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7d96c-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="7d96c-169">È possibile elencare i database hello con hello `db` comando.</span><span class="sxs-lookup"><span data-stu-id="7d96c-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="7d96c-170">Inserire alcuni dati come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7d96c-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="7d96c-171">Cercare i dati come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7d96c-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="7d96c-172">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="7d96c-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="7d96c-173">Hello uscita `mongo` console come segue:</span><span class="sxs-lookup"><span data-stu-id="7d96c-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="7d96c-174">Configurare le regole del firewall e del gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="7d96c-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="7d96c-175">Ora che MongoDB è installato e in esecuzione, aprire una porta in Windows Firewall in modo è possibile connettersi in remoto tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d96c-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="7d96c-176">toocreate una nuova regola connessioni in entrata tooallow porta 27017, aprire un prompt dei comandi amministrativi di PowerShell e immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7d96c-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="7d96c-177">È anche possibile creare regole hello utilizzando hello **Windows Firewall con sicurezza avanzata** strumento di gestione con interfaccia grafica.</span><span class="sxs-lookup"><span data-stu-id="7d96c-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="7d96c-178">Creare una nuova regola connessioni in entrata tooallow porta 27017.</span><span class="sxs-lookup"><span data-stu-id="7d96c-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="7d96c-179">Se necessario, creare un gruppo di sicurezza di rete regola tooallow accesso tooMongoDB di fuori di subnet di rete virtuale di Azure esistente hello.</span><span class="sxs-lookup"><span data-stu-id="7d96c-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="7d96c-180">È possibile creare regole del gruppo di sicurezza di rete hello utilizzando hello [portale di Azure](nsg-quickstart-portal.md) o [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7d96c-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="7d96c-181">Come con le regole Firewall di Windows hello, consentire l'interfaccia di rete virtuale toohello 27017 porta TCP di VM MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7d96c-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="7d96c-182">La porta TCP 27017 è utilizzata da MongoDB la porta predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="7d96c-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="7d96c-183">È possibile modificare la porta tramite hello `--port` parametro quando si avvia `mongod.exe` manualmente o da un servizio.</span><span class="sxs-lookup"><span data-stu-id="7d96c-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="7d96c-184">Se si modifica la porta hello, apportare che tooupdate hello Windows regole Firewall e di gruppo di sicurezza di rete nel hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="7d96c-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7d96c-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d96c-185">Next steps</span></span>
<span data-ttu-id="7d96c-186">In questa esercitazione, si è appreso come tooinstall e configurare MongoDB nella VM Windows.</span><span class="sxs-lookup"><span data-stu-id="7d96c-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="7d96c-187">È ora possibile accedere MongoDB nella VM Windows, di seguito hello avanzata nel hello [documentazione di MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="7d96c-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

