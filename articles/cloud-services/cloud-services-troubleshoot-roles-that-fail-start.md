---
title: ruoli aaaTroubleshoot che non soddisfano toostart | Documenti Microsoft
description: Ecco alcuni motivi comuni per cui un ruolo del servizio Cloud potrebbe non riuscire toostart. Sono inoltre disponibili soluzioni ai problemi di toothese.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="26d56-104">Risolvere i problemi relativi a ruoli del servizio Cloud che non soddisfano toostart</span><span class="sxs-lookup"><span data-stu-id="26d56-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="26d56-105">Ecco alcuni problemi comuni e i ruoli di servizi Cloud correlati tooAzure soluzioni che non soddisfano toostart.</span><span class="sxs-lookup"><span data-stu-id="26d56-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="26d56-106">File DLL o dipendenze mancanti</span><span class="sxs-lookup"><span data-stu-id="26d56-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="26d56-107">I problemi dovuti a ruoli che non rispondono e ruoli che passano in ciclo tra gli stati **Inizializzazione**, **Occupato** e **Arresto** possono essere provocati da file DLL o assembly mancanti.</span><span class="sxs-lookup"><span data-stu-id="26d56-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="26d56-108">I sintomi di file DLL o assembly mancati includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="26d56-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="26d56-109">L'istanza del ruolo passa in ciclo tra gli stati **Inizializzazione**, **Occupato** e **Arresto**.</span><span class="sxs-lookup"><span data-stu-id="26d56-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="26d56-110">L'istanza del ruolo è stato spostato troppo**pronto** ma se si passa l'applicazione web tooyour, non viene visualizzata la pagina di hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="26d56-111">Sono disponibili diversi metodi consigliati per esaminare questi problemi.</span><span class="sxs-lookup"><span data-stu-id="26d56-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="26d56-112">Diagnosticare i problemi di DLL mancanti in un ruolo Web</span><span class="sxs-lookup"><span data-stu-id="26d56-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="26d56-113">Quando si passa tooa sito Web viene distribuito in un ruolo web e browser hello Visualizza server errore simili toohello di seguito, è possibile che una DLL è manca.</span><span class="sxs-lookup"><span data-stu-id="26d56-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

![Errore del server nell'applicazione '/'.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="26d56-115">Diagnosticare i problemi disabilitando gli errori personalizzati</span><span class="sxs-lookup"><span data-stu-id="26d56-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="26d56-116">Informazioni sugli errori più completi possono essere visualizzati mediante la configurazione Web. config hello per tooOff modalità hello web ruolo tooset hello errore personalizzato e ridistribuire il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="26d56-117">tooview completare più errori senza usare Desktop remoto:</span><span class="sxs-lookup"><span data-stu-id="26d56-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="26d56-118">Aprire la soluzione hello in Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26d56-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="26d56-119">In hello **Esplora**, individuare il file Web. config hello e aprirlo.</span><span class="sxs-lookup"><span data-stu-id="26d56-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="26d56-120">Nel file Web. config hello, nella sezione System. Web hello e aggiungere hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="26d56-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="26d56-121">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-121">Save hello file.</span></span>
5. <span data-ttu-id="26d56-122">Ricreare il pacchetto e ridistribuire il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="26d56-123">Una volta che il servizio di hello viene ridistribuito, si verrà visualizzato un messaggio di errore con nome hello di hello mancante DLL o assembly.</span><span class="sxs-lookup"><span data-stu-id="26d56-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="26d56-124">Diagnosticare i problemi visualizzando errore hello in modalità remota</span><span class="sxs-lookup"><span data-stu-id="26d56-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="26d56-125">È possibile utilizzare Desktop remoto tooaccess hello ruolo e visualizzare informazioni sugli errori più completi in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="26d56-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="26d56-126">Utilizzare hello dopo errori di hello tooview passaggi tramite Desktop remoto:</span><span class="sxs-lookup"><span data-stu-id="26d56-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="26d56-127">Verificare che sia installato Azure SDK 1.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="26d56-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="26d56-128">Durante la distribuzione di hello della soluzione hello tramite Visual Studio, scegliere troppo "Configura connessioni Desktop remoto...".</span><span class="sxs-lookup"><span data-stu-id="26d56-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="26d56-129">Per ulteriori informazioni sulla configurazione della connessione Desktop remoto hello, vedere [tramite Desktop remoto con i ruoli Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="26d56-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="26d56-130">In hello portale Microsoft Azure classico, una volta che viene visualizzato lo stato istanza hello **pronto**, fare clic su una delle istanze del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="26d56-131">Fare clic su hello **Connetti** icona in hello **accesso remoto** area della barra multifunzione hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="26d56-132">Accedere utilizzando le credenziali specificate durante la configurazione di Desktop remoto hello hello macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="26d56-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="26d56-133">Aprire una finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="26d56-133">Open a command window.</span></span>
7. <span data-ttu-id="26d56-134">Digitare `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="26d56-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="26d56-135">Si noti il valore di indirizzo IPV4 hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="26d56-136">Aprire Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="26d56-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="26d56-137">Digitare l'indirizzo hello e il nome di hello dell'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="26d56-138">ad esempio `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="26d56-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="26d56-139">Esplorazione toohello sito Web ora restituiscono i messaggi di errore più espliciti:</span><span class="sxs-lookup"><span data-stu-id="26d56-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="26d56-140">Errore del server nell'applicazione '/'.</span><span class="sxs-lookup"><span data-stu-id="26d56-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="26d56-141">Descrizione: Si è verificata un'eccezione non gestita durante l'esecuzione di hello della richiesta web corrente hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="26d56-142">Esaminare l'analisi dello stack per ulteriori informazioni sull'errore hello hello e dove proviene dal codice hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="26d56-143">Dettagli dell'eccezione: System.IO.FIleNotFoundException: Impossibile caricare il file o l'assembly 'Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35' o una delle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="26d56-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="26d56-144">Hello Impossibile trovare il file hello specificato.</span><span class="sxs-lookup"><span data-stu-id="26d56-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="26d56-145">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="26d56-145">For example:</span></span>

![Errore esplicito del server nell'applicazione '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="26d56-147">Diagnosticare i problemi usando l'emulatore di calcolo hello</span><span class="sxs-lookup"><span data-stu-id="26d56-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="26d56-148">È possibile utilizzare hello Microsoft Azure compute emulator toodiagnose e risolvere i problemi di dipendenze mancanti e gli errori di Web. config.</span><span class="sxs-lookup"><span data-stu-id="26d56-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="26d56-149">Per ottenere risultati ottimali con questo metodo di diagnosi, è consigliabile usare un computer o una macchina virtuale in cui è presente un'installazione pulita di Windows.</span><span class="sxs-lookup"><span data-stu-id="26d56-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="26d56-150">toobest simulare hello ambiente Azure, utilizzare Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="26d56-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="26d56-151">Installare una versione autonoma di hello di hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="26d56-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="26d56-152">Nel computer di sviluppo hello, compilare il progetto di servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="26d56-153">In Esplora risorse, passare toohello nella cartella bin\debug del progetto di servizio cloud di hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="26d56-154">Copiare cartelle con estensione csx hello e computer di toohello file con estensione cscfg che si siano utilizzando problemi hello toodebug.</span><span class="sxs-lookup"><span data-stu-id="26d56-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="26d56-155">Nel computer pulito hello, aprire una finestra prompt dei comandi di Azure SDK e digitare `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="26d56-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="26d56-156">Al prompt dei comandi di hello, digitare `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="26d56-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="26d56-157">Quando viene avviato il ruolo di hello, si noterà informazioni dettagliate sull'errore in Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="26d56-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="26d56-158">È inoltre possibile utilizzare gli strumenti di risoluzione dei problemi di Windows standard toofurther diagnosticare il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="26d56-159">Diagnosticare i problemi usando IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="26d56-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="26d56-160">Per i ruoli di lavoro e i ruoli Web che fanno uso di .NET Framework 4, è possibile usare [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), disponibile in Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="26d56-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="26d56-161">Seguire questi servizio hello toodeploy di passaggi con IntelliTrace abilitato:</span><span class="sxs-lookup"><span data-stu-id="26d56-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="26d56-162">Verificare che sia installato Azure SDK 1.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="26d56-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="26d56-163">Distribuire la soluzione hello usando Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26d56-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="26d56-164">Durante la distribuzione, controllare hello **Abilita IntelliTrace per ruoli .NET 4** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="26d56-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="26d56-165">Una volta avviata l'istanza di hello, aprire hello **Esplora Server**.</span><span class="sxs-lookup"><span data-stu-id="26d56-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="26d56-166">Espandere hello **Azure\\servizi Cloud** nodo e individuare hello distribuzione.</span><span class="sxs-lookup"><span data-stu-id="26d56-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="26d56-167">Espandere la distribuzione di hello fino a visualizzare le istanze del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="26d56-168">Fare clic su una delle istanze di hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="26d56-169">Scegliere **Visualizza log IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="26d56-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="26d56-170">Hello **Riepilogo IntelliTrace** verrà aperto.</span><span class="sxs-lookup"><span data-stu-id="26d56-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="26d56-171">Individuare la sezione relativa alle eccezioni hello di hello riepilogo.</span><span class="sxs-lookup"><span data-stu-id="26d56-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="26d56-172">Se esistono eccezioni, sarà sezione hello **dati dell'eccezione**.</span><span class="sxs-lookup"><span data-stu-id="26d56-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="26d56-173">Espandere hello **dati dell'eccezione** e cercare **System.IO. FileNotFoundException** seguente toohello simili errori:</span><span class="sxs-lookup"><span data-stu-id="26d56-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![Dati eccezione, assembly o file mancante](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="26d56-175">Risolvere DLL e assembly mancanti</span><span class="sxs-lookup"><span data-stu-id="26d56-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="26d56-176">tooaddress mancante errori DLL e assembly, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="26d56-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="26d56-177">Aprire la soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26d56-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="26d56-178">In **Esplora**aprire hello **riferimenti** cartella.</span><span class="sxs-lookup"><span data-stu-id="26d56-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="26d56-179">Fare clic su assembly hello identificato in errore hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="26d56-180">In hello **proprietà** riquadro individuare **proprietà Copia localmente** e impostare il valore di hello troppo**True**.</span><span class="sxs-lookup"><span data-stu-id="26d56-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="26d56-181">Ridistribuire il servizio di cloud hello.</span><span class="sxs-lookup"><span data-stu-id="26d56-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="26d56-182">Dopo avere verificato che tutti gli errori sono stati corretti, è possibile distribuire il servizio di hello senza verificare hello **Abilita IntelliTrace per ruoli .NET 4** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="26d56-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26d56-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26d56-183">Next steps</span></span>
<span data-ttu-id="26d56-184">Altri [articoli sulla risoluzione dei problemi](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="26d56-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="26d56-185">toolearn come ruolo del servizio cloud tootroubleshoot problemi utilizzando i dati di diagnostica di Azure PaaS computer, vedere [serie di blog di Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="26d56-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
