---
title: recapito aaaContinuous per cloud services con TFS in Azure | Documenti Microsoft
description: Informazioni su come App cloud tooset le opzioni di distribuzione continua per Azure. Esempi di codice Code per istruzioni della riga di comando MSBuild e script di PowerShell.
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="34120-104">Recapito continuo per Servizi cloud in Azure</span><span class="sxs-lookup"><span data-stu-id="34120-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="34120-105">Hello processo descritto in questo articolo illustra come tooset le opzioni di distribuzione continua per le applicazioni cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="34120-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="34120-106">Questo processo consente di creare automaticamente i pacchetti e distribuire hello pacchetto tooAzure dopo ogni archiviazione codice.</span><span class="sxs-lookup"><span data-stu-id="34120-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="34120-107">il processo di compilazione pacchetto descritto in questo articolo Hello è equivalente toohello **pacchetto** comandi di Visual Studio e la procedura per la pubblicazione è equivalente toohello **pubblica** comando in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34120-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="34120-108">Hello articolo include informazioni su hello metodi utilizzare toocreate un server di compilazione con le istruzioni della riga di comando di MSBuild e script di Windows PowerShell e viene inoltre illustrato come toooptionally configurare Visual Studio Team Foundation Server - definizioni di compilazione Team i comandi di MSBuild hello toouse e gli script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34120-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="34120-109">il processo di Hello è personalizzabile per gli ambienti di Azure di destinazione e l'ambiente di compilazione.</span><span class="sxs-lookup"><span data-stu-id="34120-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="34120-110">È inoltre possibile utilizzare Visual Studio Team Services, una versione di TFS che è ospitato in Azure, toodo questo più facilmente.</span><span class="sxs-lookup"><span data-stu-id="34120-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="34120-111">Prima di iniziare, pubblicare l'applicazione da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34120-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="34120-112">Ciò garantisce che tutte le risorse di hello siano disponibili e inizializzato quando si tenta di processo di pubblicazione tooautomate hello.</span><span class="sxs-lookup"><span data-stu-id="34120-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="34120-113">1: configurare hello Build Server</span><span class="sxs-lookup"><span data-stu-id="34120-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="34120-114">Prima di creare un pacchetto Azure utilizzando MSBuild, è necessario installare il software necessario hello e gli strumenti nel server di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="34120-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="34120-115">Visual Studio non è necessario toobe installato nel server di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="34120-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="34120-116">Se si desidera toouse servizio Team Foundation Build toomanage il server di compilazione, seguire le istruzioni hello hello [servizio Team Foundation Build] [ Team Foundation Build Service] documentazione.</span><span class="sxs-lookup"><span data-stu-id="34120-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="34120-117">Nel server di compilazione hello, installare hello [.NET Framework 4.5.2][.NET Framework 4.5.2], che include MSBuild.</span><span class="sxs-lookup"><span data-stu-id="34120-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="34120-118">Installare più recente hello [gli strumenti di creazione di Azure per .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="34120-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="34120-119">Installare hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="34120-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="34120-120">Server di compilazione copia del file WebApplication hello da un toohello di installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34120-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="34120-121">In un computer con installato Visual Studio, questo file si trova nella directory hello c:\\programmi (x86)\\MSBuild\\Microsoft\\VisualStudio\\v 14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="34120-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="34120-122">È necessario copiarlo toohello stessa directory nel server di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="34120-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="34120-123">Installare hello [strumenti di Azure per Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="34120-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="34120-124">2: Compilare un pacchetto usando i comandi MSBuild</span><span class="sxs-lookup"><span data-stu-id="34120-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="34120-125">In questa sezione viene descritto come tooconstruct un MSBuild comando che compila un pacchetto di Azure.</span><span class="sxs-lookup"><span data-stu-id="34120-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="34120-126">Eseguire questo passaggio in hello tooverify server di compilazione che tutto è configurato correttamente e che il comando di MSBuild hello consente di eseguire le operazioni desiderate toodo.</span><span class="sxs-lookup"><span data-stu-id="34120-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="34120-127">È possibile aggiungere tooexisting questa riga di comando script o compilano sui server di compilazione hello, è possibile utilizzare la riga di comando hello in una definizione di compilazione TFS, come descritto nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="34120-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="34120-128">Per altre informazioni sui parametri della riga di comando e su MSBuild, vedere [Riferimenti alla riga di comando di MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="34120-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="34120-129">Se Visual Studio è installato nel server di compilazione hello, individuare e selezionare **prompt dei comandi di Visual Studio** in hello **Visual Studio Tools** cartella Windows.</span><span class="sxs-lookup"><span data-stu-id="34120-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="34120-130">Se Visual Studio non è installato nel server di compilazione hello, aprire un prompt dei comandi e assicurarsi che sia accessibile nel percorso di MSBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="34120-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="34120-131">MSBuild viene installato con .NET Framework Ciao hello percorso % WINDIR %\\Microsoft.NET\\Framework\\*versione*.</span><span class="sxs-lookup"><span data-stu-id="34120-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="34120-132">Ad esempio, per aggiungere variabile di ambiente PATH di MSBuild.exe toohello dopo aver installato .NET Framework 4, digitare hello comando al prompt dei comandi di hello seguente:</span><span class="sxs-lookup"><span data-stu-id="34120-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="34120-133">Al prompt dei comandi di hello, spostarsi sulla cartella toohello contenente il file di progetto Azure che si desidera toobuild.</span><span class="sxs-lookup"><span data-stu-id="34120-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="34120-134">Eseguire MSBuild con hello /target: opzione come hello di esempio seguente per la pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="34120-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="34120-135">Per questa opzione è possibile usare la sintassi abbreviata /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="34120-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="34120-136">opzione /t:Publish Hello in MSBuild non deve essere confuso con i comandi di pubblicazione hello disponibili in Visual Studio quando si dispone di hello che Azure SDK installato.</span><span class="sxs-lookup"><span data-stu-id="34120-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="34120-137">Hello /t: opzione per la pubblicazione solo le compilazioni hello Azure pacchetti.</span><span class="sxs-lookup"><span data-stu-id="34120-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="34120-138">Non è possibile distribuire i pacchetti hello come comandi pubblica hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34120-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="34120-139">Facoltativamente, è possibile specificare il nome di progetto hello come parametro di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="34120-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="34120-140">Se non specificato, viene utilizzata la directory corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="34120-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="34120-141">Per altre informazioni sulle opzioni della riga di comando di MSBuild, vedere [Riferimenti alla riga di comando di MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="34120-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="34120-142">Individuare l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="34120-142">Locate hello output.</span></span> <span data-ttu-id="34120-143">Per impostazione predefinita, questo comando crea una directory nella cartella radice toohello di relazione per il progetto di hello, ad esempio *ProjectDir*\\bin\\*configurazione* \\ app.publish\\.</span><span class="sxs-lookup"><span data-stu-id="34120-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="34120-144">Quando si compila un progetto Azure, si genera due file: hello file del pacchetto e hello che accompagna i file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="34120-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="34120-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="34120-145">Project.cspkg</span></span>
   * <span data-ttu-id="34120-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="34120-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="34120-147">Per impostazione predefinita, ogni progetto Azure include un file di configurazione del servizio (file con estensione cscfg) per compilazioni locali (debug) e un altro per le compilazioni nel cloud (gestione temporanea o produzione), ma è possibile aggiungere o rimuovere file di configurazione del servizio in base alle necessità.</span><span class="sxs-lookup"><span data-stu-id="34120-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="34120-148">Quando si compila un pacchetto all'interno di Visual Studio, verrà richiesto quale tooinclude file di configurazione del servizio insieme ai pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="34120-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="34120-149">Specificare il file di configurazione servizio hello.</span><span class="sxs-lookup"><span data-stu-id="34120-149">Specify hello service configuration file.</span></span> <span data-ttu-id="34120-150">Quando si compila un pacchetto utilizzando MSBuild, i file di configurazione di servizio locale hello è incluso per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="34120-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="34120-151">tooinclude un file di configurazione del servizio diverso, impostare la proprietà TargetProfile del comando di MSBuild hello, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="34120-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="34120-152">Specificare il percorso di hello per l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="34120-152">Specify hello location for hello output.</span></span> <span data-ttu-id="34120-153">Imposta percorso hello utilizzando i /p: PublishDir =*Directory* \\ opzione, tra cui hello separatore barra rovesciata, come l'esempio seguente hello finale:</span><span class="sxs-lookup"><span data-stu-id="34120-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="34120-154">Dopo avere creato e testato un appropriato MSBuild toobuild riga di comando dei progetti e combinarli in un pacchetto di Azure, è possibile aggiungere script di compilazione tooyour questa riga di comando.</span><span class="sxs-lookup"><span data-stu-id="34120-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="34120-155">Se il server di compilazione usa script personalizzati, questo processo dipende dalle specifiche del processo personalizzato di compilazione.</span><span class="sxs-lookup"><span data-stu-id="34120-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="34120-156">Se si usa TFS come un ambiente di compilazione, quindi è possibile seguire le istruzioni hello hello passaggio successivo del processo di compilazione tooyour tooadd hello Azure pacchetto compilazione.</span><span class="sxs-lookup"><span data-stu-id="34120-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="34120-157">3: Compilare un pacchetto usando TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="34120-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="34120-158">Se dispone di Team Foundation Server (TFS) impostato come server di compilazione di un controller di compilazione e hello impostato come un computer di compilazione TFS, quindi è possibile facoltativamente configurare una compilazione automatica per il pacchetto di Azure.</span><span class="sxs-lookup"><span data-stu-id="34120-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="34120-159">Per informazioni su come tooset backup e utilizzare Team Foundation server come un sistema di compilazione, vedere [scalabilità del sistema di compilazione][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="34120-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="34120-160">In particolare, la procedura seguente si presuppone che il server di compilazione è stato configurato come descritto in [distribuire e configurare un server di compilazione][Deploy and configure a build server], e che hanno creato un progetto team, creare un cloud progetto di servizio nel progetto team hello.</span><span class="sxs-lookup"><span data-stu-id="34120-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="34120-161">tooconfigure TFS toobuild Azure pacchetti, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="34120-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="34120-162">In Visual Studio nel computer di sviluppo, nel menu Visualizza di hello, scegliere **Team Explorer**, oppure scegliere Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="34120-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="34120-163">Nella finestra Team Explorer, espandere hello **compilazioni** nodo oppure scegliere hello **compilazioni** , quindi selezionare **nuova definizione di compilazione**.</span><span class="sxs-lookup"><span data-stu-id="34120-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![Opzione Nuova definizione di compilazione][0]
2. <span data-ttu-id="34120-165">Scegliere hello **Trigger** scheda e specificare hello desiderate le condizioni per cui si desidera hello toobe pacchetto generato.</span><span class="sxs-lookup"><span data-stu-id="34120-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="34120-166">Ad esempio, specificare **integrazione continua** si verifica il pacchetto hello toobuild ogni volta che un controllo origine check-in.</span><span class="sxs-lookup"><span data-stu-id="34120-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="34120-167">Scegliere hello **le impostazioni dell'origine** scheda e assicurarsi che la cartella del progetto sia elencata in hello **cartella del codice sorgente** colonna, senza che sia stato hello **Active**.</span><span class="sxs-lookup"><span data-stu-id="34120-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="34120-168">Scegliere hello **impostazioni predefinite compilazione** e controller di compilazione, verificare il nome di hello del server di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="34120-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="34120-169">Inoltre, scegliere l'opzione hello **operazioni seguenti toohello output di compilazione Copia cartella di ricezione** e specificare il percorso di rilascio hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="34120-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="34120-170">Scegliere hello **processo** scheda. Nella scheda processo hello scegliere modello predefinito hello in **compilare**, scegliere il progetto di hello se non è già selezionata, espandere hello **avanzate** sezione hello **compilare**sezione della griglia hello.</span><span class="sxs-lookup"><span data-stu-id="34120-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="34120-171">Scegliere **argomenti MSBuild**e impostare gli argomenti della riga di comando MSBuild appropriati hello, come descritto nel passaggio 2 precedente.</span><span class="sxs-lookup"><span data-stu-id="34120-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="34120-172">Ad esempio, immettere **/t: pubblicare /p: PublishDir =\\\\myserver\\Elimina\\**  toohello percorso dei file di un pacchetto di hello pacchetto e copia toobuild \\ \\myserver\\Elimina\\:</span><span class="sxs-lookup"><span data-stu-id="34120-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![Argomenti MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="34120-174">Copia tooa file hello condivisione pubblica rende più semplice toomanually distribuire i pacchetti hello dal computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="34120-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="34120-175">Test successo hello dell'istruzione di compilazione mediante il controllo in un progetto tooyour modifica o una nuova compilazione accodati.</span><span class="sxs-lookup"><span data-stu-id="34120-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="34120-176">tooqueue di una nuova compilazione, in Team Explorer, fare doppio clic su **tutte le definizioni di compilazione,** e quindi scegliere **Accoda nuova compilazione**.</span><span class="sxs-lookup"><span data-stu-id="34120-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="34120-177">4: Pubblicare un pacchetto usando uno script PowerShell</span><span class="sxs-lookup"><span data-stu-id="34120-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="34120-178">In questa sezione viene descritto come uno script di Windows PowerShell per la pubblicazione del pacchetto di app Cloud hello tooconstruct output tooAzure utilizzando i parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="34120-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="34120-179">Questo script può essere chiamato dopo la compilazione hello passaggio in automazione di compilazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="34120-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="34120-180">È possibile chiamare lo script anche da attività del flusso di lavoro del modello di processo in Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="34120-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="34120-181">Installare hello [cmdlet di Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="34120-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="34120-182">Durante la fase di installazione di cmdlet hello, scegliere tooinstall come uno snap-in.</span><span class="sxs-lookup"><span data-stu-id="34120-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="34120-183">Si noti che questa versione supportata ufficialmente sostituisce versione precedente di hello è disponibile in CodePlex, anche se le versioni precedenti di hello numero 2.</span><span class="sxs-lookup"><span data-stu-id="34120-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="34120-184">Avviare PowerShell di Azure utilizzando il menu di avvio hello o alla pagina iniziale.</span><span class="sxs-lookup"><span data-stu-id="34120-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="34120-185">Se si avvia in questo modo, verrà caricato hello cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34120-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="34120-186">Al prompt dei comandi PowerShell hello, verificare che i cmdlet di PowerShell hello vengono caricati con comando parziale hello `Get-Azure` e quindi premere il tasto Tab per il completamento delle istruzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="34120-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="34120-187">Se si preme tasto Tab hello ripetutamente, vedrai vari comandi di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="34120-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="34120-188">Verificare che sia possibile connettersi tooyour sottoscrizione di Azure importando le informazioni di sottoscrizione da file con estensione publishsettings hello.</span><span class="sxs-lookup"><span data-stu-id="34120-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="34120-189">Quindi immettere il comando hello</span><span class="sxs-lookup"><span data-stu-id="34120-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="34120-190">Vengono visualizzate le informazioni relative alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="34120-190">This shows information about your subscription.</span></span> <span data-ttu-id="34120-191">Verificarne la correttezza.</span><span class="sxs-lookup"><span data-stu-id="34120-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="34120-192">Salvare il modello di script hello fornito alla fine di hello di questo articolo per la cartella di script come c:\\script\\Azure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="34120-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="34120-193">Nella sezione hello parametri dello script hello.</span><span class="sxs-lookup"><span data-stu-id="34120-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="34120-194">Aggiungere o modificare i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="34120-194">Add or modify any default values.</span></span> <span data-ttu-id="34120-195">Questi valori possono sempre essere sostituiti mediante il passaggio di parametri espliciti.</span><span class="sxs-lookup"><span data-stu-id="34120-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="34120-196">Verificare che esistono in modo univoco il servizio cloud valido e gli account di archiviazione creati nella sottoscrizione che può essere la destinazione hello dello script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="34120-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="34120-197">L'account di archiviazione (archiviazione blob) verrà utilizzato tooupload e archiviare temporaneamente i file di pacchetto e i file di configurazione della distribuzione hello durante la creazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="34120-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="34120-198">toocreate un nuovo servizio cloud, è possibile chiamare questo script o l'utilizzo di hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34120-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="34120-199">nome del servizio cloud Hello verrà utilizzato come un prefisso in un nome di dominio completo e pertanto deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="34120-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="34120-200">toocreate un nuovo account di archiviazione, è possibile chiamare questo script o l'utilizzo di hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34120-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="34120-201">nome account di archiviazione Hello verrà utilizzato come un prefisso in un nome di dominio completo e pertanto deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="34120-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="34120-202">È possibile provare a utilizzare hello stesso nome del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="34120-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="34120-203">Chiamare lo script hello direttamente da Azure PowerShell o associare questa automazione toooccur generazione di script tooyour host dopo la compilazione del pacchetto hello.</span><span class="sxs-lookup"><span data-stu-id="34120-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="34120-204">script Hello sempre eliminerà o sostituire le distribuzioni esistenti per impostazione predefinita, se vengono rilevati.</span><span class="sxs-lookup"><span data-stu-id="34120-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="34120-205">Questo è necessario per consentire il recapito continuo da automazioni in cui non è possibile visualizzare richieste utente.</span><span class="sxs-lookup"><span data-stu-id="34120-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="34120-206">**Scenario di esempio 1:** toohello distribuzione continua l'ambiente di un servizio di gestione temporanea:</span><span class="sxs-lookup"><span data-stu-id="34120-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="34120-207">Questo è in genere seguito da verifica tramite esecuzione di test e da uno scambio di indirizzi VIP.</span><span class="sxs-lookup"><span data-stu-id="34120-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="34120-208">scambio VIP Hello può essere eseguito tramite hello [portale di Azure](https://portal.azure.com) o con cmdlet hello Move-distribuzione.</span><span class="sxs-lookup"><span data-stu-id="34120-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="34120-209">**Scenario di esempio 2:** ambiente di produzione toohello distribuzione continua di un servizio di test dedicato</span><span class="sxs-lookup"><span data-stu-id="34120-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="34120-210">**Desktop remoto:**</span><span class="sxs-lookup"><span data-stu-id="34120-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="34120-211">Se Desktop remoto sia abilitato nel progetto Azure, è necessario tooperform ulteriori passaggi monouso hello tooensure che corretto certificato del servizio Cloud è caricato tooall servizi di cloud di destinazione da questo script.</span><span class="sxs-lookup"><span data-stu-id="34120-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="34120-212">Individuare i valori di identificazione personale certificato hello previsti dai ruoli.</span><span class="sxs-lookup"><span data-stu-id="34120-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="34120-213">I valori di identificazione personale sono visibili nella sezione relativa ai certificati hello del file di configurazione cloud (ad esempio ServiceConfiguration).</span><span class="sxs-lookup"><span data-stu-id="34120-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="34120-214">È inoltre visibile nella finestra di dialogo Configurazione Desktop remoto hello in Visual Studio quando si hello Mostra opzioni e di visualizzazione selezionato alcun certificato.</span><span class="sxs-lookup"><span data-stu-id="34120-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="34120-215">Caricare i certificati di Desktop remoto come un passaggio di installazione singola utilizzando hello lo script di cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="34120-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="34120-216">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="34120-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="34120-217">In alternativa è possibile esportare il file di certificato hello PFX con chiave privata e caricare i certificati tooeach servizio di destinazione cloud con il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34120-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="34120-218">**Aggiorna distribuzione ed Elimina distribuzione -** Nuova distribuzione\></span><span class="sxs-lookup"><span data-stu-id="34120-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="34120-219">Hello script per impostazione predefinita esegue un aggiornamento della distribuzione ($enableDeploymentUpgrade = 1) quando non viene passato alcun parametro o il valore 1 viene passato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="34120-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="34120-220">Per singole istanze, questo ha il vantaggio di richiedere meno tempo rispetto a una distribuzione completa.</span><span class="sxs-lookup"><span data-stu-id="34120-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="34120-221">Per le istanze che richiedono disponibilità elevata, che ciò presenta inoltre il vantaggio di hello di lasciare alcune istanze in esecuzione mentre altri vengono aggiornate (esame del dominio di aggiornamento), nonché il VIP non verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="34120-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="34120-222">Distribuzione dell'aggiornamento può essere disabilitata in script hello ($enableDeploymentUpgrade = 0) o passando *- enableDeploymentUpgrade 0* come parametro, che modifica l'eliminazione di script comportamento toofirst qualsiasi distribuzione esistente e quindi creare un nuova distribuzione.</span><span class="sxs-lookup"><span data-stu-id="34120-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="34120-223">script Hello sempre eliminerà o sostituire le distribuzioni esistenti per impostazione predefinita, se vengono rilevati.</span><span class="sxs-lookup"><span data-stu-id="34120-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="34120-224">Questo è necessario per consentire il recapito continuo da automazioni in cui non è possibile visualizzare richieste utente/operatore.</span><span class="sxs-lookup"><span data-stu-id="34120-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="34120-225">5: Pubblicare un pacchetto usando TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="34120-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="34120-226">Questo passaggio facoltativo si connette a Team di TFS Build toohello script creato nel passaggio 4, che gestisce la pubblicazione di hello pacchetto compilazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="34120-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="34120-227">Ciò comporta hello modifica modello di processo usato per la definizione di compilazione in modo che venga eseguito un'attività di pubblicazione alla fine del flusso di lavoro hello hello.</span><span class="sxs-lookup"><span data-stu-id="34120-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="34120-228">Hello pubblica attività eseguirà il comando di PowerShell passando i parametri dalla compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="34120-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="34120-229">Nell'output di compilazione standard di hello verrà inoltrato tramite pipe l'output di hello ha come destinazione di MSBuild e script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="34120-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="34120-230">Modifica hello responsabile della definizione di compilazione continua distribuire.</span><span class="sxs-lookup"><span data-stu-id="34120-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="34120-231">Seleziona hello **processo** scheda.</span><span class="sxs-lookup"><span data-stu-id="34120-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="34120-232">Seguire [queste istruzioni](http://msdn.microsoft.com/library/dd647551.aspx) tooadd un progetto di attività per hello modello di processo di compilazione, scaricare il modello predefinito di hello, aggiungerlo al progetto hello e archiviarlo.</span><span class="sxs-lookup"><span data-stu-id="34120-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="34120-233">Assegnare un nuovo nome, ad esempio AzureBuildProcessTemplate di modello di processo di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="34120-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="34120-234">Restituire toohello **processo** scheda e utilizzare **Mostra dettagli** tooshow un elenco dei modelli di processo di compilazione disponibile.</span><span class="sxs-lookup"><span data-stu-id="34120-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="34120-235">Scegliere hello **New...**  pulsante e passare toohello progetto appena aggiunto e archiviato.</span><span class="sxs-lookup"><span data-stu-id="34120-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="34120-236">Individuare il modello di hello appena creato e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="34120-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="34120-237">Aprire hello selezionato del modello di processo per la modifica.</span><span class="sxs-lookup"><span data-stu-id="34120-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="34120-238">È possibile aprire direttamente nella finestra di progettazione del flusso di lavoro hello o toowork editor XML di hello con hello XAML.</span><span class="sxs-lookup"><span data-stu-id="34120-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="34120-239">Aggiungere hello seguente elenco di nuovi argomenti come elementi distinti di riga nella scheda argomenti hello della finestra di progettazione del flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="34120-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="34120-240">Tutti gli argomenti devono presentare direction=In e type=String.</span><span class="sxs-lookup"><span data-stu-id="34120-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="34120-241">Questi saranno i parametri utilizzati tooflow dalla definizione di compilazione hello in hello del flusso di lavoro, che quindi hello toocall utilizzato get dello script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="34120-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Elenco di argomenti][3]

   <span data-ttu-id="34120-243">Hello che XAML corrispondente è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="34120-243">hello corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="34120-244">Aggiungere una nuova sequenza alla fine hello Esegui su agente:</span><span class="sxs-lookup"><span data-stu-id="34120-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="34120-245">Per iniziare, aggiungere un toocheck attività istruzione If per un file di script valido.</span><span class="sxs-lookup"><span data-stu-id="34120-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="34120-246">Impostare il valore toothis della condizione hello:</span><span class="sxs-lookup"><span data-stu-id="34120-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="34120-247">In hello quindi i case di hello istruzione If, aggiungere una nuova attività di sequenza.</span><span class="sxs-lookup"><span data-stu-id="34120-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="34120-248">Pubblicare set hello visualizzazione nome too'Start'</span><span class="sxs-lookup"><span data-stu-id="34120-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="34120-249">Con hello inizio pubblicare sequenza ancora selezionato, aggiungere il seguente elenco di nuove variabili come elementi distinti di riga nella scheda variabili della finestra di progettazione del flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="34120-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="34120-250">Tutte le variabili presentare Variable type =String e Scope=Start publish.</span><span class="sxs-lookup"><span data-stu-id="34120-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="34120-251">Questi saranno i parametri utilizzati tooflow dalla definizione di compilazione hello nel flusso di lavoro, che quindi hello toocall utilizzato get dello script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="34120-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="34120-252">SubscriptionDataFilePath, di tipo String</span><span class="sxs-lookup"><span data-stu-id="34120-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="34120-253">PublishScriptFilePath, di tipo String</span><span class="sxs-lookup"><span data-stu-id="34120-253">PublishScriptFilePath, of type String</span></span>

        ![Nuove variabili][4]
   4. <span data-ttu-id="34120-255">Se si usa TFS 2012 o versioni precedenti, aggiungere un'attività di ConvertWorkspaceItem inizio hello hello nuova sequenza.</span><span class="sxs-lookup"><span data-stu-id="34120-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="34120-256">Se si usa TFS 2013 o versioni successive, è possibile aggiungere un'attività GetLocalPath all'inizio di hello della nuova sequenza di hello.</span><span class="sxs-lookup"><span data-stu-id="34120-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="34120-257">Per un ConvertWorkspaceItem, impostare la proprietà hello come segue: direzione = ServerToLocal, DisplayName = 'Convert publish nome file di script,' Input 'PublishScriptLocation', risultato = = 'PublishScriptFilePath', area di lavoro = 'Area di lavoro'.</span><span class="sxs-lookup"><span data-stu-id="34120-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="34120-258">Per un'attività GetLocalPath, impostare hello proprietà IncomingPath too'PublishScriptLocation', e hello too'PublishScriptFilePath risultati '.</span><span class="sxs-lookup"><span data-stu-id="34120-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="34120-259">Questo percorso toohello di attività converte hello script da percorsi di TFS server di pubblicazione (se applicabile) percorso del disco locale standard tooa.</span><span class="sxs-lookup"><span data-stu-id="34120-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="34120-260">Se si usa TFS 2012 o versioni precedenti, aggiungere un'altra attività di ConvertWorkspaceItem alla fine hello hello nuova sequenza.</span><span class="sxs-lookup"><span data-stu-id="34120-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="34120-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="34120-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="34120-262">Se si usa TFS 2013 o versione successiva, aggiungere un'altra attività GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="34120-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="34120-263">IncomingPath='SubscriptionDataFileLocation' e Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="34120-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="34120-264">Aggiungere un'attività InvokeProcess alla fine hello hello nuova sequenza.</span><span class="sxs-lookup"><span data-stu-id="34120-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="34120-265">Questo chiama attività PowerShell.exe con argomenti hello passato dal hello definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="34120-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="34120-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="34120-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="34120-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="34120-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="34120-268">FileName = "PowerShell" (che includono le offerte di hello)</span><span class="sxs-lookup"><span data-stu-id="34120-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="34120-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="34120-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="34120-270">In hello **Gestisci Output Standard** sezione casella di testo del InvokeProcess, impostare hello casella di testo valore too'data'.</span><span class="sxs-lookup"><span data-stu-id="34120-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="34120-271">Si tratta di dati di output standard una variabile toostore hello.</span><span class="sxs-lookup"><span data-stu-id="34120-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="34120-272">Aggiungere un'attività WriteBuildMessage di sotto hello **Gestisci Output Standard** sezione.</span><span class="sxs-lookup"><span data-stu-id="34120-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="34120-273">Impostare hello importanza = 'BuildMessageImportance' e messaggio hello = 'data'.</span><span class="sxs-lookup"><span data-stu-id="34120-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="34120-274">In questo modo l'output standard di hello dello script verranno scritte toohello l'output di compilazione.</span><span class="sxs-lookup"><span data-stu-id="34120-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="34120-275">In hello **Gestisci Output errore** sezione casella di testo del InvokeProcess, impostare hello casella di testo valore too'data'.</span><span class="sxs-lookup"><span data-stu-id="34120-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="34120-276">Si tratta di un dati di errore standard hello toostore variabile.</span><span class="sxs-lookup"><span data-stu-id="34120-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="34120-277">Aggiungere un'attività WriteBuildError sotto hello **Gestisci Output errore** sezione.</span><span class="sxs-lookup"><span data-stu-id="34120-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="34120-278">Impostare hello messaggio = 'data'.</span><span class="sxs-lookup"><span data-stu-id="34120-278">Set hello Message='data'.</span></span> <span data-ttu-id="34120-279">In questo modo verranno scritti hello standard errori di script hello output degli errori di compilazione toohello.</span><span class="sxs-lookup"><span data-stu-id="34120-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="34120-280">Correggere eventuali errori, indicati da punti esclamativi blu.</span><span class="sxs-lookup"><span data-stu-id="34120-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="34120-281">Passare il puntatore di tooget punti esclamativi un suggerimento su errore hello.</span><span class="sxs-lookup"><span data-stu-id="34120-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="34120-282">Salva flusso di lavoro di hello per cancellare gli errori.</span><span class="sxs-lookup"><span data-stu-id="34120-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="34120-283">risultato finale di Hello di hello pubblicazione del flusso di lavoro attività saranno simile al seguente nella finestra di progettazione hello:</span><span class="sxs-lookup"><span data-stu-id="34120-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![Attività flusso di lavoro][5]

   <span data-ttu-id="34120-285">risultato finale di Hello di hello pubblicare attività saranno simile al seguente in XAML del flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="34120-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="34120-286">Salvare un flusso di lavoro modello processo compilazione hello e archivia il file.</span><span class="sxs-lookup"><span data-stu-id="34120-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="34120-287">Modificare la definizione di compilazione hello (chiuderla se è già aperto) e seleziona hello **New** pulsante se non viene ancora visualizzato nuovo modello di hello nell'elenco di hello dei modelli di processo.</span><span class="sxs-lookup"><span data-stu-id="34120-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="34120-288">Impostare i valori delle proprietà parametro hello hello sezione varie nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="34120-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="34120-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Questo valore deriva da: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="34120-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="34120-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Questo valore deriva da: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="34120-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="34120-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="34120-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="34120-292">ServiceName = 'mycloudservicename' *utilizzare hello appropriato nome del servizio cloud qui*</span><span class="sxs-lookup"><span data-stu-id="34120-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="34120-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="34120-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="34120-294">StorageAccountName = 'mystorageaccountname' *nome account di uso hello appropriato archiviazione qui*</span><span class="sxs-lookup"><span data-stu-id="34120-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="34120-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="34120-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="34120-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="34120-296">SubscriptionName = 'default'</span></span>

    ![Valori delle proprietà dei parametri][6]
11. <span data-ttu-id="34120-298">Salvare le modifiche di hello toohello definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="34120-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="34120-299">Accodare una compilazione tooexecute entrambi hello build del pacchetto e pubblicare.</span><span class="sxs-lookup"><span data-stu-id="34120-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="34120-300">Se si dispone di un trigger tooContinuous integrazione impostato, questo comportamento verrà eseguita a ogni archiviazione.</span><span class="sxs-lookup"><span data-stu-id="34120-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="34120-301">Modello di script PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="34120-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="34120-302">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34120-302">Next steps</span></span>
<span data-ttu-id="34120-303">debug remoto tooenable quando si utilizza il recapito continuo, vedere [abilitare il debug remoto quando si utilizza il recapito continuo toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="34120-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
