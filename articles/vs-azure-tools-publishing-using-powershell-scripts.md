---
title: Uso degli script di Windows PowerShell per la pubblicazione in ambienti di sviluppo e test | Documentazione Microsoft
description: Informazioni su come utilizzare gli script di Windows PowerShell da Visual Studio per pubblicare allo sviluppo e gli ambienti di prova.
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
ms.openlocfilehash: d4c39eb7a8bc97a980061872ba0f32f375e6976f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="3c05d-103">Uso degli script di Windows PowerShell per la pubblicazione in ambienti di sviluppo e test</span><span class="sxs-lookup"><span data-stu-id="3c05d-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="3c05d-104">Quando si crea un'applicazione web in Visual Studio, è possibile generare uno script Windows PowerShell che può essere utilizzato in un secondo momento per automatizzare la pubblicazione del sito Web in Azure come un'applicazione Web nel servizio App Azure o una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3c05d-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="3c05d-105">È possibile modificare ed estendere lo script di Windows PowerShell nell'editor di Visual Studio in base alle proprie esigenze o integrare lo script di compilazione esistente, il test e la pubblicazione di script.</span><span class="sxs-lookup"><span data-stu-id="3c05d-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="3c05d-106">Utilizzando questi script, è possibile eseguire il provisioning (noto anche come ambienti di sviluppo e test) di versioni personalizzate del sito per un utilizzo temporaneo.</span><span class="sxs-lookup"><span data-stu-id="3c05d-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="3c05d-107">Ad esempio, si potrebbe impostare una particolare versione del sito Web in una macchina virtuale di Azure o in una slot di gestione temporanea in un sito Web per eseguire un gruppo di test, riprodurre un bug, testare una correzione di bug, una versione di valutazione di una modifica proposta o configurare un ambiente personalizzato per una dimostrazione o una presentazione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="3c05d-108">Dopo aver creato uno script che pubblica il progetto, è possibile ricreare ambienti identici eseguendo nuovamente lo script in base alle esigenze o eseguire lo script con la build dell'applicazione web per creare un ambiente di test personalizzato.</span><span class="sxs-lookup"><span data-stu-id="3c05d-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3c05d-109">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="3c05d-109">What you need</span></span>
* <span data-ttu-id="3c05d-110">Azure SDK 2.3 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="3c05d-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="3c05d-111">Per altre informazioni vedere [Scaricare Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384).</span><span class="sxs-lookup"><span data-stu-id="3c05d-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="3c05d-112">Non è necessario Azure SDK per generare script per i progetti web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="3c05d-113">Questa funzionalità è per i progetti web, non per i ruoli web nei servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="3c05d-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="3c05d-114">Azure PowerShell 0.7.4 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="3c05d-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="3c05d-115">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="3c05d-115">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="3c05d-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="3c05d-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="3c05d-117">Strumenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="3c05d-117">Additional tools</span></span>
<span data-ttu-id="3c05d-118">Sono disponibili altri strumenti e risorse per l'utilizzo di PowerShell in Visual Studio per lo sviluppo in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c05d-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="3c05d-119">Vedere [PowerShell Tools per Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="3c05d-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="3c05d-120">Come generare script di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="3c05d-120">Generating the publish scripts</span></span>
<span data-ttu-id="3c05d-121">È possibile generare gli script di pubblicazione per una macchina virtuale che ospita il sito Web quando si crea un nuovo progetto seguendo [queste istruzioni](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3c05d-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="3c05d-122">È possibile anche [generare script di pubblicazione per le app Web del Servizio app di Azure](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3c05d-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="3c05d-123">Script generati da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c05d-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="3c05d-124">Visual Studio genera una cartella a livello di soluzione denominata **PublishScripts** che contiene due file di Windows PowerShell, uno script di pubblicazione per la macchina virtuale o sito Web e un modulo che contiene funzioni che è possibile utilizzare negli script.</span><span class="sxs-lookup"><span data-stu-id="3c05d-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="3c05d-125">Visual Studio genera inoltre un file in formato JSON che specifica i dettagli del progetto in distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="3c05d-126">Pubblicazione di script da parte di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c05d-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="3c05d-127">Lo script di pubblicazione contiene specifici passaggi di pubblicazione per la distribuzione in una macchina virtuale o in un sito Web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="3c05d-128">Visual Studio fornisce la colorazione della sintassi per lo sviluppo di Windows PowerShell .</span><span class="sxs-lookup"><span data-stu-id="3c05d-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="3c05d-129">La Guida per le funzioni è disponibile, ed è possibile modificare liberamente le funzioni nello script per adattarle ai propri requisiti.</span><span class="sxs-lookup"><span data-stu-id="3c05d-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="3c05d-130">Modulo di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c05d-130">Windows PowerShell module</span></span>
<span data-ttu-id="3c05d-131">Il modulo Windows PowerShell generato da Visual Studio contiene funzioni che utilizzano lo script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="3c05d-132">Queste sono le funzioni di Azure PowerShell e non possono essere modificate.</span><span class="sxs-lookup"><span data-stu-id="3c05d-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="3c05d-133">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="3c05d-133">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="3c05d-134">File di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="3c05d-134">JSON configuration file</span></span>
<span data-ttu-id="3c05d-135">Il file JSON viene creato nella cartella **Configurazioni** e contiene dati di configurazione che consentono di specificare esattamente quali risorse distribuire in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c05d-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="3c05d-136">Il nome del file generato da Visual Studio è project-name-WAWS-dev. json se è stato creato un sito Web, o project name-VM-dev.json se è stata creata una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3c05d-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="3c05d-137">Di seguito è riportato un esempio di un file di configurazione JSON generato quando si crea un sito Web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="3c05d-138">La maggior parte dei valori è facilmente comprensibile.</span><span class="sxs-lookup"><span data-stu-id="3c05d-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="3c05d-139">Il nome del sito Web viene generato da Azure, pertanto potrebbe non corrispondere al nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="3c05d-139">The website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="3c05d-140">Quando si crea una macchina virtuale, il file di configurazione JSON è simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="3c05d-141">Si noti che viene creato un servizio cloud come contenitore per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3c05d-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="3c05d-142">La macchina virtuale contiene i consueti endpoint per l'accesso web tramite HTTP e HTTPS, come pure gli endpoint per distribuzione Web, che consente di pubblicare nel sito Web dal computer locale, Desktop remoto e Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c05d-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="3c05d-143">È possibile modificare la configurazione JSON per modificare l'operazione eseguita quando si eseguono gli script di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="3c05d-144">Le sezioni `cloudService` e `virtualMachine` sono necessarie, ma è possibile eliminare la sezione `databases` se non è necessario.</span><span class="sxs-lookup"><span data-stu-id="3c05d-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="3c05d-145">Le proprietà che sono vuote nel file di configurazione predefinito generato da Visual Studio sono facoltative; quelle che dispongono di valori nel file di configurazione predefinite sono necessarie.</span><span class="sxs-lookup"><span data-stu-id="3c05d-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="3c05d-146">Se si dispone di un sito Web che dispone di più ambienti di distribuzione (noti come slot) anziché di un unico sito di produzione in Azure, è possibile includere il nome dello slot nel nome del sito Web nel file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="3c05d-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="3c05d-147">Ad esempio, se si dispone di un sito Web denominato **mysite** e uno slot denominato **test**, l'URI è mysite test.cloudapp.net, ma il nome corretto da usare nel file di configurazione è mysite(test).</span><span class="sxs-lookup"><span data-stu-id="3c05d-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="3c05d-148">È possibile eseguire questo solo se il sito Web e gli slot sono già presenti nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="3c05d-149">Se non sono presenti, creare il sito Web eseguendo lo script senza specificare lo slot, quindi creare lo slot nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885)e successivamente eseguire lo script con il nome del sito Web modificato.</span><span class="sxs-lookup"><span data-stu-id="3c05d-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="3c05d-150">Per altre informazioni sugli slot di distribuzione per le app Web, vedere [Configurare ambienti di gestione temporanea per le app Web del Servizio app di Azure](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3c05d-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="3c05d-151">Come eseguire gli script di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="3c05d-151">How to run the publish scripts</span></span>
<span data-ttu-id="3c05d-152">Se non è stato eseguito prima uno script Windows PowerShell, è innanzitutto necessario impostare i criteri di esecuzione per consentire l'esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="3c05d-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="3c05d-153">Questa è una funzionalità di sicurezza per impedire agli utenti di eseguire script di Windows PowerShell se sono vulnerabili a malware o virus che comportano l'esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="3c05d-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="3c05d-154">Esecuzione dello script</span><span class="sxs-lookup"><span data-stu-id="3c05d-154">Run the script</span></span>
1. <span data-ttu-id="3c05d-155">Creare il pacchetto di distribuzione Web per il progetto.</span><span class="sxs-lookup"><span data-stu-id="3c05d-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="3c05d-156">Un pacchetto di distribuzione Web è un archivio compresso (con estensione zip) che contiene i file che si desidera copiare in una macchina virtuale o il sito Web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="3c05d-157">È possibile creare pacchetti di distribuzione Web in Visual Studio per qualsiasi applicazione web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Creare pacchetto di distribuzione web](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="3c05d-159">Per ulteriori informazioni, vedere [Procedura: Creare un pacchetto di distribuzione Web in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c05d-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="3c05d-160">È anche possibile automatizzare la creazione del pacchetto di distribuzione Web, come descritto nella sezione **Personalizzazione ed estensione degli script di pubblicazione** più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="3c05d-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="3c05d-161">In **Esplora soluzioni** aprire il menu di scelta rapida per lo script e quindi scegliere **Apri con PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="3c05d-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="3c05d-162">Se questa è la prima volta che sono stati eseguiti gli script di Windows PowerShell su questo computer, aprire una finestra del prompt dei comandi con privilegi di amministratore e digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3c05d-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="3c05d-163">Accedere ad Azure usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="3c05d-164">Quando richiesto, fornire nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="3c05d-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="3c05d-165">Si noti che quando si automatizza lo script, questo metodo per fornire credenziali di Azure non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="3c05d-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="3c05d-166">Al contrario, utilizzare il file. publishsettings per fornire le credenziali.</span><span class="sxs-lookup"><span data-stu-id="3c05d-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="3c05d-167">Una sola volta, si usa il comando **Get-AzurePublishSettingsFile** per scaricare il file da Azure e quindi **Import-AzurePublishSettingsFile** per importare il file.</span><span class="sxs-lookup"><span data-stu-id="3c05d-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="3c05d-168">Per istruzioni dettagliate, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c05d-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="3c05d-169">(Facoltativo) Se si vuole creare risorse con Azure, ad esempio la macchina virtuale, il database e il sito Web senza pubblicare l'applicazione Web, usare il comando **Publish-WebApplication.ps1** con l'argomento **-Configuration** impostato sul file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="3c05d-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="3c05d-170">Questa riga di comando utilizza il file di configurazione JSON per determinare le risorse da creare.</span><span class="sxs-lookup"><span data-stu-id="3c05d-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="3c05d-171">Poiché utilizza le impostazioni predefinite per gli altri argomenti della riga di comando, crea le risorse, ma non pubblica l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="3c05d-172">L’opzione Verbose  fornisce ulteriori informazioni sulle attività in corso.</span><span class="sxs-lookup"><span data-stu-id="3c05d-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="3c05d-173">Utilizzare il comando **Pubblica WebApplication.ps1** come indicato in uno dei seguenti esempi per richiamare lo script e pubblicare l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="3c05d-174">Se è necessario eseguire l'override delle impostazioni predefinite per gli altri argomenti, ad esempio il nome della sottoscrizione, pubblicare il nome del pacchetto, le credenziali di macchina virtuale o le credenziali del server database, è possibile specificare tali parametri.</span><span class="sxs-lookup"><span data-stu-id="3c05d-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="3c05d-175">Utilizzare l’opzione **– Verbose** per visualizzare ulteriori informazioni sullo stato di avanzamento del processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="3c05d-176">Se si crea una macchina virtuale, il comando è simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="3c05d-177">In questo esempio viene inoltre illustrato come specificare le credenziali per più database.</span><span class="sxs-lookup"><span data-stu-id="3c05d-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="3c05d-178">Per le macchine virtuali create da questi script, il certificato SSL non è da un'autorità radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="3c05d-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="3c05d-179">Pertanto, è necessario utilizzare l’opzione **-AllowUntrusted** .</span><span class="sxs-lookup"><span data-stu-id="3c05d-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="3c05d-180">Lo script può creare database, ma non crea server di database.</span><span class="sxs-lookup"><span data-stu-id="3c05d-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="3c05d-181">Se si desidera creare un server di database, è possibile utilizzare la funzione **New-AzureSqlDatabaseServer** nel modulo di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c05d-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="3c05d-182">Personalizzazione ed estensione degli script di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="3c05d-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="3c05d-183">È possibile personalizzare lo script di pubblicazione e i file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="3c05d-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="3c05d-184">Le funzioni nel modulo Windows PowerShell **AzureWebAppPublishModule.psm1** non possono essere modificati.</span><span class="sxs-lookup"><span data-stu-id="3c05d-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="3c05d-185">Se si desidera specificare un database diverso o modificare alcune delle proprietà della macchina virtuale, modificare il file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="3c05d-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="3c05d-186">Se si desidera estendere le funzionalità dello script per automatizzare la compilazione e il test del progetto, è possibile implementare stub di funzioni in **Pubblica WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="3c05d-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="3c05d-187">Per automatizzare la compilazione del progetto, aggiungere il codice che chiama MSBuild `New-WebDeployPackage` come illustrato nell'esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="3c05d-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="3c05d-188">Il percorso del comando MSBuild è diverso a seconda della versione di Visual Studio installata.</span><span class="sxs-lookup"><span data-stu-id="3c05d-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="3c05d-189">Per ottenere il percorso corretto, è possibile utilizzare la funzione **Get-msbuildcmd come**, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="3c05d-190">Per automatizzare la compilazione del progetto</span><span class="sxs-lookup"><span data-stu-id="3c05d-190">To automate building your project</span></span>
1. <span data-ttu-id="3c05d-191">Aggiungere il parametro `$ProjectFile` nella sezione param globale.</span><span class="sxs-lookup"><span data-stu-id="3c05d-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="3c05d-192">Copiare la funzione `Get-MSBuildCmd` nel file di script.</span><span class="sxs-lookup"><span data-stu-id="3c05d-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="3c05d-193">Sostituire `New-WebDeployPackage` con il seguente codice e sostituire i segnaposto per la costruzione di riga `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="3c05d-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="3c05d-194">Questo codice è per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3c05d-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="3c05d-195">Se si usa Visual Studio 2013, modificare la proprietà **VisualStudioVersion** al di sotto di `12.0`.</span><span class="sxs-lookup"><span data-stu-id="3c05d-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="3c05d-196">Per compilare l'applicazione Web, usare MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="3c05d-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="3c05d-197">Per informazioni, vedere il riferimento della riga di comando di MSBuild all'indirizzo: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="3c05d-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="3c05d-198">Avviare l'esecuzione del comando di compilazione</span><span class="sxs-lookup"><span data-stu-id="3c05d-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="3c05d-199">Chiamare la funzione `New-WebDeployPackage` prima di questa riga: `$Config = Read-ConfigFile $Configuration` per le applicazioni web o `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3c05d-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="3c05d-200">Richiamare uno script personalizzato dalla riga di comando mediante il passaggio dell’argomento `$Project`, come nella seguente riga di comando di esempio.</span><span class="sxs-lookup"><span data-stu-id="3c05d-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="3c05d-201">Per automatizzare il test dell'applicazione, aggiungere codice al `Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="3c05d-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="3c05d-202">Assicurarsi di rimuovere il commento dalle righe in **Pubblica WebApplication.ps1** dove queste funzioni vengono chiamate.</span><span class="sxs-lookup"><span data-stu-id="3c05d-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="3c05d-203">Se non si fornisce un'implementazione, è possibile compilare manualmente il progetto con Visual Studio e quindi eseguire lo script per pubblicare in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c05d-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="3c05d-204">Riepilogo della funzione di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="3c05d-204">Publishing function summary</span></span>
<span data-ttu-id="3c05d-205">Per visualizzare la Guida per le funzioni è possibile utilizzare il prompt dei comandi Windows PowerShell, utilizzare il comando `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="3c05d-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="3c05d-206">Nella Guida sono inclusi esempi e informazioni sui parametri.</span><span class="sxs-lookup"><span data-stu-id="3c05d-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="3c05d-207">Lo stesso testo della Guida in linea è presente anche nei file di origine script **AzureWebAppPublishModule.psm1** e **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="3c05d-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="3c05d-208">Lo script e la Guida si trovano nella lingua di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c05d-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="3c05d-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="3c05d-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="3c05d-210">Nome della funzione</span><span class="sxs-lookup"><span data-stu-id="3c05d-210">Function name</span></span> | <span data-ttu-id="3c05d-211">Description</span><span class="sxs-lookup"><span data-stu-id="3c05d-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c05d-212">Aggiungere AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="3c05d-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="3c05d-213">Creare un nuovo database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3c05d-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="3c05d-214">Aggiungere AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="3c05d-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="3c05d-215">Crea database SQL di Azure da valori nel file di configurazione JSON generato da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c05d-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="3c05d-216">Aggiungere-AzureVM</span><span class="sxs-lookup"><span data-stu-id="3c05d-216">Add-AzureVM</span></span> |<span data-ttu-id="3c05d-217">Crea una macchina virtuale di Azure e restituisce l'URL della macchina virtuale distribuita.</span><span class="sxs-lookup"><span data-stu-id="3c05d-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="3c05d-218">La funzione imposta i prerequisiti e quindi chiama la funzione **New-AzureVM** (modulo di Azure) per creare una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3c05d-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="3c05d-219">Aggiungere AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="3c05d-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="3c05d-220">Aggiunge nuovi endpoint di input a una macchina virtuale e restituisce la macchina virtuale con il nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="3c05d-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="3c05d-221">Aggiungere AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="3c05d-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="3c05d-222">Crea un nuovo account di archiviazione di Azure nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="3c05d-223">Il nome dell'account inizia con "devtest" seguito da una stringa alfanumerica univoca.</span><span class="sxs-lookup"><span data-stu-id="3c05d-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="3c05d-224">La funzione restituisce il nome del nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="3c05d-225">È necessario specificare un percorso o un gruppo di affinità per il nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="3c05d-226">Aggiungere-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="3c05d-226">Add-AzureWebsite</span></span> |<span data-ttu-id="3c05d-227">Crea un sito Web con nome e percorso specificati.</span><span class="sxs-lookup"><span data-stu-id="3c05d-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="3c05d-228">Questa funzione chiama la funzione **New-AzureWebsite** nel modulo di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c05d-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="3c05d-229">Se la sottoscrizione non include già un sito Web con il nome specificato, questa funzione crea il sito Web e restituisce un oggetto sito Web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="3c05d-230">In caso contrario, restituirà `$null`.</span><span class="sxs-lookup"><span data-stu-id="3c05d-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="3c05d-231">Backup-Sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="3c05d-231">Backup-Subscription</span></span> |<span data-ttu-id="3c05d-232">Salva la sottoscrizione di Azure corrente nella variabile`$Script:originalSubscription` nell'ambito dello script. Questa funzione salva nell'ambito dello script la sottoscrizione di Azure corrente, ottenuta da `Get-AzureSubscription -Current`, e il relativo account di archiviazione nonché la sottoscrizione modificata da questo script, memorizzato nella variabile `$UserSpecifiedSubscription`, e il relativo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="3c05d-233">Salvando i valori, è possibile usare una funzione, ad esempio `Restore-Subscription`, per ripristinare allo stato corrente la sottoscrizione e l'account di archiviazione corrente originale se è stato modificato lo stato corrente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="3c05d-234">Trovare-AzureVM</span><span class="sxs-lookup"><span data-stu-id="3c05d-234">Find-AzureVM</span></span> |<span data-ttu-id="3c05d-235">Ottiene la macchina virtuale di Azure specificata.</span><span class="sxs-lookup"><span data-stu-id="3c05d-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="3c05d-236">Formato DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="3c05d-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="3c05d-237">Antepone la data e l’ora a un messaggio.</span><span class="sxs-lookup"><span data-stu-id="3c05d-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="3c05d-238">Questa funzione è progettata per i messaggi scritti ai flussi di errore e dettagliati.</span><span class="sxs-lookup"><span data-stu-id="3c05d-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="3c05d-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="3c05d-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="3c05d-240">Assembla una stringa di connessione per connettersi a un database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3c05d-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="3c05d-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="3c05d-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="3c05d-242">Restituisce il nome del primo account di archiviazione con il modello di nome "devtest*", senza distinzione maiuscole/minuscole, nel percorso o nel gruppo di affinità specificato. Se l'account di archiviazione "devtest*" non corrisponde alla posizione o al gruppo di affinità, la funzione lo ignora.</span><span class="sxs-lookup"><span data-stu-id="3c05d-242">Returns the name of the first storage account with the name pattern "devtest*" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="3c05d-243">È necessario specificare un percorso o un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="3c05d-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="3c05d-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="3c05d-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="3c05d-245">Restituisce un comando per eseguire lo strumento MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="3c05d-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="3c05d-246">Nuovo AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="3c05d-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="3c05d-247">Trova o crea una macchina virtuale nella sottoscrizione che corrisponde ai valori nel file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="3c05d-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="3c05d-248">Pubblicare-WebPackage</span><span class="sxs-lookup"><span data-stu-id="3c05d-248">Publish-WebPackage</span></span> |<span data-ttu-id="3c05d-249">Utilizza MsDeploy.exe e un file Zip del pacchetto di pubblicazione web per distribuire le risorse a un sito Web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="3c05d-250">Questa funzione non genera alcun output.</span><span class="sxs-lookup"><span data-stu-id="3c05d-250">This function doesn't generate any output.</span></span> <span data-ttu-id="3c05d-251">Se la chiamata a MSDeploy.exe non riesce, la funzione genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="3c05d-252">Per ottenere un output più dettagliato, utilizzare l’opzione **-Verbose** .</span><span class="sxs-lookup"><span data-stu-id="3c05d-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="3c05d-253">Pubblicar-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="3c05d-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="3c05d-254">Verifica i valori di parametro e chiama quindi la funzione **Publish-WebPackage** .</span><span class="sxs-lookup"><span data-stu-id="3c05d-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="3c05d-255">Leggere-configFile</span><span class="sxs-lookup"><span data-stu-id="3c05d-255">Read-ConfigFile</span></span> |<span data-ttu-id="3c05d-256">Convalida il file di configurazione JSON e restituisce una tabella hash di valori selezionati.</span><span class="sxs-lookup"><span data-stu-id="3c05d-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="3c05d-257">Ripristina-Subscription</span><span class="sxs-lookup"><span data-stu-id="3c05d-257">Restore-Subscription</span></span> |<span data-ttu-id="3c05d-258">Reimposta la sottoscrizione corrente a quella originale.</span><span class="sxs-lookup"><span data-stu-id="3c05d-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="3c05d-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="3c05d-259">Test-AzureModule</span></span> |<span data-ttu-id="3c05d-260">Restituisce `$true` se la versione del modulo Azure installata è 0.7.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="3c05d-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="3c05d-261">Restituisce `$false` Se il modulo non è installato o è una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="3c05d-262">Questa funzione non ha parametri.</span><span class="sxs-lookup"><span data-stu-id="3c05d-262">This function has no parameters.</span></span> |
| <span data-ttu-id="3c05d-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="3c05d-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="3c05d-264">Restituisce `$true` se la versione del modulo Azure è 0.7.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="3c05d-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="3c05d-265">Restituisce `$false` Se il modulo non è installato o è una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="3c05d-266">Questa funzione non ha parametri.</span><span class="sxs-lookup"><span data-stu-id="3c05d-266">This function has no parameters.</span></span> |
| <span data-ttu-id="3c05d-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="3c05d-267">Test-HttpsUrl</span></span> |<span data-ttu-id="3c05d-268">Converte l'URL di input in un oggetto System. Uri.</span><span class="sxs-lookup"><span data-stu-id="3c05d-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="3c05d-269">Restituisce `$True` se l'URL è assoluto e il relativo schema è https.</span><span class="sxs-lookup"><span data-stu-id="3c05d-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="3c05d-270">Restituisce `$false` se l'URL è relativo, lo schema non è HTTPS o la stringa di input non può essere convertita in un URL.</span><span class="sxs-lookup"><span data-stu-id="3c05d-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="3c05d-271">Test- Member</span><span class="sxs-lookup"><span data-stu-id="3c05d-271">Test-Member</span></span> |<span data-ttu-id="3c05d-272">Restituisce `$true` se una proprietà o metodo è un membro dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="3c05d-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="3c05d-273">In caso contrario, restituisce `$false`.</span><span class="sxs-lookup"><span data-stu-id="3c05d-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="3c05d-274">Scrivere-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="3c05d-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="3c05d-275">Scrive un messaggio di errore prefisso con l'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="3c05d-276">Questa funzione chiama la funzione **Format-DevTestMessageWithTime** per anteporre il tempo prima della scrittura del messaggio per il flusso di errore.</span><span class="sxs-lookup"><span data-stu-id="3c05d-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="3c05d-277">Scrivere-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="3c05d-277">Write-HostWithTime</span></span> |<span data-ttu-id="3c05d-278">Scrive un messaggio nel programma host (**Write-Host**) prestabilito con l'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="3c05d-279">L'effetto della scrittura nel programma host varia.</span><span class="sxs-lookup"><span data-stu-id="3c05d-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="3c05d-280">La maggior parte dei programmi che ospitano Windows PowerShell scrive questi messaggi nell'output standard.</span><span class="sxs-lookup"><span data-stu-id="3c05d-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="3c05d-281">Scrivere-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="3c05d-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="3c05d-282">Scrive un messaggio dettagliato con l'ora corrente.</span><span class="sxs-lookup"><span data-stu-id="3c05d-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="3c05d-283">Poiché chiama **Write-Verbose**, il messaggio viene visualizzato solo quando lo script viene eseguito con il parametro **Verbose** o quando la preferenza **VerbosePreference** è impostata su **Continua**.</span><span class="sxs-lookup"><span data-stu-id="3c05d-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="3c05d-284">**Pubblicare-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="3c05d-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="3c05d-285">Nome della funzione</span><span class="sxs-lookup"><span data-stu-id="3c05d-285">Function name</span></span> | <span data-ttu-id="3c05d-286">Description</span><span class="sxs-lookup"><span data-stu-id="3c05d-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c05d-287">Nuovo-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="3c05d-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="3c05d-288">Crea risorse di Azure, ad esempio una macchina virtuale o un sito Web.</span><span class="sxs-lookup"><span data-stu-id="3c05d-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="3c05d-289">Nuovo-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="3c05d-289">New-WebDeployPackage</span></span> |<span data-ttu-id="3c05d-290">Questa funzione non è implementata.</span><span class="sxs-lookup"><span data-stu-id="3c05d-290">This function isn't implemented.</span></span> <span data-ttu-id="3c05d-291">È possibile aggiungere comandi in questa funzione per compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="3c05d-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="3c05d-292">Pubblicare-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="3c05d-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="3c05d-293">Pubblicare un'applicazione Web in Azure</span><span class="sxs-lookup"><span data-stu-id="3c05d-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="3c05d-294">Pubblicare-WebApplication</span><span class="sxs-lookup"><span data-stu-id="3c05d-294">Publish-WebApplication</span></span> |<span data-ttu-id="3c05d-295">Crea e distribuisce le app Web, le macchine virtuali, i database SQL e gli account di archiviazione per un progetto web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c05d-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="3c05d-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="3c05d-296">Test-WebApplication</span></span> |<span data-ttu-id="3c05d-297">Questa funzione non è implementata.</span><span class="sxs-lookup"><span data-stu-id="3c05d-297">This function isn't implemented.</span></span> <span data-ttu-id="3c05d-298">È possibile aggiungere comandi in questa funzione per testare l’applicazione.</span><span class="sxs-lookup"><span data-stu-id="3c05d-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3c05d-299">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c05d-299">Next steps</span></span>
<span data-ttu-id="3c05d-300">Per altre informazioni sulla creazione di script PowerShell, leggere [Scripting con Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) e vedere gli altri script di Azure PowerShell nello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="3c05d-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
