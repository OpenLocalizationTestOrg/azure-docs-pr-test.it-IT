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
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>Abilitare il debug remoto quando si utilizza il recapito continuo toopublish tooAzure
È possibile abilitare il debug remoto in Azure, per i servizi cloud o macchine virtuali, quando si utilizza [il recapito continuo](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish attenendosi alla procedura seguente.

## <a name="enabling-remote-debugging-for-cloud-services"></a>Abilitazione del debug remoto per i servizi cloud
1. Agente di compilazione hello, configurare hello iniziale ambiente per Azure come descritto [della riga di comando di compilazione per Azure](http://msdn.microsoft.com/library/hh535755.aspx).
2. Poiché il runtime di eseguire il debug remoto hello (msvsmon.exe) è obbligatorio per il pacchetto di hello, installare hello **Remote Tools per Visual Studio**.

    * [Remote Tools per Visual Studio 2017](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Remote Tools per Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Remote Tools per Visual Studio 2013 Update 5](https://www.microsoft.com/download/details.aspx?id=48156)
    
    In alternativa, è possibile copiare i file binari di debug remoto di hello da un sistema che è installato Visual Studio.

3. Creare un certificato come descritto in [Panoramica dei certificati per servizi cloud di Azure](cloud-services-certs-create.md). Mantenere PFX hello e identificazione personale del certificato RDP e caricare il servizio cloud destinazione di hello certificato toohello.
4. Utilizzare hello seguenti opzioni nel toobuild riga di comando di MSBuild hello e pacchetto con il debug remoto abilitato. (Sostituire i percorsi effettivi tooyour progetto file di sistema e per gli elementi racchiusi tra parentesi quadre angolo hello).
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`è cartella toohello hello contenente msvsmon.exe in hello Remote Tools per Visual Studio.
    `RemoteDebuggerConnectorVersion`è hello Azure SDK versione nel servizio cloud. Deve inoltre corrispondere a versione hello installata con Visual Studio.
5. Pubblicazione servizio cloud di destinazione toohello tramite file di pacchetto e un file con estensione cscfg di hello generato nel passaggio precedente hello.
6. Importare hello certificato (file con estensione pfx) toohello macchina che dispone di Visual Studio con Azure SDK per .NET sia installato. Verificare che tooimport toohello `CurrentUser\My` archivio certificati, in caso contrario collegamento toohello debugger in Visual Studio avrà esito negativo.

## <a name="enabling-remote-debugging-for-virtual-machines"></a>Abilitazione del debug remoto per le macchine virtuali
1. Creare una macchina virtuale di Azure. Per informazioni, vedere l'articolo su come [creare una macchina virtuale che esegue Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) oppure l'articolo su come [Creare e gestire macchine virtuali di Azure in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
2. In hello [pagina del portale Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=269851), dashboard toosee hello della macchina virtuale della macchina virtuale hello visualizzare **identificazione personale del certificato RDP**. Questo valore viene utilizzato per hello `ServerThumbprint` valore nella configurazione dell'estensione hello.
3. Creare un certificato client, come indicato nella [panoramica dei certificati per servizi Cloud di Azure](cloud-services-certs-create.md) (mantenere PFX hello e identificazione personale del certificato RDP).
4. Installare Azure Powershell (versione 0.7.4 o successiva) come descritto [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
5. Eseguire hello seguente estensione RemoteDebug hello tooenable di script. Sostituire i percorsi di hello e dati personali con valori personalizzati, ad esempio il nome della sottoscrizione, nome del servizio e l'identificazione digitale.
   
   > [!NOTE]
   > Questo script è configurato per Visual Studio 2015. Se si utilizza Visual Studio 2013 o Visual Studio 2017, modificare hello `$referenceName` e `$extensionName` assegnazioni seguenti troppo`RemoteDebugVS2013` o `RemoteDebugVS2017`.

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

6. Importa hello certificato (PFX) toohello macchina che dispone di Visual Studio con Azure SDK per .NET sia installato.

