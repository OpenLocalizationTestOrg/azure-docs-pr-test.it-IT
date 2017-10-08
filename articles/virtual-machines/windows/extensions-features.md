---
title: "aaaVirtual computer estensioni e funzionalità per Windows in Azure | Documenti Microsoft"
description: "Informazioni sulle estensioni disponibili per le macchine virtuali di Azure, raggruppate in base a ciò che forniscono o migliorano."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Estensioni e funzionalità della macchina virtuale per Windows

Le estensioni della macchina virtuale di Azure sono piccole applicazioni che eseguono attività di configurazione e automazione post-distribuzione sulle macchine virtuali di Azure. Ad esempio, se una macchina virtuale richiede l'installazione del software, protezione antivirus o configurazione di Docker, un'estensione della macchina virtuale può essere utilizzato toocomplete queste attività. Le estensioni VM di Azure possono essere eseguite utilizzando hello CLI di Azure PowerShell, i modelli, Gestione risorse di Azure e hello portale di Azure. Le estensioni possono essere unite in bundle con una nuova distribuzione di macchina virtuale o eseguite su un sistema esistente.

Questo documento viene fornita una panoramica delle estensioni di macchina virtuale, i prerequisiti per l'utilizzo di estensioni di macchine virtuali e istruzioni su come gestire toodetect e rimuovere estensioni di macchina virtuale. Questo documento fornisce informazioni generali perché sono disponibili molte estensioni della macchina virtuale, ognuna con una configurazione potenzialmente univoca. Dettagli specifici dell'estensione sono disponibili in ogni estensione singoli toohello specifico di documento.

## <a name="use-cases-and-samples"></a>Casi d'uso ed esempi

Sono disponibili numerose estensioni della macchina virtuale di Azure, ognuna con un caso d'uso specifico. Alcuni esempi di casi d'uso sono:

- Applicare macchina virtuale di tooa configurazioni dello stato desiderato di PowerShell utilizzando l'estensione DSC hello per Windows. Per altre informazioni, vedere l'argomento relativo all'[Estensione DSC (Desired State Configuration) di Azure](extensions-dsc-overview.md).
- Configurare il monitoraggio di macchina virtuale utilizzando l'estensione di macchina virtuale di Microsoft Monitoring Agent hello. Per ulteriori informazioni, vedere [tooLog di macchine virtuali di Azure connettersi Analitica](../../log-analytics/log-analytics-azure-vm-extension.md).
- Configurare il monitoraggio dell'infrastruttura di Azure con estensione Datadog hello. Per ulteriori informazioni, vedere hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configurare una macchina virtuale di Azure con Chef. Per altre informazioni, vedere l'argomento [Automazione della distribuzione delle macchine virtuali di Azure con Chef](chef-automation.md)

Inoltre estensioni specifiche di tooprocess, un'estensione Script personalizzato è disponibile per le macchine virtuali Windows e Linux. estensione Script personalizzato per Windows Hello consente qualsiasi toobe di script di PowerShell eseguire in una macchina virtuale. È utile per la progettazione di distribuzioni di Azure che richiedono una configurazione oltre a quella offerta dagli strumenti nativi di Azure. Per altre informazioni, vedere [Estensione Script personalizzato per macchine virtuali Windows](extensions-customscript.md).


## <a name="prerequisites"></a>Prerequisiti

Ogni estensione macchina virtuale può avere un insieme specifico di prerequisiti. Ad esempio, hello estensione della macchina virtuale Docker è un prerequisito di una distribuzione di Linux supportata. Requisiti di singole estensioni vengono descritti in dettaglio nella documentazione di hello specifiche dell'estensione.

### <a name="azure-vm-agent"></a>Agente VM di Azure
agente VM di Azure Hello gestisce l'interazione tra una macchina virtuale di Azure e il controller di infrastruttura di Azure hello. agente VM Hello è responsabile per molti aspetti funzionali di distribuzione e gestione di macchine virtuali di Azure, incluse l'esecuzione di estensioni di macchina virtuale. agente VM di Azure Hello è preinstallato in immagini di Azure Marketplace e può essere installato nei sistemi operativi supportati.

Per informazioni sui sistemi operativi supportati e per le istruzioni di installazione, vedere [Agente delle macchine virtuali di Azure](agent-user-guide.md).

## <a name="discover-vm-extensions"></a>Individuare le estensioni della macchina virtuale
Molte estensioni delle macchine virtuali di diverso tipo sono disponibili per l'uso con macchine virtuali di Azure. toosee un elenco completo, eseguire hello comando con il modulo di gestione risorse di Azure PowerShell hello seguente. Impostare percorsi di hello desiderato di toospecify che quando si esegue questo comando.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>Eseguire le estensioni della macchina virtuale

Estensioni di macchina virtuale di Azure possono essere eseguite nelle macchine virtuali esistenti, che è utile quando è necessario toomake modifiche di configurazione o ripristinare la connessione in una macchina virtuale già distribuita. Le estensioni della macchina virtuale possono essere anche unite in bundle con le distribuzioni del modello di Azure Resource Manager. Utilizzando le estensioni con modelli di gestione risorse, è possibile abilitare toobe macchine virtuali di Azure distribuito e configurato senza la necessità di hello di interventi di post-distribuzione.

Hello dei seguenti metodi può essere utilizzati toorun un'estensione in una macchina virtuale esistente.

### <a name="powershell"></a>PowerShell

Molti comandi di PowerShell vengono utilizzati per l'esecuzione di estensioni singole. toosee un elenco, eseguire i comandi di PowerShell seguente hello.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

Questo fornisce seguenti toohello simili di output:

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

Hello esempio utilizza toodownload di estensione Custom Script hello uno script da un repository di GitHub nella macchina virtuale di destinazione hello e quindi eseguirla script hello. Per ulteriori informazioni sull'estensione dello Script personalizzata hello, vedere [Panoramica di estensione Custom Script](extensions-customscript.md).

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

In questo esempio, hello estensione accesso alle macchine Virtuali è password amministrativa di hello tooreset usate di una macchina virtuale di Windows. Per ulteriori informazioni su hello estensione accesso alle macchine Virtuali, vedere [servizio reimpostare Desktop remoto in una macchina virtuale Windows](reset-rdp.md).

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

Hello `Set-AzureRmVMExtension` comando può essere utilizzato toostart qualsiasi estensione della macchina virtuale. Per ulteriori informazioni, vedere hello [Set AzureRmVMExtension riferimento](https://msdn.microsoft.com/en-us/library/mt603745.aspx).


### <a name="azure-portal"></a>Portale di Azure

Un'estensione della macchina virtuale può essere applicato tooan macchina virtuale esistente tramite hello portale di Azure. toodo in tal caso, selezionare macchina virtuale hello toouse desiderati, scegliere **estensioni**, fare clic su **Aggiungi**. In questo modo si ottiene un elenco di estensioni disponibili. Selezionare hello uno desiderato e quindi seguire i passaggi di hello nella procedura guidata hello.

Hello immagine seguente viene illustrata hello installazione dell'estensione di Microsoft Antimalware dal portale di Azure hello hello.

![Installare un'estensione antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Modelli di Gestione risorse di Azure

Estensioni di macchina virtuale possono essere aggiunto tooan modello di gestione risorse di Azure ed eseguita con la distribuzione di hello del modello di hello. La distribuzione di estensioni con un modello è utile per la creazione di distribuzioni di Azure completamente configurate. Ad esempio, hello che JSON seguente viene eseguita da un modello di gestione risorse che distribuisce un insieme di macchine virtuali di bilanciamento del carico e un database SQL di Azure e quindi installa un'applicazione .NET Core su ogni macchina virtuale. estensione della macchina virtuale Hello occupa hello dell'installazione del software.

Per ulteriori informazioni, vedere hello [complete dei modelli di gestione risorse](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

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

Per altre informazioni, vedere [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions) (Creazione di modelli di Azure Resource Manager con le estensioni della macchina virtuale Windows).

## <a name="secure-vm-extension-data"></a>Proteggere i dati dell'estensione della macchina virtuale

Quando si esegue un'estensione della macchina virtuale, potrebbe essere necessario tooinclude informazioni riservate, ad esempio le credenziali e i nomi degli account di archiviazione chiavi di accesso di account di archiviazione. Molte estensioni VM includono una configurazione protetta, che crittografa i dati e lo decrittografa solo all'interno di hello macchina virtuale di destinazione. Ogni estensione ha uno schema di configurazione protetto specifico che sarà descritto in maniera dettagliata nella documentazione specifica dell'estensione.

Hello di esempio seguente mostra un'istanza di hello estensione Script personalizzato per Windows. Si noti che tooexecute comando hello include un set di credenziali. In questo esempio hello comando tooexecute non verrà crittografati.


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
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Proteggere la stringa di esecuzione hello spostando hello **comando tooexecute** proprietà toohello **protetti** configurazione.

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

## <a name="troubleshoot-vm-extensions"></a>Risoluzione dei problemi relativi alle estensioni della macchina virtuale

Ogni estensione macchina virtuale può disporre di passaggi per la risoluzione dei problemi specifici. Ad esempio, quando si utilizza l'estensione Custom Script hello, dettagli sull'esecuzione di script è reperibile in locale nella macchina virtuale hello in cui è stata eseguita l'estensione hello. Tutti i passaggi per la risoluzione dei problemi specifici dell'estensione sono descritti in dettaglio nella documentazione specifica dell'estensione.

Hello risoluzione dei problemi relativi alla procedura seguente si applica tooall estensioni delle macchine virtuali.

### <a name="view-extension-status"></a>Visualizzare lo stato dell'estensione

Dopo l'esecuzione di un'estensione della macchina virtuale in una macchina virtuale, utilizzare hello lo stato dell'estensione tooreturn comando PowerShell seguente. Sostituire i nomi dei parametri di esempio con i valori desiderati. Hello `Name` parametro accetta il nome di hello assegnato toohello estensione in fase di esecuzione.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

output di Hello è simile hello seguenti:

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

Lo stato dell'esecuzione di estensione può essere rilevata anche in hello portale di Azure. stato hello tooview di un'estensione, hello selezionare macchina virtuale, scegliere **estensioni**, e selezionare hello estensione desiderata.

### <a name="rerun-vm-extensions"></a>Eseguire nuovamente le estensioni della macchina virtuale

Potrebbero essere presenti i casi in cui un'estensione della macchina virtuale deve toobe eseguire di nuovo. È possibile farlo rimuovendo estensione hello e quindi eseguire nuovamente estensione hello con un metodo di esecuzione di propria scelta. tooremove un'estensione, eseguire hello comando con il modulo di Azure PowerShell hello seguente. Sostituire i nomi dei parametri di esempio con i valori desiderati.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Un'estensione può essere rimosso anche tramite hello portale di Azure. toodo in modo:

1. Selezionare una macchina virtuale.
2. Selezionare **Estensioni**.
3. Scegliere l'estensione hello desiderato.
4. Selezionare **Disinstalla**.

## <a name="common-vm-extensions-reference"></a>Riferimento alle estensioni della macchina virtuale comuni
| Nome estensione | Descrizione | Altre informazioni |
| --- | --- | --- |
| Estensione Script personalizzato per Windows |Eseguire script su una macchina virtuale di Azure. |[Estensione script personalizzata per Windows](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Estensione DSC per Windows |Estensione PowerShell DSC (Desired State Configuration) |[Estensione DSC per Windows](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Estensione di Diagnostica di Azure |Gestisce Diagnostica di Azure. |[Estensione di Diagnostica di Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Estensione dell'accesso alla VM di Azure |Gestire gli utenti e le credenziali |[Estensione dell'accesso alle macchine virtuali per Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
