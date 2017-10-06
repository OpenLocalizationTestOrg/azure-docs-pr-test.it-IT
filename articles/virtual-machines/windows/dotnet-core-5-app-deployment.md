---
title: Distribuzione dell'applicazione con estensioni di macchine virtuali aaaAutomating | Documenti Microsoft
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Distribuzione di applicazioni con i modelli di Azure Resource Manager per macchine virtuali Windows

Una volta tutti i requisiti infrastrutturali Azure sono stati identificati e convertiti in un modello di distribuzione, distribuzione di applicazione reale hello deve toobe risolti. Distribuzione dell'applicazione qui fa riferimento a file binari dell'applicazione effettivo hello tooinstalling su risorse di Azure. Per esempio negozio hello, .net Core e IIS devono toobe installato e configurato in ogni macchina virtuale. Hello negozio file binari necessari toobe installato nella macchina virtuale hello e database dell'archivio di musica hello creato in precedenza.

Questo documento illustra in dettaglio come estensioni di macchine virtuali consente di automatizzare la distribuzione e configurazione tooAzure macchine virtuali dell'applicazione. Tutte le dipendenze e le configurazioni univoche sono evidenziate. Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello. è disponibili qui: modello completa Hello [musica archivio distribuzione in Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Script di configurazione
Estensioni di macchine virtuali sono programmi specializzati eseguite sui automazione configurazione tooprovide di macchine virtuali. Le estensioni sono disponibili per molti scopi specifici, ad esempio un programma antivirus, la configurazione della registrazione e la configurazione di Docker. Hello estensione Script personalizzato può essere utilizzato toorun qualsiasi a fronte di una macchina virtuale. Con l'esempio hello Negozio, è backup di macchine virtuali toohello script personalizzato estensione tooconfigure hello Windows e installare un'applicazione hello Negozio.

Prima che riporta in dettaglio come estensioni di macchine virtuali vengono dichiarate in un modello di gestione risorse di Azure, esaminare script hello che viene eseguito. Questo script configura hello toohost di macchina virtuale Windows hello applicazione Negozio. Durante l'esecuzione, script hello installa il software necessario tutte, installare un'applicazione hello musica archivio dal controllo del codice sorgente e preparare i database di hello. 

> Questo esempio è fornito a scopo dimostrativo.

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a>Estensione script della macchina virtuale
Le estensioni VM possibile eseguire in una macchina virtuale in fase di compilazione con l'inclusione di risorse di estensione hello nel modello di gestione risorse di Azure hello. Hello estensione può essere aggiunta con hello Visual Studio Aggiunta guidata risorsa o tramite l'inserimento di un oggetto JSON valido nel modello hello. risorse di estensione dello Script Hello è annidata all'interno di hello risorsa macchina virtuale. può essere visto nell'esempio seguente hello.

Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [estensione della macchina virtuale Script](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Si noti che in hello seguito JSON che hello script viene archiviato in GitHub. Questo script può essere incluso anche nell'archiviazione BLOB di Azure. Inoltre, i modelli di gestione risorse di Azure consentono hello script esecuzione stringa toobe costruito in modo che i valori di parametri di modello possono essere usati come parametri per l'esecuzione dello script. In questo caso i dati vengono forniti durante la distribuzione di modelli di hello e questi valori possono quindi essere utilizzati durante l'esecuzione di script hello.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

Come indicato in precedenza, è anche possibile toostore script personalizzato nell'archiviazione Blob di Azure. Sono disponibili due opzioni per l'archiviazione di risorse di script hello nell'archiviazione blob. rendere pubblico contenitore/script hello e seguire hello stesso approccio sopra, o può anche essere conservato nell'archiviazione blob privato che richiede il tooprovide hello storageAccountName e storageAccountKey toohello CustomScriptExtension definizione di risorsa.

Nel seguente esempio hello è stato effettuato un passaggio ulteriormente. Sebbene sia possibile tooprovide nome account di archiviazione hello e la chiave come parametro o variabile durante la distribuzione, i modelli di gestione risorse forniscono hello `listKeys` funzione che è possibile ottenere l'account di archiviazione hello chiave a livello di codice e inserirlo in toohello modello per l'utente in fase di distribuzione.

Nell'esempio hello CustomScriptExtension definizione di risorsa seguente, lo script personalizzato è già stato caricato tooan account di archiviazione di Azure denominato `mystorageaccount9999` che esiste in un altro gruppo di risorse denominato `mysa999rgname`. Quando si distribuisce un modello che contiene la risorsa, hello `listKeys` funzione a livello di codice ottiene chiave dell'account di archiviazione per l'account di archiviazione hello hello `mystorageaccount9999` nel gruppo di risorse hello `mysa999rgname` e lo inserisce nel modello toohello per noi.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

vantaggio principale di Hello di questo approccio è che non richiede toochange è il modello o i parametri di distribuzione nell'evento hello di hello Modifica chiave account di archiviazione.

Per ulteriori informazioni sull'uso delle estensioni hello script personalizzato, vedere [le estensioni degli script personalizzati con modelli di gestione risorse](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Passaggio successivo
<hr>

[Explore More Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates)

