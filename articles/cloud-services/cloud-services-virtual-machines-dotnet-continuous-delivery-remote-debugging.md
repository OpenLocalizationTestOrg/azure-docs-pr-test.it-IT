---
title: debug remoto con il recapito continuo aaaEnable | Documenti Microsoft
description: Informazioni su come tooenable il debug remoto quando si utilizza il recapito continuo toodeploy tooAzure
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
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="80b9c-103">Abilitare il debug remoto quando si utilizza il recapito continuo toopublish tooAzure</span><span class="sxs-lookup"><span data-stu-id="80b9c-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="80b9c-104">È possibile abilitare il debug remoto in Azure, per i servizi cloud o macchine virtuali, quando si utilizza [il recapito continuo](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish attenendosi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="80b9c-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="80b9c-105">Abilitazione del debug remoto per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="80b9c-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="80b9c-106">Agente di compilazione hello, configurare hello iniziale ambiente per Azure come descritto [della riga di comando di compilazione per Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="80b9c-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="80b9c-107">Poiché il runtime di eseguire il debug remoto hello (msvsmon.exe) è obbligatorio per il pacchetto di hello, installare hello **Remote Tools per Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="80b9c-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="80b9c-108">Remote Tools per Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="80b9c-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="80b9c-109">Remote Tools per Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="80b9c-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="80b9c-110">Remote Tools per Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="80b9c-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="80b9c-111">In alternativa, è possibile copiare i file binari di debug remoto di hello da un sistema che è installato Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80b9c-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="80b9c-112">Creare un certificato come descritto in [Panoramica dei certificati per servizi cloud di Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="80b9c-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="80b9c-113">Mantenere PFX hello e identificazione personale del certificato RDP e caricare il servizio cloud destinazione di hello certificato toohello.</span><span class="sxs-lookup"><span data-stu-id="80b9c-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="80b9c-114">Utilizzare hello seguenti opzioni nel toobuild riga di comando di MSBuild hello e pacchetto con il debug remoto abilitato.</span><span class="sxs-lookup"><span data-stu-id="80b9c-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="80b9c-115">(Sostituire i percorsi effettivi tooyour progetto file di sistema e per gli elementi racchiusi tra parentesi quadre angolo hello).</span><span class="sxs-lookup"><span data-stu-id="80b9c-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="80b9c-116">`VSX64RemoteDebuggerPath`è cartella toohello hello contenente msvsmon.exe in hello Remote Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80b9c-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="80b9c-117">`RemoteDebuggerConnectorVersion`è hello Azure SDK versione nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="80b9c-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="80b9c-118">Deve inoltre corrispondere a versione hello installata con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80b9c-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="80b9c-119">Pubblicazione servizio cloud di destinazione toohello tramite file di pacchetto e un file con estensione cscfg di hello generato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="80b9c-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="80b9c-120">Importare hello certificato (file con estensione pfx) toohello macchina che dispone di Visual Studio con Azure SDK per .NET sia installato.</span><span class="sxs-lookup"><span data-stu-id="80b9c-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="80b9c-121">Verificare che tooimport toohello `CurrentUser\My` archivio certificati, in caso contrario collegamento toohello debugger in Visual Studio avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="80b9c-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="80b9c-122">Abilitazione del debug remoto per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="80b9c-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="80b9c-123">Creare una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="80b9c-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="80b9c-124">Per informazioni, vedere l'articolo su come [creare una macchina virtuale che esegue Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) oppure l'articolo su come [Creare e gestire macchine virtuali di Azure in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80b9c-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="80b9c-125">In hello [pagina del portale Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=269851), dashboard toosee hello della macchina virtuale della macchina virtuale hello visualizzare **identificazione personale del certificato RDP**.</span><span class="sxs-lookup"><span data-stu-id="80b9c-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="80b9c-126">Questo valore viene utilizzato per hello `ServerThumbprint` valore nella configurazione dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="80b9c-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="80b9c-127">Creare un certificato client, come indicato nella [panoramica dei certificati per servizi Cloud di Azure](cloud-services-certs-create.md) (mantenere PFX hello e identificazione personale del certificato RDP).</span><span class="sxs-lookup"><span data-stu-id="80b9c-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="80b9c-128">Installare Azure Powershell (versione 0.7.4 o successiva) come descritto [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80b9c-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="80b9c-129">Eseguire hello seguente estensione RemoteDebug hello tooenable di script.</span><span class="sxs-lookup"><span data-stu-id="80b9c-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="80b9c-130">Sostituire i percorsi di hello e dati personali con valori personalizzati, ad esempio il nome della sottoscrizione, nome del servizio e l'identificazione digitale.</span><span class="sxs-lookup"><span data-stu-id="80b9c-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="80b9c-131">Questo script è configurato per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="80b9c-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="80b9c-132">Se si utilizza Visual Studio 2013 o Visual Studio 2017, modificare hello `$referenceName` e `$extensionName` assegnazioni seguenti troppo`RemoteDebugVS2013` o `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="80b9c-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="80b9c-133">Importa hello certificato (PFX) toohello macchina che dispone di Visual Studio con Azure SDK per .NET sia installato.</span><span class="sxs-lookup"><span data-stu-id="80b9c-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

