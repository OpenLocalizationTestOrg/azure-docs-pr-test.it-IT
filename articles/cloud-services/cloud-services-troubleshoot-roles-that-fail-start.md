---
title: Risolvere i problemi dei ruoli che non vengono avviati | Documentazione Microsoft
description: Informazioni su alcuni motivi comuni del mancato avvio di un ruolo del servizio cloud. Include anche soluzioni per questi problemi.
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
ms.openlocfilehash: 7d956192e8b9c3688b8b6f0108bd9296f66fbd62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="d4448-104">Risolvere i problemi dei ruoli del servizio cloud che non vengono avviati</span><span class="sxs-lookup"><span data-stu-id="d4448-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="d4448-105">Ecco alcuni problemi e soluzioni comini correlati ai ruoli di Servizi cloud di Azure che non vengono avviati.</span><span class="sxs-lookup"><span data-stu-id="d4448-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="d4448-106">File DLL o dipendenze mancanti</span><span class="sxs-lookup"><span data-stu-id="d4448-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="d4448-107">I problemi dovuti a ruoli che non rispondono e ruoli che passano in ciclo tra gli stati **Inizializzazione**, **Occupato** e **Arresto** possono essere provocati da file DLL o assembly mancanti.</span><span class="sxs-lookup"><span data-stu-id="d4448-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="d4448-108">I sintomi di file DLL o assembly mancati includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4448-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="d4448-109">L'istanza del ruolo passa in ciclo tra gli stati **Inizializzazione**, **Occupato** e **Arresto**.</span><span class="sxs-lookup"><span data-stu-id="d4448-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="d4448-110">L'istanza del ruolo è passata allo stato **Pronto** , ma, se si passa all'applicazione Web, la pagina non viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="d4448-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="d4448-111">Sono disponibili diversi metodi consigliati per esaminare questi problemi.</span><span class="sxs-lookup"><span data-stu-id="d4448-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="d4448-112">Diagnosticare i problemi di DLL mancanti in un ruolo Web</span><span class="sxs-lookup"><span data-stu-id="d4448-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="d4448-113">Quando si passa a un sito Web distribuito in un ruolo Web e il browser visualizza un errore server simile al seguente, è possibile che indichi una DLL mancante.</span><span class="sxs-lookup"><span data-stu-id="d4448-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

![Errore del server nell'applicazione '/'.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="d4448-115">Diagnosticare i problemi disabilitando gli errori personalizzati</span><span class="sxs-lookup"><span data-stu-id="d4448-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="d4448-116">Per visualizzare informazioni sugli errori più completi, configurare il file web.config per il ruolo Web per poter disattivare la modalità di errore personalizzata e ridistribuire il servizio.</span><span class="sxs-lookup"><span data-stu-id="d4448-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="d4448-117">Per visualizzare errori più completi senza usare Desktop remoto:</span><span class="sxs-lookup"><span data-stu-id="d4448-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="d4448-118">Aprire la soluzione in Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4448-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="d4448-119">In **Esplora soluzioni**individuare il file web.config e aprirlo.</span><span class="sxs-lookup"><span data-stu-id="d4448-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="d4448-120">Nel file web.config individuare la sezione system.web e aggiungere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="d4448-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="d4448-121">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="d4448-121">Save the file.</span></span>
5. <span data-ttu-id="d4448-122">Ricreare il pacchetto e ridistribuire il servizio.</span><span class="sxs-lookup"><span data-stu-id="d4448-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="d4448-123">Quando il servizio viene ridistribuito, verrà visualizzato un messaggio di errore con il nome dell'assembly o della DLL mancante.</span><span class="sxs-lookup"><span data-stu-id="d4448-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="d4448-124">Diagnosticare i problemi visualizzando l'errore in remoto</span><span class="sxs-lookup"><span data-stu-id="d4448-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="d4448-125">È possibile usare Desktop remoto per accedere al ruolo e visualizzare informazioni sugli errori più complete in remoto.</span><span class="sxs-lookup"><span data-stu-id="d4448-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="d4448-126">Seguire questa procedura per visualizzare gli errori usando Desktop remoto:</span><span class="sxs-lookup"><span data-stu-id="d4448-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="d4448-127">Verificare che sia installato Azure SDK 1.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d4448-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="d4448-128">Durante la distribuzione della soluzione con Visual Studio, scegliere "Configura connessioni Desktop remoto".</span><span class="sxs-lookup"><span data-stu-id="d4448-128">During the deployment of the solution by using Visual Studio, choose to “Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="d4448-129">Per altre informazioni sulla configurazione della connessione Desktop remoto, vedere [Utilizzo di Desktop remoto con i ruoli Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d4448-129">For more information on configuring the Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="d4448-130">Quando lo stato dell'istanza è **Pronto**, nel portale di Microsoft Azure classico fare clic su una delle istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="d4448-130">In the Microsoft Azure classic portal, once the instance shows a status of **Ready**, click one of the role instances.</span></span>
4. <span data-ttu-id="d4448-131">Fare clic sull'icona **Connetti** nell'area **Accesso remoto** della barra multifunzione.</span><span class="sxs-lookup"><span data-stu-id="d4448-131">Click the **Connect** icon in the **Remote Access** area of the ribbon.</span></span>
5. <span data-ttu-id="d4448-132">Accedere alla macchina virtuale usando le credenziali specificate durante la configurazione di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="d4448-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="d4448-133">Aprire una finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="d4448-133">Open a command window.</span></span>
7. <span data-ttu-id="d4448-134">Digitare `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="d4448-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="d4448-135">Annotare il valore dell'indirizzo IPV4.</span><span class="sxs-lookup"><span data-stu-id="d4448-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="d4448-136">Aprire Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d4448-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="d4448-137">Digitare l'indirizzo e il nome dell'applicazione Web,</span><span class="sxs-lookup"><span data-stu-id="d4448-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="d4448-138">ad esempio `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="d4448-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="d4448-139">Se si passa al sito Web, ora verranno restituiti messaggi di errore più espliciti:</span><span class="sxs-lookup"><span data-stu-id="d4448-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="d4448-140">Errore del server nell'applicazione '/'.</span><span class="sxs-lookup"><span data-stu-id="d4448-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="d4448-141">Descrizione: Eccezione non gestita durante l'esecuzione della richiesta Web corrente.</span><span class="sxs-lookup"><span data-stu-id="d4448-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="d4448-142">Per altre informazioni sull'errore e sul suo punto di origine nel codice, vedere l'analisi dello stack.</span><span class="sxs-lookup"><span data-stu-id="d4448-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="d4448-143">Dettagli dell'eccezione: System.IO.FIleNotFoundException: Impossibile caricare il file o l'assembly 'Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35' o una delle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="d4448-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="d4448-144">Non è possibile trovare il file specificato.</span><span class="sxs-lookup"><span data-stu-id="d4448-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="d4448-145">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d4448-145">For example:</span></span>

![Errore esplicito del server nell'applicazione '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="d4448-147">Diagnosticare i problemi usando l'emulatore di calcolo</span><span class="sxs-lookup"><span data-stu-id="d4448-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="d4448-148">È possibile usare l'emulatore di calcolo di Microsoft Azure per diagnosticare e risolvere i problemi relativi a dipendenze mancanti e gli errori del file web.config.</span><span class="sxs-lookup"><span data-stu-id="d4448-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="d4448-149">Per ottenere risultati ottimali con questo metodo di diagnosi, è consigliabile usare un computer o una macchina virtuale in cui è presente un'installazione pulita di Windows.</span><span class="sxs-lookup"><span data-stu-id="d4448-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="d4448-150">Per simulare in modo ottimale l'ambiente Azure, usare Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="d4448-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="d4448-151">Installare la versione autonoma di [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d4448-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d4448-152">Nel computer di sviluppo compilare il progetto di servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d4448-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="d4448-153">In Esplora risorse passare alla cartella bin\debug del progetto di servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d4448-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="d4448-154">Copiare la cartella con estensione csx e il file con estensione cscfg nel computer usato per eseguire il debug dei problemi.</span><span class="sxs-lookup"><span data-stu-id="d4448-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="d4448-155">Nel computer pulito aprire una finestra del prompt dei comandi di Azure SDK e digitare `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="d4448-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="d4448-156">Al prompt dei comandi digitare `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="d4448-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="d4448-157">All'avvio del ruolo, verranno visualizzate informazioni dettagliate sull'errore in Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d4448-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="d4448-158">È anche possibile usare gli strumenti di risoluzione dei problemi standard di Windows per diagnosticare ulteriormente il problema.</span><span class="sxs-lookup"><span data-stu-id="d4448-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="d4448-159">Diagnosticare i problemi usando IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="d4448-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="d4448-160">Per i ruoli di lavoro e i ruoli Web che fanno uso di .NET Framework 4, è possibile usare [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), disponibile in Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d4448-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="d4448-161">Seguire questa procedura per distribuire il servizio con IntelliTrace abilitato:</span><span class="sxs-lookup"><span data-stu-id="d4448-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="d4448-162">Verificare che sia installato Azure SDK 1.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d4448-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="d4448-163">Distribuire la soluzione usando Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4448-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="d4448-164">Durante la distribuzione selezionare la casella di controllo **Abilita IntelliTrace per ruoli .NET 4** .</span><span class="sxs-lookup"><span data-stu-id="d4448-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="d4448-165">Dopo l'avvio dell'istanza, aprire **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="d4448-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="d4448-166">Espandere il nodo **Azure\\Servizi cloud** e trovare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4448-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="d4448-167">Espandere la distribuzione finché non vengono visualizzate le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="d4448-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="d4448-168">Fare clic con il pulsante destro del mouse su una delle istanze.</span><span class="sxs-lookup"><span data-stu-id="d4448-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="d4448-169">Scegliere **Visualizza log IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="d4448-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="d4448-170">Verrà visualizzato il **Riepilogo IntelliTrace** .</span><span class="sxs-lookup"><span data-stu-id="d4448-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="d4448-171">Individuare la sezione delle eccezioni del riepilogo.</span><span class="sxs-lookup"><span data-stu-id="d4448-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="d4448-172">Se sono presenti eccezioni, la sezione sarà denominata **Dati eccezione**.</span><span class="sxs-lookup"><span data-stu-id="d4448-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="d4448-173">Espandere **Dati eccezione**e cercare errori **System.IO.FileNotFoundException** analoghi al seguente:</span><span class="sxs-lookup"><span data-stu-id="d4448-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![Dati eccezione, assembly o file mancante](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="d4448-175">Risolvere DLL e assembly mancanti</span><span class="sxs-lookup"><span data-stu-id="d4448-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="d4448-176">Per risolvere errori di assembly e DLL mancanti, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d4448-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="d4448-177">Aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4448-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="d4448-178">In **Esplora soluzioni** aprire la cartella **Riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="d4448-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="d4448-179">Fare clic sull'assembly specificato nell'errore.</span><span class="sxs-lookup"><span data-stu-id="d4448-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="d4448-180">Nel riquadro **Proprietà** trovare la proprietà **Copia localmente** e impostare il valore su **True**.</span><span class="sxs-lookup"><span data-stu-id="d4448-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="d4448-181">Ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d4448-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="d4448-182">Dopo avere verificato che tutti gli errori sono stati corretti, è possibile distribuire il servizio senza selezionare la casella di controllo **Abilita IntelliTrace per ruoli .NET 4** .</span><span class="sxs-lookup"><span data-stu-id="d4448-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4448-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4448-183">Next steps</span></span>
<span data-ttu-id="d4448-184">Altri [articoli sulla risoluzione dei problemi](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="d4448-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="d4448-185">Per informazioni su come risolvere i problemi dei ruoli del servizio cloud utilizzando i dati di diagnostica del calcolo Azure PaaS, vedere la [serie di blog di Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4448-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
