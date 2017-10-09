---
title: aaaUsing tooDev tooPublish script di Windows PowerShell e gli ambienti di Test | Documenti Microsoft
description: Informazioni su come Windows PowerShell toouse gli script da ambienti di test e di toodevelopment toopublish Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="8e7a2-103">Utilizzo di Windows PowerShell consente di generare script toopublish toodev e test ambienti</span><span class="sxs-lookup"><span data-stu-id="8e7a2-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="8e7a2-104">Quando si crea un'applicazione web in Visual Studio, è possibile generare uno script di Windows PowerShell che è possibile usare la pubblicazione di hello tooautomate successive di tooAzure il sito Web come un'App Web nel servizio App di Azure o di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="8e7a2-105">È possibile modificare ed estendere i requisiti di script di Windows PowerShell hello in toosuit editor di Visual Studio hello oppure integrarlo script hello compilazione esistente, test e script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="8e7a2-106">Utilizzando questi script, è possibile eseguire il provisioning (noto anche come ambienti di sviluppo e test) di versioni personalizzate del sito per un utilizzo temporaneo.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="8e7a2-107">Ad esempio, è possibile configurare una particolare versione del sito Web in una macchina virtuale di Azure o hello slot toorun un sito Web di gestione temporanea un gruppo di test, riprodurre un bug, testare una correzione di bug, valutare una modifica proposta o configurare un ambiente personalizzato per una demo o una presentazione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="8e7a2-108">Dopo aver creato uno script che pubblica il progetto, è possibile ricreare ambienti identici eseguendo nuovamente script hello, in base alle esigenze o eseguire script hello con build del toocreate di applicazione web un ambiente di test personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8e7a2-109">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="8e7a2-109">What you need</span></span>
* <span data-ttu-id="8e7a2-110">Azure SDK 2.3 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="8e7a2-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="8e7a2-111">Per altre informazioni vedere [Scaricare Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="8e7a2-112">Gli script hello toogenerate di hello Azure SDK non è necessario per i progetti web.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="8e7a2-113">Questa funzionalità è per i progetti web, non per i ruoli web nei servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="8e7a2-114">Azure PowerShell 0.7.4 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="8e7a2-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="8e7a2-115">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="8e7a2-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="8e7a2-117">Strumenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="8e7a2-117">Additional tools</span></span>
<span data-ttu-id="8e7a2-118">Sono disponibili altri strumenti e risorse per l'utilizzo di PowerShell in Visual Studio per lo sviluppo in Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="8e7a2-119">Vedere [PowerShell Tools per Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="8e7a2-120">Hello di generazione script di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="8e7a2-120">Generating hello publish scripts</span></span>
<span data-ttu-id="8e7a2-121">È possibile generare hello script di pubblicazione per una macchina virtuale che ospita il sito Web quando si crea un nuovo progetto seguendo [queste istruzioni](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="8e7a2-122">È possibile anche [generare script di pubblicazione per le app Web del Servizio app di Azure](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="8e7a2-123">Script generati da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8e7a2-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="8e7a2-124">Visual Studio genera una cartella a livello di soluzione denominata **PublishScripts** che contiene due file di Windows PowerShell, uno script di pubblicazione per la macchina virtuale o del sito Web e un modulo che contiene funzioni che è possibile utilizzare in hello script.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="8e7a2-125">Visual Studio genera anche un file in formato JSON hello che specifica i dettagli di hello del progetto hello che si sta distribuendo.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="8e7a2-126">Pubblicazione di script da parte di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e7a2-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="8e7a2-127">script di pubblicazione Hello contiene specifico pubblicare i passaggi per la distribuzione del sito Web tooa o una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="8e7a2-128">Visual Studio fornisce la colorazione della sintassi per lo sviluppo di Windows PowerShell .</span><span class="sxs-lookup"><span data-stu-id="8e7a2-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="8e7a2-129">La Guida per le funzioni hello è disponibile ed è possibile modificare liberamente le funzioni hello in hello script toosuit propri requisiti.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="8e7a2-130">Modulo di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e7a2-130">Windows PowerShell module</span></span>
<span data-ttu-id="8e7a2-131">Hello modulo generato da Visual Studio contiene le funzioni hello di Windows PowerShell Usa script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="8e7a2-132">Queste sono funzioni di Azure PowerShell e non sono previsti toobe modificato.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="8e7a2-133">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="8e7a2-134">File di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-134">JSON configuration file</span></span>
<span data-ttu-id="8e7a2-135">file JSON di Hello viene creato in hello **configurazioni** cartella e contiene i dati di configurazione che specifica esattamente quali tooAzure toodeploy risorse.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="8e7a2-136">nome di Hello del file hello generato da Visual Studio è progetto-nome-WAWS-DEV se è stato creato un sito Web o progetto nome-VM-DEV se è stata creata una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="8e7a2-137">Di seguito è riportato un esempio di un file di configurazione JSON generato quando si crea un sito Web.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="8e7a2-138">La maggior parte dei valori hello sono di chiara interpretazione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="8e7a2-139">nome del sito Web Hello viene generato da Azure, pertanto potrebbe non corrispondere al nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="8e7a2-140">Quando si crea una macchina virtuale, il file di configurazione JSON hello ricerca simili toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="8e7a2-141">Si noti che viene creato un servizio cloud come contenitore per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="8e7a2-142">macchina virtuale Hello contiene i consueti endpoint di hello per l'accesso al web tramite HTTP e HTTPS, oltre agli endpoint per distribuzione Web, che consente di pubblicare toohello sito Web dal computer locale, Desktop remoto e Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="8e7a2-143">È possibile modificare hello JSON configurazione toochange cosa accade quando si esegue hello script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="8e7a2-144">Hello `cloudService` e `virtualMachine` le sezioni sono obbligatorie, ma è possibile eliminare hello `databases` sezione se non è necessario.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="8e7a2-145">proprietà Hello vuota nel file di configurazione predefinita di hello generato da Visual Studio sono facoltative. che hanno valori nel file di configurazione predefinito hello sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="8e7a2-146">Se si dispone di un sito Web che dispone di più ambienti di distribuzione (noti come slot) anziché un unico sito di produzione in Azure, è possibile includere nome dello slot hello in nome hello del sito Web di hello nel file di configurazione JSON hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="8e7a2-147">Ad esempio, se si dispone di un sito Web denominato **mysite** e uno slot denominato **test** quindi hello URI è mysite test.cloudapp.net, ma hello nome corretto toouse nel file di configurazione hello è MySite (test) .</span><span class="sxs-lookup"><span data-stu-id="8e7a2-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="8e7a2-148">È possibile farlo solo se gli slot e il sito Web di hello esistano già nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="8e7a2-149">In caso contrario, Crea sito Web di hello eseguendo script hello senza specificare slot hello, quindi creare uno slot hello hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), e successivamente eseguire script hello con il nome del sito Web modificato hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="8e7a2-150">Per altre informazioni sugli slot di distribuzione per le app Web, vedere [Configurare ambienti di gestione temporanea per le app Web del Servizio app di Azure](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="8e7a2-151">Come toorun hello pubblica script</span><span class="sxs-lookup"><span data-stu-id="8e7a2-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="8e7a2-152">Se non è stato eseguito uno script di Windows PowerShell prima di, è innanzitutto necessario impostare hello esecuzione criteri tooenable script toorun.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="8e7a2-153">Si tratta di un utenti tooprevent funzionalità di protezione dall'esecuzione di script di Windows PowerShell se sono vulnerabili toomalware o virus che comportano l'esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="8e7a2-154">Eseguire script hello</span><span class="sxs-lookup"><span data-stu-id="8e7a2-154">Run hello script</span></span>
1. <span data-ttu-id="8e7a2-155">Creare pacchetto di distribuzione Web hello per il progetto.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="8e7a2-156">Un pacchetto di distribuzione Web è un archivio compresso (file con estensione zip) che contengono i file che si desidera sito Web tooyour toocopy o macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="8e7a2-157">È possibile creare pacchetti di distribuzione Web in Visual Studio per qualsiasi applicazione web.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Creare pacchetto di distribuzione web](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="8e7a2-159">Per ulteriori informazioni, vedere [Procedura: Creare un pacchetto di distribuzione Web in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="8e7a2-160">È inoltre possibile automatizzare la creazione di hello del pacchetto di distribuzione Web, come descritto nella sezione hello **personalizzazione ed estensione hello pubblica script** più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="8e7a2-161">In **Esplora**, aprire il menu di scelta hello per script hello e quindi scegliere **aprire con PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="8e7a2-162">Se si tratta di hello prima volta che si eseguono script di Windows PowerShell nel computer, aprire una finestra del prompt dei comandi con privilegi di amministratore e hello tipo comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8e7a2-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="8e7a2-163">Accedi tooAzure utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="8e7a2-164">Quando richiesto, fornire nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="8e7a2-165">Si noti che quando si automatizza script hello, questo metodo per fornire le credenziali di Azure non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="8e7a2-166">In alternativa, è necessario utilizzare le credenziali tooprovide di file con estensione publishsettings hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="8e7a2-167">Una volta, è sufficiente usare il comando hello **Get-AzurePublishSettingsFile** hello toodownload file da Azure e successivamente usare **Import-AzurePublishSettingsFile** file hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="8e7a2-168">Per istruzioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="8e7a2-169">(Facoltativo) Se si desidera toocreate Azure le risorse, ad esempio hello virtual machine, database e del sito Web senza pubblicare l'applicazione web, utilizzare hello **Publish-WebApplication.ps1** con hello **-configurazione** argomento impostato toohello file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="8e7a2-170">Questo comando Usa hello JSON configurazione file toodetermine toocreate le risorse.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="8e7a2-171">Poiché utilizza le impostazioni predefinite di hello per gli altri argomenti della riga di comando, crea risorse hello, ma non di pubblicare l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="8e7a2-172">Hello-opzione /verbose offre ulteriori informazioni su ciò che accade.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="8e7a2-173">Hello utilizzare **Publish-WebApplication.ps1** comando come illustrato in uno degli esempi tooinvoke hello script seguente hello e pubblicare l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="8e7a2-174">Se è necessario toooverride le impostazioni predefinite di hello per le hello altri argomenti, ad esempio nome della sottoscrizione hello, nome del pacchetto, le credenziali di macchina virtuale o le credenziali del server database di pubblicazione, è possibile specificare tali parametri.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="8e7a2-175">Hello utilizzare **-Verbose** opzione toosee ulteriori informazioni sullo stato di avanzamento hello di hello processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="8e7a2-176">Se si crea una macchina virtuale, il comando di hello è simile al seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="8e7a2-177">Questo esempio mostra anche come hello toospecify le credenziali per più database.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="8e7a2-178">Per le macchine virtuali hello create da questi script, certificati SSL hello non da un'autorità radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="8e7a2-179">È pertanto necessario hello toouse **-AllowUntrusted** opzione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="8e7a2-180">Hello script può creare database, ma non crea server di database.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="8e7a2-181">Se si desidera toocreate un server di database, è possibile utilizzare hello **New-AzureSqlDatabaseServer** funzione nel modulo Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="8e7a2-182">Personalizzazione ed estensione hello pubblica script</span><span class="sxs-lookup"><span data-stu-id="8e7a2-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="8e7a2-183">È possibile personalizzare hello pubblicare script e file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="8e7a2-184">Hello funzioni nel modulo di Windows PowerShell hello **AzureWebAppPublishModule.psm1** non sono previsti toobe modificato.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="8e7a2-185">Se si appena desidera toospecify un database diverso o modificare alcune delle proprietà hello della macchina virtuale hello, modificare il file di configurazione JSON hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="8e7a2-186">Se si vuole la funzionalità di hello tooextend di hello script tooautomate compilazione e test del progetto, è possibile implementare stub di funzioni in **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="8e7a2-187">tooautomate compilazione del progetto, aggiungere il codice che chiama MSBuild troppo`New-WebDeployPackage` come illustrato nell'esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="8e7a2-188">Hello percorso toohello comando MSBuild è diversa a seconda della versione di hello di Visual Studio è installato.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="8e7a2-189">percorso corretto hello tooget, è possibile utilizzare la funzione hello **Get-MSBuildCmd**, come illustrato in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="8e7a2-190">compilazione del progetto tooautomate</span><span class="sxs-lookup"><span data-stu-id="8e7a2-190">tooautomate building your project</span></span>
1. <span data-ttu-id="8e7a2-191">Aggiungere hello `$ProjectFile` parametro nella sezione parametri globali hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="8e7a2-192">Copy (funzione) hello `Get-MSBuildCmd` nel file di script.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="8e7a2-193">Sostituire `New-WebDeployPackage` con hello seguente di codice e sostituire il segnaposto hello nella costruzione di riga hello `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="8e7a2-194">Questo codice è per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="8e7a2-195">Se si utilizza Visual Studio 2013, modificare hello **VisualStudioVersion** proprietà seguente troppo`12.0`.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="8e7a2-196">toobuild l'applicazione web, usare MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="8e7a2-197">Per informazioni, vedere il riferimento della riga di comando di MSBuild all'indirizzo: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="8e7a2-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="8e7a2-198">Avvia l'esecuzione del comando di compilazione hello</span><span class="sxs-lookup"><span data-stu-id="8e7a2-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="8e7a2-199">Chiamare hello `New-WebDeployPackage` funzione prima di questa riga: `$Config = Read-ConfigFile $Configuration` per le app web o `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="8e7a2-200">Richiamare hello personalizzato script dalla riga di comando utilizzando il passaggio hello `$Project` argomento, come hello seguente riga di comando di esempio.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="8e7a2-201">tooautomate il test dell'applicazione, aggiungere il codice troppo`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="8e7a2-202">Essere toouncomment che righe hello **Publish-WebApplication.ps1** in cui queste funzioni vengono chiamate.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="8e7a2-203">Se non si fornisce un'implementazione, è possibile creare manualmente il progetto con Visual Studio, di pubblicare script toopublish tooAzure hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="8e7a2-204">Riepilogo della funzione di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="8e7a2-204">Publishing function summary</span></span>
<span data-ttu-id="8e7a2-205">tooget della Guida per le funzioni che è possibile usare al prompt dei comandi di Windows PowerShell hello, utilizzare il comando di hello `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="8e7a2-206">Guida di Hello sono inclusi esempi e informazioni sui parametri.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="8e7a2-207">stesso testo della Guida è disponibile anche nei file di origine script hello, Hello **AzureWebAppPublishModule.psm1** e **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="8e7a2-208">Guida in linea e script hello è localizzati nella lingua di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="8e7a2-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="8e7a2-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="8e7a2-210">Nome della funzione</span><span class="sxs-lookup"><span data-stu-id="8e7a2-210">Function name</span></span> | <span data-ttu-id="8e7a2-211">Description</span><span class="sxs-lookup"><span data-stu-id="8e7a2-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e7a2-212">Aggiungere AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="8e7a2-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="8e7a2-213">Creare un nuovo database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="8e7a2-214">Aggiungere AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="8e7a2-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="8e7a2-215">Crea database SQL di Azure dai valori hello nel file di configurazione JSON hello generato da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="8e7a2-216">Aggiungere-AzureVM</span><span class="sxs-lookup"><span data-stu-id="8e7a2-216">Add-AzureVM</span></span> |<span data-ttu-id="8e7a2-217">Crea una macchina virtuale di Azure e restituisce il che URL hello di hello distribuito macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="8e7a2-218">Hello funzione imposta i prerequisiti di hello e quindi hello chiamate **New-AzureVM** funzione toocreate (modulo Azure) una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="8e7a2-219">Aggiungere AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="8e7a2-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="8e7a2-220">Aggiunge una nuova macchina virtuale di tooa gli endpoint di input e restituisce hello di macchina virtuale con nuovo endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="8e7a2-221">Aggiungere AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="8e7a2-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="8e7a2-222">Crea un nuovo account di archiviazione di Azure nella sottoscrizione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="8e7a2-223">nome Hello dell'account di hello inizia con "devtest" seguito da una stringa alfanumerica univoca.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="8e7a2-224">funzione Hello restituisce il nome di hello del nuovo account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="8e7a2-225">È necessario specificare un percorso o un gruppo di affinità per il nuovo account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="8e7a2-226">Aggiungere-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="8e7a2-226">Add-AzureWebsite</span></span> |<span data-ttu-id="8e7a2-227">Crea un sito Web con percorso e il nome specificato hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="8e7a2-228">Questa funzione chiama hello **New-AzureWebsite** funzione nel modulo Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="8e7a2-229">Se la sottoscrizione hello non include già un sito Web con nome specificato hello, questa funzione Crea sito Web di hello e restituisce un oggetto sito Web.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="8e7a2-230">In caso contrario, restituirà `$null`.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="8e7a2-231">Backup-Sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="8e7a2-231">Backup-Subscription</span></span> |<span data-ttu-id="8e7a2-232">Consente di risparmiare hello sottoscrizione Azure corrente nella hello `$Script:originalSubscription` variabile nell'ambito dello script. Questa funzione Salva la sottoscrizione di Azure corrente di hello (ottenuta da `Get-AzureSubscription -Current`) e il relativo account di archiviazione, nonché hello sottoscrizione viene modificato da questo script (archiviata nella variabile hello `$UserSpecifiedSubscription`) e il relativo account di archiviazione, nell'ambito dello script.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="8e7a2-233">Salvando i valori hello, è possibile utilizzare una funzione, ad esempio `Restore-Subscription`, toorestore hello corrente sottoscrizione e l'archiviazione account toocurrent stato originale se è stato modificato lo stato corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="8e7a2-234">Trovare-AzureVM</span><span class="sxs-lookup"><span data-stu-id="8e7a2-234">Find-AzureVM</span></span> |<span data-ttu-id="8e7a2-235">Ottiene hello specificato macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="8e7a2-236">Formato DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="8e7a2-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="8e7a2-237">Antepone data e ora tooa messaggio.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="8e7a2-238">Questa funzione è progettata per i messaggi scritti toohello flussi di errore e dettagliato.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="8e7a2-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="8e7a2-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="8e7a2-240">Assembla un database SQL di Azure di tooan tooconnect di stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="8e7a2-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="8e7a2-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="8e7a2-242">Nome dell'account di archiviazione prima di hello con modello di nome hello di hello restituisce "devtest*" (tra maiuscole e minuscole) nel gruppo di affinità o percorso specificato hello. Se hello "devtest*" account di archiviazione non corrisponde al percorso di hello o un gruppo di affinità, viene ignorato dalla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="8e7a2-243">È necessario specificare un percorso o un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="8e7a2-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="8e7a2-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="8e7a2-245">Restituisce uno strumento di comando toorun hello MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="8e7a2-246">Nuovo AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="8e7a2-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="8e7a2-247">Trova o crea una macchina virtuale nella sottoscrizione di hello che corrispondono ai valori nel file di configurazione JSON hello hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="8e7a2-248">Pubblicare-WebPackage</span><span class="sxs-lookup"><span data-stu-id="8e7a2-248">Publish-WebPackage</span></span> |<span data-ttu-id="8e7a2-249">Usa MsDeploy.exe e un sito web di pubblicazione del pacchetto. Sito Web tooa di ZIP file toodeploy risorse.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="8e7a2-250">Questa funzione non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-250">This function doesn't generate any output.</span></span> <span data-ttu-id="8e7a2-251">Se hello chiamata tooMSDeploy.exe non riesce, la funzione hello genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="8e7a2-252">tooget più dettagliati di output, utilizzare hello **-Verbose** opzione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="8e7a2-253">Pubblicar-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="8e7a2-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="8e7a2-254">Verificare i valori di parametro hello e quindi chiama hello **Publish-WebPackage** (funzione).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="8e7a2-255">Leggere-configFile</span><span class="sxs-lookup"><span data-stu-id="8e7a2-255">Read-ConfigFile</span></span> |<span data-ttu-id="8e7a2-256">Convalida il file di configurazione JSON hello e restituisce una tabella hash di valori selezionati.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="8e7a2-257">Ripristina-Subscription</span><span class="sxs-lookup"><span data-stu-id="8e7a2-257">Restore-Subscription</span></span> |<span data-ttu-id="8e7a2-258">Reimposta hello sottoscrizione toohello originale abbonamento.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="8e7a2-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="8e7a2-259">Test-AzureModule</span></span> |<span data-ttu-id="8e7a2-260">Restituisce `$true` se hello installato la versione del modulo Azure è 0.7.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="8e7a2-261">Restituisce `$false` se il modulo di hello non è installato o è una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="8e7a2-262">Questa funzione non ha parametri.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-262">This function has no parameters.</span></span> |
| <span data-ttu-id="8e7a2-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="8e7a2-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="8e7a2-264">Restituisce `$true` se hello versione di hello modulo Azure è 0.7.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="8e7a2-265">Restituisce `$false` se il modulo di hello non è installato o è una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="8e7a2-266">Questa funzione non ha parametri.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-266">This function has no parameters.</span></span> |
| <span data-ttu-id="8e7a2-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="8e7a2-267">Test-HttpsUrl</span></span> |<span data-ttu-id="8e7a2-268">Converte l'oggetto System. Uri tooa hello input URL.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="8e7a2-269">Restituisce `$True` se hello URL è assoluto e relativo schema è https.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="8e7a2-270">Restituisce `$false` se hello URL è relativo, lo schema non è HTTPS o stringa di input hello non può essere convertito tooa URL.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="8e7a2-271">Test- Member</span><span class="sxs-lookup"><span data-stu-id="8e7a2-271">Test-Member</span></span> |<span data-ttu-id="8e7a2-272">Restituisce `$true` se una proprietà o metodo è un membro dell'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="8e7a2-273">In caso contrario, restituisce `$false`.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="8e7a2-274">Scrivere-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="8e7a2-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="8e7a2-275">Scrive un messaggio di errore preceduto hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="8e7a2-276">Questa funzione chiama hello **Format-DevTestMessageWithTime** ora hello tooprepend di funzione prima di scrivere il flusso di errore toohello messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="8e7a2-277">Scrivere-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="8e7a2-277">Write-HostWithTime</span></span> |<span data-ttu-id="8e7a2-278">Scrive un programma host di messaggio toohello (**Write-Host**) preceduti hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="8e7a2-279">Hello effetto della scrittura del programma host toohello varia.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="8e7a2-280">La maggior parte dei programmi che ospitano Windows PowerShell di scrittura questi messaggi toostandard output.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="8e7a2-281">Scrivere-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="8e7a2-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="8e7a2-282">Scrive un messaggio dettagliato preceduto hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="8e7a2-283">Poiché chiama **Write-Verbose**, il messaggio hello viene visualizzato solo quando viene eseguito uno script hello con hello **Verbose** parametro o quando hello **VerbosePreference** preferenza è impostare troppo**continua**.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="8e7a2-284">**Pubblicare-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="8e7a2-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="8e7a2-285">Nome della funzione</span><span class="sxs-lookup"><span data-stu-id="8e7a2-285">Function name</span></span> | <span data-ttu-id="8e7a2-286">Description</span><span class="sxs-lookup"><span data-stu-id="8e7a2-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e7a2-287">Nuovo-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="8e7a2-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="8e7a2-288">Crea risorse di Azure, ad esempio una macchina virtuale o un sito Web.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="8e7a2-289">Nuovo-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="8e7a2-289">New-WebDeployPackage</span></span> |<span data-ttu-id="8e7a2-290">Questa funzione non è implementata.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-290">This function isn't implemented.</span></span> <span data-ttu-id="8e7a2-291">È possibile aggiungere comandi in toobuild questa funzione al progetto.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="8e7a2-292">Pubblicare-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="8e7a2-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="8e7a2-293">Pubblica un tooAzure di applicazione web.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="8e7a2-294">Pubblicare-WebApplication</span><span class="sxs-lookup"><span data-stu-id="8e7a2-294">Publish-WebApplication</span></span> |<span data-ttu-id="8e7a2-295">Crea e distribuisce le app Web, le macchine virtuali, i database SQL e gli account di archiviazione per un progetto web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="8e7a2-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="8e7a2-296">Test-WebApplication</span></span> |<span data-ttu-id="8e7a2-297">Questa funzione non è implementata.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-297">This function isn't implemented.</span></span> <span data-ttu-id="8e7a2-298">È possibile aggiungere comandi in questo tootest funzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8e7a2-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8e7a2-299">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e7a2-299">Next steps</span></span>
<span data-ttu-id="8e7a2-300">Ulteriori informazioni sulla creazione di script PowerShell leggendo [Scripting con Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) e vedere altri script di PowerShell di Azure in hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="8e7a2-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
