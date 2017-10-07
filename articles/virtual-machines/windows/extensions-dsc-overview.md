---
title: Configurazione dello stato per una panoramica di Azure aaaDesired | Documenti Microsoft
description: "Panoramica per l'utilizzo di gestore di estensioni di Microsoft Azure hello per PowerShell Desired State Configuration. Inclusi prerequisiti, architettura, cmdlet e così via."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Gestore di estensioni di Azure DSC toohello introduzione
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello agente VM di Azure e le estensioni associate fanno parte di hello servizi infrastruttura di Microsoft Azure. Le estensioni VM sono componenti software che estendono le funzionalità di macchina virtuale hello e semplificano le operazioni di gestione diverse VM. Ad esempio, hello estensione VMAccess può essere utilizzato tooreset una password dell'amministratore o hello Custom Script estensione può essere utilizzato tooexecute uno script nella macchina virtuale hello.

Questo articolo descrive hello estensione PowerShell DSC Desired State Configuration () per le macchine virtuali di Azure come parte di hello Azure PowerShell SDK. È possibile utilizzare i nuovi cmdlet tooupload e applicare una configurazione DSC PowerShell in una macchina virtuale di Azure abilitata con l'estensione DSC PowerShell hello. chiamate di estensione DSC PowerShell Hello in hello tooenact PowerShell DSC ha ricevuto la configurazione DSC in hello VM. Questa funzionalità è anche disponibile tramite hello portale di Azure.

## <a name="prerequisites"></a>Prerequisiti
**Computer locale** toointeract con hello estensione della macchina virtuale di Azure, è necessario toouse entrambi hello portale di Azure o hello Azure PowerShell SDK. 

**Agente guest** hello macchina virtuale di Azure è configurata per la configurazione DSC hello deve toobe un sistema operativo che supporta Windows Management Framework (WMF) 4.0 o 5.0. elenco completo di Hello versioni supportate del sistema operativo è reperibile in hello [cronologia delle versioni estensione DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Termini e concetti
Questa guida si presuppone una certa familiarità con hello seguenti concetti:

Configurazione: documento di configurazione DSC. 

Nodo: destinazione per una configurazione DSC. In questo documento, "il termine nodo" fa sempre riferimento tooan macchina virtuale di Azure.

Dati di configurazione: file con estensione psd1 contenente i dati ambientali per una configurazione.

## <a name="architectural-overview"></a>Panoramica dell'architettura
Hello estensione DSC di Azure Usa hello agente VM di Azure framework toodeliver, applicare e segnalare le configurazioni DSC in esecuzione in macchine virtuali di Azure. estensione DSC Hello prevede un file con estensione zip che contiene almeno un documento di configurazione e un set di parametri forniti tramite Azure PowerShell SDK hello o hello portale di Azure.

Estensione hello viene chiamato per hello prima volta, viene eseguito un processo di installazione. Questo processo installa una versione di hello Windows Management Framework (WMF) utilizzando hello seguente logica:

1. Se Windows Server 2016 hello del sistema operativo VM di Azure, viene eseguita alcuna azione. Windows Server 2016 già versione più recente di hello di PowerShell installata.
2. Se hello `wmfVersion` proprietà viene specificata la versione di hello WMF è installati, a meno che non è compatibile con sistema operativo della macchina virtuale di hello.
3. Se non `wmfVersion` proprietà viene specificata, viene installato hello più recente versione applicabile di hello WMF.

L'installazione di WMF hello richiede un riavvio. Dopo il riavvio, estensione hello Scarica i file con estensione zip hello specificato in hello `modulesUrl` proprietà. Se questo percorso nell'archiviazione blob di Azure, è possibile specificare un token di firma di accesso condiviso in hello `sasToken` tooaccess proprietà hello file. Dopo aver ZIP hello viene scaricato e decompresso, hello definito nella funzione di configurazione `configurationFunction` esecuzione file MOF di hello toogenerate. estensione Hello esegue quindi `Start-DscConfiguration -Force` nel file MOF di hello generato. estensione Hello acquisisce l'output e lo scrive nuovamente toohello canale lo stato di Azure. Da questo momento, hello Gestione configurazione locale DSC gestisce il monitoraggio e correzione come di consueto. 

## <a name="powershell-cmdlets"></a>Cmdlet PowerShell
I cmdlet di PowerShell possono essere utilizzati con Gestione risorse di Azure o hello toopackage modello di distribuzione classica, pubblicano e monitorare le distribuzioni di estensione DSC. i cmdlet seguenti elencati Hello sono moduli di distribuzione classica hello, ma "Azure" può essere sostituito con modello di gestione risorse di Azure hello toouse "Azure Resource Manager". Ad esempio, `Publish-AzureVMDscConfiguration` utilizza hello modello di distribuzione classico, in cui `Publish-AzureRmVMDscConfiguration` Usa Gestione risorse di Azure. 

`Publish-AzureVMDscConfiguration`accetta un file di configurazione, esegue l'analisi per le risorse DSC dipendenti e crea un file zip contenente hello e configurazione di hello tooenact necessarie risorse DSC. Inoltre, è possibile creare pacchetti hello in locale utilizzando hello `-ConfigurationArchivePath` parametro. In caso contrario, pubblica l'archiviazione di blob tooAzure file con estensione zip hello e protegge con un token di firma di accesso condiviso.

file con estensione zip Hello creati da questo cmdlet ha script di configurazione con estensione ps1 hello nella radice di hello della cartella di archiviazione hello. Risorse hanno inserito nella cartella di archiviazione hello cartella del modulo di hello. 

`Set-AzureVMDscExtension`Inserisce le impostazioni di hello necessarie hello estensione DSC PowerShell in un oggetto configurazione macchina virtuale. Nel modello di distribuzione classica hello, modifiche alla macchina virtuale hello deve essere applicato tooan macchina virtuale di Azure con `Update-AzureVM`. 

`Get-AzureVMDscExtension`Recupera lo stato dell'estensione DSC hello di una determinata macchina virtuale. 

`Get-AzureVMDscExtensionStatus`Recupera informazioni sullo stato hello di configurazione di DSC hello applicata dal gestore dell'estensione DSC hello. Questa azione può essere eseguita su una singola VM o su un gruppo di VM.

`Remove-AzureVMDscExtension`Rimuove il gestore di estensioni di hello da una macchina virtuale specificata. Questo cmdlet non **non** rimuovere la configurazione di hello, disinstallare WMF hello o modificare le impostazioni applicata hello nella macchina virtuale hello. Rimuove solo il gestore dell'estensione hello. 

**Differenze principali tra cmdlet ASM e cmdlet di Azure Resource Manager**

* I cmdlet di Azure Resource Manager sono sincroni, mentre i cmdlet di Gestione dei servizi di Azure sono asincroni.
* ResourceGroupName, VMName, ArchiveStorageAccountName, Version e Location sono tutti parametri obbligatori in Azure Resource Manager.
* ArchiveResourceGroupName è un nuovo parametro facoltativo per Azure Resource Manager. È possibile specificare questo parametro quando l'account di archiviazione appartiene tooa gruppo di risorse diverso rispetto a hello uno in cui viene creato macchina virtuale hello.
* ConfigurationArchive è denominato ArchiveBlobName in Azure Resource Manager
* ContainerName è denominato ArchiveContainerName in Azure Resource Manager
* StorageEndpointSuffix è denominato ArchiveStorageEndpointSuffix in Azure Resource Manager
* opzione di aggiornamento automatico di Hello è stato aggiunto tooAzure tooenable Gestione risorse di hello estensione gestore toohello versione più recente come e quando è disponibile l'aggiornamento automatico. Si noti che questo parametro ha toocause potenziali hello viene riavviato nel hello VM quando una nuova versione di hello che WMF viene rilasciato. 

## <a name="azure-portal-functionality"></a>Funzionalità del portale di Azure
Sfoglia tooa macchina virtuale. In Impostazioni -> Generale fare clic su "Estensioni". Verrà creato un nuovo riquadro. Fare clic su Add e selezionare PowerShell DSC.

portale di Hello richiede input.
**Configuration Modules or Script**(Moduli o script di configurazione): questo è un campo obbligatorio. È necessario un file con estensione ps1 che contiene uno script di configurazione o un file ZIP con uno script di configurazione con estensione ps1 nella directory principale di hello e tutte le risorse dipendenti nelle cartelle di modulo all'interno di hello ZIP. Può essere creato con hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet inclusi in hello Azure PowerShell SDK. file con estensione zip Hello verrà caricate nell'archiviazione blob utente protetto da un token di firma di accesso condiviso. 

**Configuration Data PSD1 File**(File PSD1 dati di configurazione): questo è un campo facoltativo. Se la configurazione richiede un file di dati di configurazione in psd1, utilizzare tooselect questo campo è e caricarlo archiviazione blob di tooyour utente, in cui si è protetto da un token di firma di accesso condiviso. 

**Module-Qualified Name of Configuration**: i file con estensione .ps1 possono avere più funzioni di configurazione. Immettere il nome di hello dello script con estensione PS1 di configurazione hello seguito da un '\' e il nome della funzione di configurazione hello hello. Ad esempio, se lo script con estensione ps1 ha nome hello "configuration.ps1" e la configurazione di hello è "IisInstall", immettere:`configuration.ps1\IisInstall`

**Gli argomenti di configurazione**: se la funzione di configurazione hello accetta argomenti, immetterli in questa pagina in formato hello `argumentName1=value1,argumentName2=value2`. Questo formato è diverso rispetto a quello in cui vengono accettati gli argomenti di configurazione tramite i cmdlet di PowerShell o i modelli di Resource Manager. 

## <a name="getting-started"></a>introduttiva
Hello estensione DSC di Azure accetta i documenti di configurazione DSC e li successivamente vengono eseguiti in macchine virtuali di Azure. Di seguito è riportato un semplice esempio di configurazione. Salvarlo in locale come "IisInstall.ps1":

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

Hello seguendo i passaggi sul posto hello IisInstall.ps1 script hello specificato macchina virtuale, eseguire la configurazione hello e segnalare lo stato.
###<a name="classic-model"></a>Modello classico
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Modello di Azure Resource Manager

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>Registrazione
I log vengono inseriti in:

C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Numero versione]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su PowerShell DSC, [visitare Centro documentazione di PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

Esaminare hello [il modello di gestione risorse di Azure per l'estensione DSC hello](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

funzionalità aggiuntive di toofind è possibile gestire con PowerShell DSC, [Sfoglia raccolta PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) per più risorse DSC.

Per ulteriori informazioni sul passaggio di parametri sensibili in configurazioni, vedere [gestire le credenziali in modo sicuro con gestore dell'estensione DSC hello](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

