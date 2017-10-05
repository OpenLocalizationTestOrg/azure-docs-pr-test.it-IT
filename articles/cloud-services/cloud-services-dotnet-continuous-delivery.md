---
title: Recapito continuo per Servizi cloud con TFS in Azure | Documentazione Microsoft
description: Informazioni sulla configurazione del recapito continuo per le app cloud di Azure. Esempi di codice Code per istruzioni della riga di comando MSBuild e script di PowerShell.
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
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="f039f-104">Recapito continuo per Servizi cloud in Azure</span><span class="sxs-lookup"><span data-stu-id="f039f-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="f039f-105">Nel processo descritto in questo articolo viene illustrato come configurare il recapito continuo per le app cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="f039f-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="f039f-106">Questa procedura crea automaticamente e distribuisce pacchetti in Azure dopo ogni archiviazione di codice.</span><span class="sxs-lookup"><span data-stu-id="f039f-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="f039f-107">Il processo di compilazione del pacchetto descritto in questo articolo è equivalente al comando **Pacchetto** di Visual Studio, mentre i passaggi per la pubblicazione equivalgono al comando **Pubblica** di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f039f-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="f039f-108">L'articolo riguarda i metodi da usare per creare un server di compilazione con istruzioni da riga di comando di MSBuild e script di Windows PowerShell. Viene inoltre illustrato come configurare, facoltativamente, definizioni di Visual Studio Team Foundation Server - Team Build per usare i comandi di MSBuild e gli script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f039f-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="f039f-109">Il processo è personalizzabile per il proprio ambiente di compilazione e per gli ambienti Azure di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="f039f-110">Per agevolare tali operazioni è inoltre disponibile Visual Studio Team Services, una versione di TFS ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="f039f-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="f039f-111">Prima di iniziare, pubblicare l'applicazione da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f039f-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="f039f-112">Questo garantisce che tutte le risorse siano disponibili e inizializzate quando si tenta di automatizzare il processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="f039f-113">1: Configurare il server di compilazione</span><span class="sxs-lookup"><span data-stu-id="f039f-113">1: Configure the Build Server</span></span>
<span data-ttu-id="f039f-114">Prima di creare un pacchetto di Azure usando MSBuild, è necessario installare il software e gli strumenti necessari nel server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="f039f-115">L'installazione di Visual Studio nel server di compilazione non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="f039f-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="f039f-116">Per usare il servizio Team Foundation Build per gestire il server di compilazione, seguire le istruzioni riportate nella documentazione del [servizio Team Foundation Build][Team Foundation Build Service].</span><span class="sxs-lookup"><span data-stu-id="f039f-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="f039f-117">Nel server di compilazione installare [.NET Framework 4.5.2][.NET Framework 4.5.2], che include MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f039f-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="f039f-118">Installare la versione più recente [Strumenti di creazione di Azure per .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="f039f-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="f039f-119">Installare le [Librerie di Azure per .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="f039f-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="f039f-120">Copiare il file Microsoft.WebApplication.targets da un'installazione di Visual Studio al server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="f039f-121">In un computer in cui è installato Visual Studio, questo file si trova nella directory \\Program Files (x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="f039f-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="f039f-122">Copiare il file nella stessa cartella del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="f039f-123">Installare gli [strumenti di Azure per Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="f039f-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="f039f-124">2: Compilare un pacchetto usando i comandi MSBuild</span><span class="sxs-lookup"><span data-stu-id="f039f-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="f039f-125">Questa sezione descrive come creare un comando MSBuild per compilare un pacchetto di Azure.</span><span class="sxs-lookup"><span data-stu-id="f039f-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="f039f-126">Eseguire questo passaggio nel server di compilazione per verificare che tutto sia configurato correttamente e che il comando MSBuild abbia l'effetto desiderato.</span><span class="sxs-lookup"><span data-stu-id="f039f-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="f039f-127">È possibile aggiungere questa riga di comando agli script di compilazione esistenti nel server di compilazione oppure è possibile usare la riga di comando in una definizione di compilazione di TFS, come descritto nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="f039f-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="f039f-128">Per altre informazioni sui parametri della riga di comando e su MSBuild, vedere [Riferimenti alla riga di comando di MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f039f-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="f039f-129">Se Visual Studio è installato nel server di compilazione, trovare e scegliere **Prompt dei comandi di Visual Studio** nella cartella **Strumenti di Visual Studio** in Windows.</span><span class="sxs-lookup"><span data-stu-id="f039f-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="f039f-130">Se Visual Studio non è installato nel server di compilazione, aprire un prompt dei comandi e verificare che MSBuild.exe sia accessibile nel percorso.</span><span class="sxs-lookup"><span data-stu-id="f039f-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="f039f-131">MSBuild viene installato con .NET Framework nel percorso %WINDIR%\\Microsoft.NET\\Framework\\*Versione*.</span><span class="sxs-lookup"><span data-stu-id="f039f-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="f039f-132">Per aggiungere MSBuild.exe alla variabile di ambiente PATH quando .NET Framework 4 è stato installato, ad esempio, digitare il comando seguente al prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="f039f-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="f039f-133">Dal prompt dei comandi, passare alla cartella contenente il file del progetto di Azure che si desidera compilare.</span><span class="sxs-lookup"><span data-stu-id="f039f-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="f039f-134">Eseguire MSbuild con l'opzione /target:Publish come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f039f-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="f039f-135">Per questa opzione è possibile usare la sintassi abbreviata /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="f039f-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="f039f-136">Quando è installato Azure SDK, l'opzione /t:Publish in MSBuild non va confusa con i comandi di pubblicazione disponibili in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f039f-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="f039f-137">L'opzione /t:Publish compila unicamente pacchetti di Azure</span><span class="sxs-lookup"><span data-stu-id="f039f-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="f039f-138">ma non li distribuisce come accade con i comandi di pubblicazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f039f-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="f039f-139">Facoltativamente, è possibile specificare il nome del progetto come parametro di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f039f-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="f039f-140">Se non specificato, viene usata la directory corrente.</span><span class="sxs-lookup"><span data-stu-id="f039f-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="f039f-141">Per altre informazioni sulle opzioni della riga di comando di MSBuild, vedere [Riferimenti alla riga di comando di MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f039f-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="f039f-142">Individuare l'output.</span><span class="sxs-lookup"><span data-stu-id="f039f-142">Locate the output.</span></span> <span data-ttu-id="f039f-143">Per impostazione predefinita, questo comando crea una directory in relazione alla cartella radice del progetto, ad esempio *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span><span class="sxs-lookup"><span data-stu-id="f039f-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="f039f-144">Quando si compila un progetto Azure, vengono generati due file, il file del pacchetto e il file di configurazione di accompagnamento:</span><span class="sxs-lookup"><span data-stu-id="f039f-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="f039f-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="f039f-145">Project.cspkg</span></span>
   * <span data-ttu-id="f039f-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="f039f-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="f039f-147">Per impostazione predefinita, ogni progetto Azure include un file di configurazione del servizio (file con estensione cscfg) per compilazioni locali (debug) e un altro per le compilazioni nel cloud (gestione temporanea o produzione), ma è possibile aggiungere o rimuovere file di configurazione del servizio in base alle necessità.</span><span class="sxs-lookup"><span data-stu-id="f039f-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="f039f-148">Quando si compila un pacchetto all'interno di Visual Studio, verrà chiesto quale file di configurazione del servizio includere insieme al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f039f-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="f039f-149">Specificare il file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="f039f-149">Specify the service configuration file.</span></span> <span data-ttu-id="f039f-150">Quando si compila un pacchetto usando MSBuild, il file di configurazione del servizio locale viene incluso per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f039f-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="f039f-151">Per includere un file di configurazione del servizio diverso, impostare la proprietà TargetProfile del comando MSBuild, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f039f-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="f039f-152">Specificare il percorso per l'output.</span><span class="sxs-lookup"><span data-stu-id="f039f-152">Specify the location for the output.</span></span> <span data-ttu-id="f039f-153">Impostare il percorso usando l'opzione /p:PublishDir=*Directory*\\, compreso il separatore barra rovesciata finale, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f039f-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="f039f-154">Una volta creata e testata una riga di comando di MSBuild appropriata per compilare i progetti e combinarli in un pacchetto di Azure, è possibile aggiungere tale riga di comando agli script di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="f039f-155">Se il server di compilazione usa script personalizzati, questo processo dipende dalle specifiche del processo personalizzato di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="f039f-156">Se si usa TFS come ambiente di compilazione, è possibile seguire le istruzioni nel prossimo passaggio per aggiungere la compilazione del pacchetto di Azure al proprio processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="f039f-157">3: Compilare un pacchetto usando TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="f039f-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="f039f-158">Se si dispone di Team Foundation Server (TFS) configurato come controller di compilazione, e il server di compilazione è impostato come computer di compilazione TFS, è possibile configurare facoltativamente una compilazione automatica per il pacchetto Azure.</span><span class="sxs-lookup"><span data-stu-id="f039f-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="f039f-159">Per informazioni su come configurare e usare Team Foundation Server come sistema di compilazione, vedere [Aumentare il numero di istanze del sistema di compilazione][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="f039f-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="f039f-160">In particolare, nella procedura seguente si presuppone che il server di compilazione sia stato configurato come descritto in [Distribuire e configurare un server di compilazione][Deploy and configure a build server] e che siano stati creati un progetto team e un progetto servizio cloud nel progetto team.</span><span class="sxs-lookup"><span data-stu-id="f039f-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="f039f-161">Per configurare TFS per la compilazione di pacchetti Azure, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f039f-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="f039f-162">In Visual Studio, nel computer di sviluppo, scegliere **Team Explorer** dal menu Visualizza oppure premere Ctrl+\\, Ctrl+M.</span><span class="sxs-lookup"><span data-stu-id="f039f-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="f039f-163">Nella finestra di Team Explorer espandere il nodo **Compilazioni** o scegliere la pagina **Compilazioni** e fare clic su **Nuova definizione di compilazione**.</span><span class="sxs-lookup"><span data-stu-id="f039f-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![Opzione Nuova definizione di compilazione][0]
2. <span data-ttu-id="f039f-165">Selezionare la scheda **Trigger** e specificare le condizioni desiderate relativamente al momento in cui si desidera che il pacchetto venga creato.</span><span class="sxs-lookup"><span data-stu-id="f039f-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="f039f-166">Specificare **Integrazione continuata** per compilare il pacchetto ogni volta che ha luogo un'archiviazione del controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="f039f-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="f039f-167">Scegliere la scheda **Impostazioni di origine** e verificare che la cartella del progetto sia elencata nella colonna **Cartella del controllo del codice sorgente** e che lo stato sia **Attivo**.</span><span class="sxs-lookup"><span data-stu-id="f039f-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="f039f-168">Scegliere la scheda **Impostazioni predefinite compilazione** e, in Controller di compilazione, verificare il nome del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="f039f-169">Scegliere anche l'opzione **Copia output di compilazione nella seguente cartella di ricezione** e specificare la destinazione finale desiderata.</span><span class="sxs-lookup"><span data-stu-id="f039f-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="f039f-170">Selezionare la scheda **Processo** . Nella scheda Processo scegliere il modello predefinito in **Compilazione**, scegliere il progetto se non è già selezionato ed espandere la sezione **Avanzate** nella sezione **Compilazione** della griglia.</span><span class="sxs-lookup"><span data-stu-id="f039f-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="f039f-171">Scegliere **Argomenti MSBuild**e impostare gli argomenti della riga di comando MSBuild appropriati come descritto al precedente punto 2.</span><span class="sxs-lookup"><span data-stu-id="f039f-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="f039f-172">Immettere ad esempio **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** per compilare un pacchetto e copiare i relativi file nel percorso \\\\myserver\\drops\\:</span><span class="sxs-lookup"><span data-stu-id="f039f-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![Argomenti MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="f039f-174">la copia dei file in una condivisione pubblica semplifica la distribuzione manuale dei pacchetti dal computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="f039f-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="f039f-175">Verificare l'esito del passaggio di compilazione archiviando una modifica al progetto o inserire in coda una nuova compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="f039f-176">Per inserire in coda una nuova compilazione, in Team Explorer fare clic con il pulsante destro del mouse su **Tutte le definizioni di compilazione**, quindi scegliere **Accoda nuova compilazione**.</span><span class="sxs-lookup"><span data-stu-id="f039f-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="f039f-177">4: Pubblicare un pacchetto usando uno script PowerShell</span><span class="sxs-lookup"><span data-stu-id="f039f-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="f039f-178">In questa sezione viene descritto come creare uno script di Windows PowerShell che pubblicherà l'output del pacchetto dell'app per cloud in Azure usando parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="f039f-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="f039f-179">Questo script può essere chiamato dopo il passaggio di compilazione nell'automazione della compilazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="f039f-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="f039f-180">È possibile chiamare lo script anche da attività del flusso di lavoro del modello di processo in Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="f039f-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="f039f-181">Installare i [cmdlet di Azure PowerShell][Azure PowerShell cmdlets] (0.6.1 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="f039f-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="f039f-182">Durante la fase di installazione dei cmdlet, scegliere l'installazione come snap-in.</span><span class="sxs-lookup"><span data-stu-id="f039f-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="f039f-183">Si noti che questa versione ufficialmente supportata sostituisce la versione precedente offerta tramite CodePlex, anche se le versioni precedenti sono state numerate 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="f039f-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="f039f-184">Avviare Azure PowerShell usando il menu o la pagina Start.</span><span class="sxs-lookup"><span data-stu-id="f039f-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="f039f-185">Con l'avvio in questa modalità, verranno caricati i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f039f-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="f039f-186">Al prompt di PowerShell, verificare che i cmdlet di PowerShell sono caricati immettendo il comando parziale `Get-Azure` , quindi premendo il tasto TAB per il completamento.</span><span class="sxs-lookup"><span data-stu-id="f039f-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="f039f-187">Premendo il tasto TAB ripetutamente, verranno visualizzati diversi comandi di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f039f-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="f039f-188">Verificare che sia possibile connettersi alla propria sottoscrizione Azure importando le proprie informazioni di sottoscrizione dal file con estensione .publishsettings come segue:</span><span class="sxs-lookup"><span data-stu-id="f039f-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="f039f-189">Quindi immettere il comando</span><span class="sxs-lookup"><span data-stu-id="f039f-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="f039f-190">Vengono visualizzate le informazioni relative alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f039f-190">This shows information about your subscription.</span></span> <span data-ttu-id="f039f-191">Verificarne la correttezza.</span><span class="sxs-lookup"><span data-stu-id="f039f-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="f039f-192">Salvare il modello di script fornito alla fine di questo articolo nella cartella degli script, ad esempio c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="f039f-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="f039f-193">Rivedere la sezione dello script relativa ai parametri.</span><span class="sxs-lookup"><span data-stu-id="f039f-193">Review the parameters section of the script.</span></span> <span data-ttu-id="f039f-194">Aggiungere o modificare i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="f039f-194">Add or modify any default values.</span></span> <span data-ttu-id="f039f-195">Questi valori possono sempre essere sostituiti mediante il passaggio di parametri espliciti.</span><span class="sxs-lookup"><span data-stu-id="f039f-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="f039f-196">Assicurarsi che siano presenti account validi per i servizi cloud e di archiviazione creati nella sottoscrizione a cui lo script sia in grado di fare riferimento.</span><span class="sxs-lookup"><span data-stu-id="f039f-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="f039f-197">L'account di archiviazione (archiviazione BLOB) verrà usato per caricare e archiviare temporaneamente il pacchetto di distribuzione e il file di configurazione durante la creazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f039f-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="f039f-198">Per creare un nuovo servizio cloud, è possibile chiamare questo script o usare il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f039f-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f039f-199">Il nome del servizio cloud verrà usato come prefisso di un nome di dominio completo e deve pertanto essere univoco.</span><span class="sxs-lookup"><span data-stu-id="f039f-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="f039f-200">Per creare un nuovo account di archiviazione, è possibile chiamare questo script o usare il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f039f-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f039f-201">Il nome dell'account di archiviazione verrà usato come prefisso di un nome di dominio completo e deve pertanto essere univoco.</span><span class="sxs-lookup"><span data-stu-id="f039f-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="f039f-202">È possibile provare a usare lo stesso nome come del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="f039f-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="f039f-203">Chiamare lo script direttamente da Azure PowerShell o collegarlo all'automazione delle compilazioni dell'host in uso in modo che venga eseguito dopo la compilazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f039f-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f039f-204">se vengono rilevate distribuzioni esistenti, lo script le elimina o le sostituisce per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f039f-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="f039f-205">Questo è necessario per consentire il recapito continuo da automazioni in cui non è possibile visualizzare richieste utente.</span><span class="sxs-lookup"><span data-stu-id="f039f-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="f039f-206">**Scenario di esempio 1** : distribuzione continua di un servizio nell'ambiente di gestione temporanea:</span><span class="sxs-lookup"><span data-stu-id="f039f-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="f039f-207">Questo è in genere seguito da verifica tramite esecuzione di test e da uno scambio di indirizzi VIP.</span><span class="sxs-lookup"><span data-stu-id="f039f-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="f039f-208">Tale scambio di indirizzi VIP può essere eseguito nel [portale di Azure](https://portal.azure.com) o con il cmdlet Move-Deployment.</span><span class="sxs-lookup"><span data-stu-id="f039f-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="f039f-209">**Scenario di esempio 2** : distribuzione continua di un servizio di test dedicato nell'ambiente di produzione</span><span class="sxs-lookup"><span data-stu-id="f039f-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="f039f-210">**Desktop remoto:**</span><span class="sxs-lookup"><span data-stu-id="f039f-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="f039f-211">Se Desktop remoto è abilitato nel progetto Azure, sarà necessario eseguire passaggi aggiuntivi una tantum per assicurarsi che il corretto certificato di servizio cloud venga caricato in tutti i servizi cloud che questo script ha come destinazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="f039f-212">Individuare i valori di identificazione personale del certificato previsti dai ruoli in uso.</span><span class="sxs-lookup"><span data-stu-id="f039f-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="f039f-213">I valori di identificazione personale sono visibili nella sezione Certificati del file config cloud (ovvero ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="f039f-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="f039f-214">Sono inoltre visibili nella finestra di dialogo di configurazione di Desktop remoto in Visual Studio quando si accede alle opzioni e si visualizza il certificato selezionato.</span><span class="sxs-lookup"><span data-stu-id="f039f-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="f039f-215">Caricare i certificati di Desktop remoto come passaggio di installazione una tantum usando lo script di cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="f039f-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="f039f-216">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f039f-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="f039f-217">In alternativa è possibile esportare il file di certificato PFX con la chiave privata e caricare i certificati in ogni servizio cloud di destinazione tramite il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f039f-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="f039f-218">**Aggiorna distribuzione ed Elimina distribuzione -** Nuova distribuzione\></span><span class="sxs-lookup"><span data-stu-id="f039f-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="f039f-219">Per impostazione predefinita, questo script esegue un aggiornamento della distribuzione ($enableDeploymentUpgrade = 1) quando non viene passato alcun parametro o quando 1 viene passato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="f039f-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="f039f-220">Per singole istanze, questo ha il vantaggio di richiedere meno tempo rispetto a una distribuzione completa.</span><span class="sxs-lookup"><span data-stu-id="f039f-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="f039f-221">Per istanze che richiedono un'elevata disponibilità, vi è inoltre il vantaggio del mantenimento di alcune istanze in esecuzione mentre altre vengono aggiornate (enumerazione del dominio di aggiornamento). L'indirizzo VIP, inoltre, non verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="f039f-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="f039f-222">L'aggiornamento della distribuzione può essere disabilitato nello script ($enableDeploymentUpgrade = 0) oppure passando *- enableDeploymentUpgrade 0* come parametro, il che modifica il comportamento dello script in modo che questo elimini innanzitutto qualsiasi distribuzione esistente e quindi ne crei una nuova.</span><span class="sxs-lookup"><span data-stu-id="f039f-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f039f-223">se vengono rilevate distribuzioni esistenti, lo script le elimina o le sostituisce per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f039f-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="f039f-224">Questo è necessario per consentire il recapito continuo da automazioni in cui non è possibile visualizzare richieste utente/operatore.</span><span class="sxs-lookup"><span data-stu-id="f039f-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="f039f-225">5: Pubblicare un pacchetto usando TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="f039f-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="f039f-226">In questo passaggio facoltativo si collega TFS Team Build con lo script creato nel passaggio 4, che gestisce la pubblicazione della compilazione del pacchetto in Azure.</span><span class="sxs-lookup"><span data-stu-id="f039f-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="f039f-227">Questo comporta la modifica del modello di processo usato dalla definizione di compilazione in modo che venga eseguita un'attività di pubblicazione al termine del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f039f-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="f039f-228">L'attività di pubblicazione eseguirà il comando PowerShell passando i parametri dalla compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="f039f-229">L'output delle destinazioni di MSBuild e dello script di pubblicazione verrà inviato all'output standard della compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="f039f-230">Modificare la definizione di compilazione responsabile della distribuzione continua.</span><span class="sxs-lookup"><span data-stu-id="f039f-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="f039f-231">Selezionare la scheda **Processo** .</span><span class="sxs-lookup"><span data-stu-id="f039f-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="f039f-232">Seguire [queste istruzioni](http://msdn.microsoft.com/library/dd647551.aspx) per aggiungere un progetto di attività per il modello di processo di compilazione, scaricare il modello predefinito, aggiungerlo al progetto e archiviarlo.</span><span class="sxs-lookup"><span data-stu-id="f039f-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="f039f-233">Assegnare un nuovo nome al modello di processo di compilazione, ad esempio AzureBuildProcessTemplate.</span><span class="sxs-lookup"><span data-stu-id="f039f-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="f039f-234">Tornare alla scheda **Processo** e usare **Mostra dettagli** per visualizzare un elenco dei modelli di processo di compilazione disponibili.</span><span class="sxs-lookup"><span data-stu-id="f039f-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="f039f-235">Scegliere il pulsante **Nuovo** e passare al progetto appena aggiunto e archiviato.</span><span class="sxs-lookup"><span data-stu-id="f039f-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="f039f-236">Individuare il modello appena creato e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="f039f-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="f039f-237">Aprire il modello di processo selezionato per la modifica.</span><span class="sxs-lookup"><span data-stu-id="f039f-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="f039f-238">È possibile aprirlo direttamente in Progettazione flussi di lavoro o nell'editor XML per lavorare con XAML.</span><span class="sxs-lookup"><span data-stu-id="f039f-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="f039f-239">Aggiungere l'elenco seguente di argomenti nuovi come voci, una per riga, nella scheda degli argomenti della progettazione flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f039f-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="f039f-240">Tutti gli argomenti devono presentare direction=In e type=String.</span><span class="sxs-lookup"><span data-stu-id="f039f-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="f039f-241">Questi verranno usati per inviare i parametri dalla definizione di compilazione al flusso di lavoro, dove poi verranno usati per chiamare lo script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Elenco di argomenti][3]

   <span data-ttu-id="f039f-243">Il codice XAML corrispondente sarà analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="f039f-243">The corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="f039f-244">Aggiungere una nuova sequenza alla fine di Esegui su agente:</span><span class="sxs-lookup"><span data-stu-id="f039f-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="f039f-245">Iniziare con l'aggiunta di un'attività di istruzione If per verificare la presenza di un file di script valido.</span><span class="sxs-lookup"><span data-stu-id="f039f-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="f039f-246">Impostare la condizione sul valore seguente:</span><span class="sxs-lookup"><span data-stu-id="f039f-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="f039f-247">Nella condizione Then dell'istruzione If aggiungere una nuova attività di sequenza.</span><span class="sxs-lookup"><span data-stu-id="f039f-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="f039f-248">Impostare il nome visualizzato su 'Start publish'</span><span class="sxs-lookup"><span data-stu-id="f039f-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="f039f-249">Con l'opzione di avvio della sequenza di pubblicazione ancora selezionata, aggiungere l'elenco seguente di nuove variabili come voci ognuna su una nuova riga nella scheda delle variabili della progettazione flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f039f-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="f039f-250">Tutte le variabili presentare Variable type =String e Scope=Start publish.</span><span class="sxs-lookup"><span data-stu-id="f039f-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="f039f-251">Questi verranno usati per inviare i parametri dalla definizione di compilazione al flusso di lavoro, dove poi verranno usati per chiamare lo script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="f039f-252">SubscriptionDataFilePath, di tipo String</span><span class="sxs-lookup"><span data-stu-id="f039f-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="f039f-253">PublishScriptFilePath, di tipo String</span><span class="sxs-lookup"><span data-stu-id="f039f-253">PublishScriptFilePath, of type String</span></span>

        ![Nuove variabili][4]
   4. <span data-ttu-id="f039f-255">Se si usa TFS 2012 o versione precedente, aggiungere un'attività ConvertWorkspaceItem all'inizio della nuova sequenza.</span><span class="sxs-lookup"><span data-stu-id="f039f-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="f039f-256">Se si usa TFS 2013 o versione successiva, aggiungere un'attività GetLocalPath all'inizio della nuova sequenza.</span><span class="sxs-lookup"><span data-stu-id="f039f-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="f039f-257">Per ConvertWorkspaceItem impostare le proprietà come segue: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="f039f-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="f039f-258">Per un'attività GetLocalPath impostare la proprietà IncomingPath su 'PublishScriptLocation' e Result su 'PublishScriptFilePath'.</span><span class="sxs-lookup"><span data-stu-id="f039f-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="f039f-259">Questa attività converte il percorso dello script di pubblicazione dai percorsi server TFS (se applicabile) in un percorso standard di disco locale.</span><span class="sxs-lookup"><span data-stu-id="f039f-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="f039f-260">Se si usa TFS 2012 o versione precedente, aggiungere un'altra attività ConvertWorkspaceItem alla fine della nuova sequenza.</span><span class="sxs-lookup"><span data-stu-id="f039f-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="f039f-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="f039f-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="f039f-262">Se si usa TFS 2013 o versione successiva, aggiungere un'altra attività GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="f039f-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="f039f-263">IncomingPath='SubscriptionDataFileLocation' e Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="f039f-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="f039f-264">Aggiungere un'attività InvokeProcess alla fine della nuova sequenza.</span><span class="sxs-lookup"><span data-stu-id="f039f-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="f039f-265">Questa attività chiama PowerShell.exe con gli argomenti passati dalla definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="f039f-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="f039f-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="f039f-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="f039f-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="f039f-268">FileName = "PowerShell" (includere le virgolette)</span><span class="sxs-lookup"><span data-stu-id="f039f-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="f039f-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="f039f-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="f039f-270">Nella casella di testo della sezione **Gestisci output standard** di InvokeProcess impostare il valore della casella di testo su 'data'.</span><span class="sxs-lookup"><span data-stu-id="f039f-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="f039f-271">Questa è una variabile in cui archiviare i dati dell'output standard.</span><span class="sxs-lookup"><span data-stu-id="f039f-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="f039f-272">Aggiungere un'attività WriteBuildMessage appena sotto la sezione **Gestisci output standard** .</span><span class="sxs-lookup"><span data-stu-id="f039f-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="f039f-273">Impostare Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' e Message='data'.</span><span class="sxs-lookup"><span data-stu-id="f039f-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="f039f-274">Questo garantisce che l'output standard dello script verrà scritto nell'output di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="f039f-275">Nella casella di testo della sezione **Gestisci output errore** di InvokeProcess impostare il valore della casella di testo su 'data'.</span><span class="sxs-lookup"><span data-stu-id="f039f-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="f039f-276">Questa è una variabile in cui archiviare i dati dell'output errore.</span><span class="sxs-lookup"><span data-stu-id="f039f-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="f039f-277">Aggiungere un'attività WriteBuildError appena sotto la sezione **Gestisci output errore** .</span><span class="sxs-lookup"><span data-stu-id="f039f-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="f039f-278">Impostare Message='data'.</span><span class="sxs-lookup"><span data-stu-id="f039f-278">Set the Message='data'.</span></span> <span data-ttu-id="f039f-279">Questo garantisce che l'output di errore dello script verrà scritto nell'output di errore della compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="f039f-280">Correggere eventuali errori, indicati da punti esclamativi blu.</span><span class="sxs-lookup"><span data-stu-id="f039f-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="f039f-281">Passare il puntatore sui punti esclamativi per ottenere un suggerimento relativo all'errore.</span><span class="sxs-lookup"><span data-stu-id="f039f-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="f039f-282">Salvare il flusso di lavoro per cancellare gli errori.</span><span class="sxs-lookup"><span data-stu-id="f039f-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="f039f-283">Il risultato finale delle attività del flusso di lavoro di pubblicazione sarà simile al seguente nella finestra di progettazione:</span><span class="sxs-lookup"><span data-stu-id="f039f-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![Attività flusso di lavoro][5]

   <span data-ttu-id="f039f-285">Il risultato finale delle attività del flusso di lavoro di pubblicazione sarà simile al seguente nel codice XAML:</span><span class="sxs-lookup"><span data-stu-id="f039f-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="f039f-286">Salvare il flusso di lavoro del modello di processo di compilazione ed eseguire l'archiviazione di questo file.</span><span class="sxs-lookup"><span data-stu-id="f039f-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="f039f-287">Modificare la definizione di compilazione (chiuderla se è già aperta) e fare clic sul pulsante **Nuovo** se il nuovo modello non è ancora visibile nell'elenco di modelli di processo.</span><span class="sxs-lookup"><span data-stu-id="f039f-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="f039f-288">Impostare i valori delle proprietà dei parametri nella sezione Varie come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f039f-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="f039f-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Questo valore deriva da: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="f039f-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="f039f-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Questo valore deriva da: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="f039f-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="f039f-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="f039f-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="f039f-292">ServiceName = 'mycloudservicename' *Qui usare il nome del servizio cloud appropriato*</span><span class="sxs-lookup"><span data-stu-id="f039f-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="f039f-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="f039f-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="f039f-294">StorageAccountName = 'mystorageaccountname' *Qui usare il nome dell'account di archiviazione appropriato*</span><span class="sxs-lookup"><span data-stu-id="f039f-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="f039f-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="f039f-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="f039f-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="f039f-296">SubscriptionName = 'default'</span></span>

    ![Valori delle proprietà dei parametri][6]
11. <span data-ttu-id="f039f-298">Salvare le modifiche nella definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="f039f-299">Accodare una compilazione per eseguire sia la compilazione del pacchetto che la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="f039f-300">Se è impostato un trigger per la distribuzione continua, questo comportamento verrà eseguito a ogni archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f039f-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="f039f-301">Modello di script PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="f039f-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="f039f-302">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f039f-302">Next steps</span></span>
<span data-ttu-id="f039f-303">Per abilitare il debug remoto durante l'uso della distribuzione continua, vedere [Abilitare il debug remoto con la distribuzione continua per la pubblicazione in Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="f039f-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
