---
title: configurazioni aaaCompiling in Automation DSC per Azure | Documenti Microsoft
description: Questo articolo viene descritto come le configurazioni di configurazione DSC (Desired State) toocompile per l'automazione di Azure.
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Compilazione di configurazioni in Azure Automation DSC

È possibile compilare le configurazioni di configurazione DSC (Desired State) in due modi con automazione di Azure: nel portale di Azure hello e con Windows PowerShell. Hello nella tabella seguente consentono di determinare quando il metodo in base alle caratteristiche di hello di ogni toouse:

### <a name="azure-portal"></a>Portale di Azure

* Metodo più semplice con interfaccia utente interattiva
* Valori dei parametri semplice tooprovide modulo
* Facilità di controllo dello stato dei processi
* Accesso autenticato con l'accesso di Azure

### <a name="windows-powershell"></a>Windows PowerShell

* Chiamata mediante cmdlet di Windows PowerShell nella riga di comando
* Possibilità di inclusione in una soluzione automatizzata con più passaggi
* Possibilità di specificare valori di parametri semplici e complessi
* Possibilità di controllare lo stato dei processi
* Toosupport client necessari i cmdlet di PowerShell
* Passaggio di ConfigurationData
* Compilazione di configurazioni che usano credenziali

Dopo aver scelto un metodo di compilazione, è possibile seguire procedure rispettivi di hello sotto toostart la compilazione.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>La compilazione di una configurazione DSC con hello portale di Azure

1. Nell'account di Automazione fare clic su **Configurazioni DSC**.
2. Fare clic su una configurazione tooopen il pannello.
3. Fare clic su **Compila**.
4. Se la configurazione hello non ha alcun parametro, si tooconfirm richiesta se si desidera toocompile è. Se la configurazione hello include parametri, hello **configurazione compilazione** pannello verrà aperta, pertanto è possibile fornire i valori dei parametri. Vedere hello [ **parametri di base** ](#basic-parameters) sezione riportata di seguito per ulteriori informazioni sui parametri.
5. Hello **processo di compilazione** pannello viene aperto in modo che è possibile tenere traccia dello stato del processo di compilazione hello e hello configurazioni del nodo (documenti di configurazione MOF) ha causato toobe sul Server di Pull DSC di Azure Automation hello.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>Compilazione di una configurazione DSC con Windows PowerShell

È possibile utilizzare [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart la compilazione con Windows PowerShell. Hello codice di esempio seguente viene avviata la compilazione di una configurazione DSC denominata **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`oggetto che è possibile utilizzare tootrack lo stato del processo restituisce una compilazione. È quindi possibile utilizzare questo oggetto processo di compilazione con [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) stato hello toodetermine del processo di compilazione, hello e [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview dei flussi (output). Hello codice di esempio seguente viene avviata la compilazione di hello **SampleConfig** configurazione, è in attesa fino a quando non è stata completata e quindi Visualizza dei flussi.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>Parametri di base
Dichiarazione di parametro nelle configurazioni DSC, inclusi i tipi di parametro e le proprietà, works hello stesso come runbook di automazione di Azure. Vedere [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md) toolearn ulteriori informazioni sui parametri di runbook.

esempio Hello utilizza due parametri denominati **FeatureName** e **IsPresent**, i valori hello toodetermine delle proprietà in hello **ParametersExample.sample** nodo configurazione, generata durante la compilazione.

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

È possibile compilare le configurazioni DSC che utilizzano parametri di base nel portale di Azure Automation DSC hello o con Azure PowerShell:

### <a name="portal"></a>di Microsoft Azure

Nel portale di hello, è possibile immettere i valori dei parametri dopo aver fatto clic **compilare**.

![testo alternativo](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell richiede i parametri in un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) dove hello chiave corrisponde a nome del parametro hello e valore hello è uguale a valore del parametro hello.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

Per informazioni sul passaggio di PSCredentials come parametri, vedere <a href="#credential-assets">**Asset credenziali**</a> più avanti.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** consente la configurazione strutturale di tooseparate da qualsiasi configurazione dell'ambiente specifico durante l'utilizzo di PowerShell DSC. Vedere [separazione "Novità" da "Dove" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn ulteriori informazioni sulla **ConfigurationData**.

> [!NOTE]
> È possibile utilizzare **ConfigurationData** durante la compilazione in Automation DSC per Azure con Azure PowerShell, ma non nel portale di Azure hello.

Hello configurazione DSC di esempio seguente viene utilizzato **ConfigurationData** tramite hello **$ConfigurationData** e **$AllNodes** parole chiave. È anche necessario hello [ **xWebAdministration** modulo](https://www.powershellgallery.com/packages/xWebAdministration/) per questo esempio:

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

È possibile compilare una configurazione di DSC hello sopra con PowerShell. Hello sotto PowerShell aggiunge due nodo configurazioni toohello Server di Pull DSC di Azure Automation: **ConfigurationDataSample.MyVM1** e **ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>Asset

I riferimenti di asset vengono hello stesso nei runbook e le configurazioni DSC di automazione di Azure. Vedere hello seguenti per ulteriori informazioni:

* [Certificati](automation-certificates.md)
* [Connessioni](automation-connections.md)
* [Credenziali](automation-credentials.md)
* [Variabili](automation-variables.md)

### <a name="credential-assets"></a>Asset credenziali

Anche se le configurazioni DSC in Automazione di Azure possono fare riferimento ad asset di credenziali con **Get-AzureRmAutomationCredential**, gli asset di credenziali possono essere passati anche con i parametri, se necessario. Se una configurazione accetta un parametro di **PSCredential** digitare, quindi è necessario nome di stringa hello toopass di un asset delle credenziali di automazione di Azure come valore del parametro che, anziché un oggetto PSCredential. Background hello, asset delle credenziali di automazione di Azure hello con tale nome verrà recuperato e passato toohello configurazione.

Mantenendo le credenziali protette in configurazioni del nodo (documenti di configurazione MOF) richiede la crittografia delle credenziali hello nel file MOF di configurazione nodo hello. Automazione di Azure accetta ulteriormente questo passaggio e crittografa tutto il file MOF hello. Tuttavia, attualmente è necessario indicare PowerShell DSC è accettabile per le credenziali toobe output in formato testo normale durante la generazione del file MOF di configurazione nodo, perché DSC PowerShell non riconosce che è possibile che automazione di Azure verrà crittografia intero file MOF hello dopo il generazione tramite un processo di compilazione.

È possibile indicare che è per le credenziali toobe restituiti in testo normale nella configurazione del nodo hello generato i file MOF DSC PowerShell utilizzando [ **ConfigurationData**](#configurationdata). È necessario passare `PSDscAllowPlainTextPassword = $true` tramite **ConfigurationData** per nome di ogni nodo del blocco che viene visualizzato nella configurazione DSC hello e utilizza le credenziali.

Hello seguente viene illustrata una configurazione DSC che utilizza un asset delle credenziali di automazione.

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

È possibile compilare una configurazione di DSC hello sopra con PowerShell. Hello sotto PowerShell aggiunge due nodo configurazioni toohello Server di Pull DSC di Azure Automation: **CredentialSample.MyVM1** e **CredentialSample.MyVM2**.

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>Importazione delle configurazioni di nodo

È anche possibile importare configurazioni di nodo (MOF) compilate all'esterno di Azure. Uno dei vantaggi di questa operazione consiste nel fatto che le configurazioni di nodo possono essere firmate.
Una configurazione di un nodo con segno viene verificata in locale in un nodo gestito da agente hello DSC, garantendo che la configurazione di hello viene applicato toohello nodo proviene da un'origine autorizzata.

> [!NOTE]
> È possibile importare configurazioni firmate nell'account di Automazione di Azure, che tuttavia attualmente non supporta la compilazione di configurazioni firmate.

> [!NOTE]
> Un file di configurazione del nodo deve essere non maggiore di 1 MB tooallow è toobe importati in automazione di Azure.

È possibile ottenere informazioni come configurazioni del nodo toosign in https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Importare una configurazione del nodo in hello portale di Azure

1. Nell'account di Automazione fare clic su **Configurazioni del nodo DSC**.

    ![Configurazioni del nodo DSC](./media/automation-dsc-compile/node-config.png)
2. In hello **configurazioni del nodo DSC** pannello, fare clic su **aggiungere un NodeConfiguration**.
3. In hello **importazione** pannello, fare clic su hello cartella icona Avanti toohello **File di configurazione nodo** toobrowse casella di testo per un file di configurazione del nodo (MOF) nel computer locale.

    ![Cercare il file locale](./media/automation-dsc-compile/import-browse.png)
4. Immettere un nome in hello **nome configurazione** casella di testo. Questo nome deve corrispondere il nome di hello della configurazione di hello da cui è stata compilata la configurazione di un nodo hello.
5. Fare clic su **OK**.

### <a name="importing-a-node-configuration-with-powershell"></a>Importazione di una configurazione del nodo con PowerShell

È possibile utilizzare hello [importazione AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) tooimport cmdlet una configurazione del nodo nell'account di automazione.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



