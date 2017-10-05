---
title: Abilitare il debug remoto con il recapito continuo | Documentazione Microsoft
description: Informazioni su come abilitare il debug remoto quando si usa la distribuzione continua per la pubblicazione in Azure.
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 7a8a853a93e3e9915f687a20c871444e6a0de50d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-to-publish-to-azure"></a><span data-ttu-id="88fb3-103">Abilitare il debug remoto con la distribuzione continua per la pubblicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="88fb3-103">Enable remote debugging when using continuous delivery to publish to Azure</span></span>
<span data-ttu-id="88fb3-104">Per abilitare il debug remoto in Azure, per i servizi cloud o le macchine virtuali, quando si usa la [distribuzione continua](cloud-services-dotnet-continuous-delivery.md) per la pubblicazione in Azure, eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="88fb3-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) to publish to Azure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="88fb3-105">Abilitazione del debug remoto per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="88fb3-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="88fb3-106">Nell'agente di compilazione configurare l'ambiente iniziale per Azure come descritto in [Compilazione da riga di comando per Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="88fb3-106">On the build agent, set up the initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="88fb3-107">Poiché il pacchetto richiede l'installazione del runtime di debug remoto (msvsmon.exe), installare **Remote Tools per Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="88fb3-107">Because the remote debug runtime (msvsmon.exe) is required for the package, install the **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="88fb3-108">Remote Tools per Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="88fb3-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="88fb3-109">Remote Tools per Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="88fb3-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="88fb3-110">Remote Tools per Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="88fb3-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="88fb3-111">In alternativa, copiare i binari di debug remoto da un sistema in cui è installato Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88fb3-111">As an alternative, you can copy the remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="88fb3-112">Creare un certificato come descritto in [Panoramica dei certificati per servizi cloud di Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="88fb3-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="88fb3-113">Mantenere il file con estensione pfx e l'identificazione personale del certificato RDP e caricare il certificato nel servizio cloud di destinazione.</span><span class="sxs-lookup"><span data-stu-id="88fb3-113">Keep the .pfx and RDP certificate thumbprint and upload the certificate to the target cloud service.</span></span>
4. <span data-ttu-id="88fb3-114">Nella riga di comando MSBuild usare le opzioni seguenti per eseguire la compilazione e creare un pacchetto con il debug remoto abilitato.</span><span class="sxs-lookup"><span data-stu-id="88fb3-114">Use the following options in the MSBuild command line to build and package with remote debug enabled.</span></span> <span data-ttu-id="88fb3-115">Sostituire i percorsi effettivi ai file di progetto e di sistema per gli elementi racchiusi tra parentesi angolari.</span><span class="sxs-lookup"><span data-stu-id="88fb3-115">(Substitute actual paths to your system and project files for the angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of the certificate added to the cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path to your VS solution file>"
   
    <span data-ttu-id="88fb3-116">`VSX64RemoteDebuggerPath` è il percorso della cartella contenente msvsmon.exe in Remote Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88fb3-116">`VSX64RemoteDebuggerPath` is the path to the folder containing msvsmon.exe in the Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="88fb3-117">`RemoteDebuggerConnectorVersion` è la versione di Azure SDK nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="88fb3-117">`RemoteDebuggerConnectorVersion` is the Azure SDK version in your cloud service.</span></span> <span data-ttu-id="88fb3-118">Deve corrispondere anche alla versione installata con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88fb3-118">It should also match the version installed with Visual Studio.</span></span>
5. <span data-ttu-id="88fb3-119">Eseguire la pubblicazione nel servizio cloud di destinazione usando il pacchetto e il file di configurazione (CSCFG) generato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="88fb3-119">Publish to the target cloud service by using the package and .cscfg file generated in the previous step.</span></span>
6. <span data-ttu-id="88fb3-120">Importare il certificato (file PFX) nel computer in cui è installato Visual Studio con Azure SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="88fb3-120">Import the certificate (.pfx file) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="88fb3-121">Assicurarsi di eseguire l'importazione nell'archivio certificati `CurrentUser\My` , in caso contrario il collegamento al debugger di Visual Studio avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="88fb3-121">Make sure to import to the `CurrentUser\My` certificate store, otherwise attaching to the debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="88fb3-122">Abilitazione del debug remoto per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="88fb3-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="88fb3-123">Creare una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="88fb3-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="88fb3-124">Per informazioni, vedere l'articolo su come [creare una macchina virtuale che esegue Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) oppure l'articolo su come [Creare e gestire macchine virtuali di Azure in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="88fb3-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="88fb3-125">Nella [pagina del portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=269851)visualizzare il dashboard della macchina virtuale per individuare **L’IDENTIFICAZIONE PERSONALE CERTIFICATO RDP**della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="88fb3-125">On the [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view the virtual machine's dashboard to see the virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="88fb3-126">Questo valore viene utilizzato per il valore `ServerThumbprint` nella configurazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="88fb3-126">This value is used for the `ServerThumbprint` value in the extension configuration.</span></span>
3. <span data-ttu-id="88fb3-127">Creare un certificato client come descritto in [Panoramica sui certificati per i servizi cloud di Azure](cloud-services-certs-create.md) (conservare il file .pfx e l'identificazione personale del certificato RDP).</span><span class="sxs-lookup"><span data-stu-id="88fb3-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep the .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="88fb3-128">Installare Azure Powershell (versione 0.7.4 o versione successiva) come descritto in [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="88fb3-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="88fb3-129">Eseguire lo script seguente per abilitare l'estensione RemoteDebug.</span><span class="sxs-lookup"><span data-stu-id="88fb3-129">Run the following script to enable the RemoteDebug extension.</span></span> <span data-ttu-id="88fb3-130">Sostituire i percorsi e i dati personali con i dati personali dell'utente, ad esempio nome della sottoscrizione, nome del servizio e identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="88fb3-130">Replace the paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="88fb3-131">Questo script è configurato per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="88fb3-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="88fb3-132">Se si usa Visual Studio 2013 o Visual Studio 2017, modificare le assegnazioni `$referenceName` e `$extensionName` seguenti in `RemoteDebugVS2013` o `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="88fb3-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify the `$referenceName` and `$extensionName` assignments below to `RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="88fb3-133">Importare il certificato (file PFX) nel computer in cui è installato Visual Studio con Azure SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="88fb3-133">Import the certificate (.pfx) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

