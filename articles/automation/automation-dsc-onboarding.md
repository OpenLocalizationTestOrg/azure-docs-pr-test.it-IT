---
title: aaaOnboarding macchine per la gestione da DSC di automazione di Azure | Documenti Microsoft
description: Come toosetup macchine per la gestione con DSC di automazione di Azure
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Caricamento di computer per la gestione con Automation DSC per Azure

## <a name="why-manage-machines-with-azure-automation-dsc"></a>Perché gestire computer con Automation DSC per Azure

Come [PowerShell DSC (Desired State Configuration)](https://technet.microsoft.com/library/dn249912.aspx), Automation DSC (Desired State Configuration) per Azure è un servizio semplice ma potente per la gestione della configurazione dei nodi DSC (macchine virtuali e computer fisici) in qualsiasi data center nel cloud o locale. Consente la scalabilità tra migliaia di computer in modo rapido e facile da una posizione centrale e sicura. È possibile caricare facilmente le macchine, assegnare loro configurazioni dichiarative e visualizzare i report che mostra ogni computer di stato di conformità toohello desiderato specificato. livello di gestione di automazione di Azure DSC Hello è tooDSC il livello di gestione di automazione di Azure hello tooPowerShell di script. In altre parole, in hello stesso modo in cui l'automazione di Azure consente di gestire gli script di PowerShell, consente inoltre di gestire le configurazioni DSC. toolearn ulteriori informazioni sui vantaggi di hello dell'utilizzo di Automation DSC per Azure, vedere [Cenni preliminari su automazione di Azure DSC](automation-dsc-overview.md).

DSC di automazione di Azure può essere utilizzato toomanage diverse macchine:

* Macchine virtuali di Azure (classica)
* Macchine virtuali di Azure
* Macchine virtuali di Amazon Web Services (AWS)
* Computer fisici/macchine virtuali Windows locali o in un cloud diverso da Azure/AWS
* Computer fisici/macchine virtuali Linux locali, in Azure o in un cloud diverso da Azure

Inoltre, se non si dispone di una configurazione della macchina toomanage pronto dal cloud hello, DSC di automazione di Azure anche utilizzabile come un endpoint solo report. In questo modo è tooset (push) la configurazione desiderata tramite DSC locale e Visualizza dettagli report avanzati sulla conformità di nodo con hello desiderato lo stato in automazione di Azure.

Hello le sezioni seguenti viene descritto come è possibile iniziare ogni tipo di computer tooAzure DSC di automazione.

## <a name="azure-virtual-machines-classic"></a>Macchine virtuali di Azure (classica)

Con Automation DSC per Azure, è possibile caricare facilmente le macchine virtuali Azure (versione classica) per la gestione della configurazione con hello portale di Azure o PowerShell. Quinte hello e senza un amministratore con tooremote in hello VM, hello estensione Azure VM Desired State Configuration registra hello VM con automazione di Azure DSC. Poiché hello estensione configurazione dello stato desiderato di macchina virtuale di Azure viene eseguito in modo asincrono, i passaggi tootrack lo stato di avanzamento o risolvere i problemi sono disponibili in hello [ **onboarding di macchina virtuale di Azure di risoluzione dei problemi** ](#troubleshooting-azure-virtual-machine-onboarding)sezione riportata di seguito.

### <a name="azure-portal"></a>Portale di Azure

In hello [portale di Azure](http://portal.azure.com/), fare clic su **Sfoglia** -> **macchine virtuali (classico)**. Selezionare hello desiderato tooonboard macchina virtuale di Windows. Nel Pannello di dashboard della macchina virtuale hello, fare clic su **tutte le impostazioni** -> **estensioni** -> **Aggiungi**  ->   **Automazione di Azure DSC** -> **creare**. Immettere hello [i valori di Configuration Manager locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessarie per il caso d'uso, la chiave di registrazione dell'account di automazione e registrazione URL e facoltativamente un toohello tooassign di nodo configurazione macchina virtuale.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

URL di registrazione toofind hello e la chiave per la macchina hello automazione account tooonboard hello, vedere hello [ **Secure registrazione** ](#secure-registration) sezione riportata di seguito.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Macchine virtuali di Azure

DSC di automazione di Azure consente di caricare facilmente macchine virtuali di Azure per la gestione della configurazione, utilizzando hello portale di Azure, modelli di gestione risorse di Azure o PowerShell. Quinte hello e senza un amministratore con tooremote in hello VM, hello estensione Azure VM Desired State Configuration registra hello VM con automazione di Azure DSC. Poiché hello estensione configurazione dello stato desiderato di macchina virtuale di Azure viene eseguito in modo asincrono, i passaggi tootrack lo stato di avanzamento o risolvere i problemi sono disponibili in hello [ **onboarding di macchina virtuale di Azure di risoluzione dei problemi** ](#troubleshooting-azure-virtual-machine-onboarding)sezione riportata di seguito.

### <a name="azure-portal"></a>Portale di Azure

In hello [portale di Azure](https://portal.azure.com/), passare toohello account di automazione di Azure in cui si desidera tooonboard le macchine virtuali. Nel dashboard dell'account di automazione hello, fare clic su **i nodi DSC** -> **macchina virtuale di Azure aggiungere**.

In **selezionare le macchine virtuali tooonboard**, selezionare uno o tooonboard di macchine virtuali di Azure più.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

In **configurare i dati di registrazione**, immettere hello [i valori di Configuration Manager locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessari per il caso d'uso e, facoltativamente, un toohello tooassign di nodo configurazione macchina virtuale.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Modelli di Gestione risorse di Azure

Macchine virtuali di Azure può essere distribuite e caricate tooAzure DSC di automazione tramite modelli di gestione risorse di Azure. Vedere [configurare una macchina virtuale tramite l'estensione DSC e automazione di Azure DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) per un modello di esempio che onboards un tooAzure VM DSC di automazione esistente. toofind hello chiave e registrazione URL di registrazione eseguito come input in questo modello, vedere hello [ **Secure registrazione** ](#secure-registration) sezione riportata di seguito.

### <a name="powershell"></a>PowerShell

Hello [registro AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet può essere utilizzato tooonboard di macchine virtuali nel portale di Azure tramite PowerShell hello.

## <a name="amazon-web-services-aws-virtual-machines"></a>Macchine virtuali di Amazon Web Services (AWS)

È possibile caricare facilmente le macchine virtuali Amazon Web Services per la gestione della configurazione da Automation DSC per Azure utilizzando hello AWS DSC Toolkit. Altre informazioni sul toolkit di hello [qui](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>Computer fisici/macchine virtuali Windows locali o in un cloud diverso da Azure/AWS

Il computer di Windows locale e i computer di Windows in aree diverse da Azure (ad esempio, Amazon Web Services) possono rivelarsi caricate tooAzure DSC di automazione, purché dispongano dell'accesso in uscita toohello internet, con pochi semplici passaggi:

1. Verificare che hello di versione più recente del [WMF 5](http://aka.ms/wmf5latest) viene installato nei computer hello desiderato tooonboard tooAzure DSC di automazione.
2. Seguire le direzioni di hello nella sezione [ **generazione DSC metaconfigurazioni** ](#generating-dsc-metaconfigurations) seguito toogenerate una cartella contenente hello necessari metaconfigurazioni DSC.
3. Si applica in modalità remota hello DSC PowerShell metaconfigurazione toohello le macchine da tooonboard. **Questo comando viene eseguito dalla macchina di Hello deve avere più recente di hello [WMF 5](http://aka.ms/wmf5latest) installato**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Se non è possibile applicare metaconfigurazioni di PowerShell DSC hello in modalità remota, è possibile copiare cartella metaconfigurazioni hello dal passaggio 2 in tooonboard ogni computer. Chiamare quindi **Set-DscLocalConfigurationManager** in ogni tooonboard macchina locale.
5. Utilizzo di hello portale di Azure o i cmdlet, verificare che hello macchine tooonboard ora visualizzati come nodi DSC registrato nell'account di automazione di Azure.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>Computer fisici/macchine virtuali Linux locali, in Azure o in un cloud diverso da Azure

Computer Linux locale, i computer Linux in Azure, oltre a macchine Linux in cloud di Azure non caricate tooAzure DSC di automazione, purché dispongano dell'accesso in uscita toohello internet, con pochi semplici passaggi:

1. Verificare che hello di versione più recente del [PowerShell DSC per Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) viene installato nei computer hello desiderato tooonboard tooAzure DSC di automazione.
2. Se hello [valori predefiniti di Configuration Manager locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) corrisponde il caso d'uso e si desidera tooonboard computer ad che essi **entrambi** pull da e report tooAzure DSC di automazione:

   + TooAzure DSC di automazione del tooonboard di computer ogni Linux, utilizzare tooonboard Register.py hello impostazioni predefinite di Gestione configurazione locale DSC di PowerShell utilizzando:

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind hello chiave e registrazione URL di registrazione per l'account di automazione, vedere hello [ **Secure registrazione** ](#secure-registration) sezione riportata di seguito.

     Se hello Configuration Manager locale DSC PowerShell predefinito **si** **non** corrisponde il caso d'uso o se si desidera tooonboard macchine in modo che solo report tooAzure DSC di automazione, ma non effettuare il pull configurazione o i moduli di PowerShell, seguire i passaggi da 3 a 6. In caso contrario, procedere direttamente toostep 6.

3. Seguire le direzioni di hello in hello [ **generazione DSC metaconfigurazioni** ](#generating-dsc-metaconfigurations) sezione toogenerate una cartella contenente metaconfigurazioni DSC hello necessita.
4. Applica in modalità remota hello DSC PowerShell metaconfigurazione toohello le macchine da tooonboard:

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

Questo comando viene eseguito dalla macchina di Hello deve avere più recente di hello [WMF 5](http://aka.ms/wmf5latest) installato.

1. Se non è possibile applicare metaconfigurazioni di PowerShell DSC hello in modalità remota, per ogni tooonboard computer Linux, è possibile copiare la macchina hello metaconfigurazione corrispondente toothat dalla cartella hello nel passaggio 5 in computer Linux hello. Chiamare quindi `SetDscLocalConfigurationManager.py` in locale in ogni computer Linux desiderato tooonboard tooAzure DSC di automazione:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. Utilizzo di hello portale di Azure o i cmdlet, verificare che hello macchine tooonboard ora visualizzati come nodi DSC registrato nell'account di automazione di Azure.

## <a name="generating-dsc-metaconfigurations"></a>Generazione di metaconfigurazioni DSC

toogenerically caricare qualsiasi computer tooAzure DSC di automazione, un [metaconfigurazione DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) può essere generato che, quando applicata, indica ad Agente hello DSC in hello macchina toopull da e/o report tooAzure DSC di automazione. Metaconfigurazioni di DSC per Azure Automation DSC possono essere generato utilizzando una configurazione DSC PowerShell o i cmdlet di PowerShell di automazione di Azure hello.

> [!NOTE]
> Metaconfigurazioni di DSC contengono hello segreti necessiti tooonboard un account di automazione per la gestione di tooan macchina. Verificare che tooproperly proteggere qualsiasi metaconfigurazioni DSC che crei o eliminarli dopo l'uso.

### <a name="using-a-dsc-configuration"></a>Uso di una configurazione DSC

1. Aprire PowerShell ISE come amministratore hello in un computer nell'ambiente locale. macchina Hello deve avere una versione più recente di hello di [WMF 5](http://aka.ms/wmf5latest) installato.
2. Hello Copia localmente lo script seguente. Questo script contiene una configurazione DSC PowerShell per la creazione di metaconfigurazioni e tookick un comando esterno creazione metaconfigurazione hello.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Compilare il codice di registrazione hello e l'URL per l'account di automazione, nonché i nomi di hello di hello macchine tooonboard. Tutti gli altri parametri sono facoltativi. toofind hello chiave e registrazione URL di registrazione per l'account di automazione, vedere hello [ **Secure registrazione** ](#secure-registration) sezione riportata di seguito.
4. Se si desidera hello macchine tooreport DSC stato informazioni tooAzure DSC di automazione, ma non effettuare il pull configurazione o i moduli di PowerShell, impostare hello **ReportOnly** tootrue di parametro.
5. Eseguire script hello. È ora una cartella denominata **DscMetaConfigs** nella directory di lavoro, contenente hello metaconfigurazioni di PowerShell DSC per hello macchine tooonboard (come amministratore):

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>Utilizzo dei cmdlet di automazione di Azure hello

Se le impostazioni predefinite di Configuration Manager locale DSC PowerShell hello corrispondano il caso d'uso, e si desidera tooonboard macchine quale effettuare il pull da e tooAzure DSC di automazione del report, i cmdlet di automazione di Azure hello offrono un metodo semplificato di generazione hello DSC metaconfigurazioni necessita:

1. Aprire la console di PowerShell hello o PowerShell ISE come amministratore in un computer nell'ambiente locale.
2. Connettersi usando Gestione risorse tooAzure **Aggiungi AzureRmAccount**
3. Scaricare metaconfigurazioni di PowerShell DSC hello per le macchine hello da tooonboard da hello automazione account toowhich desiderato tooonboard nodi:

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. È ora una cartella denominata ***DscMetaConfigs***, contenente hello metaconfigurazioni di PowerShell DSC per hello macchine tooonboard (come amministratore):
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Registrazione sicura

Macchine è possibile caricare in modo sicuro tooan account di automazione di Azure tramite protocollo di registrazione WMF 5 DSC hello, che consente un DSC nodo tooauthenticate tooa PowerShell DSC V2 Pull o Reporting server (inclusi DSC di automazione di Azure). nodo Hello Registra server toohello un **registrazione URL**, che esegue l'autenticazione utilizzando un **chiave di registrazione**. Durante la registrazione, nodo hello DSC e i server di Pull DSC/report negoziare un certificato univoco per questo toouse nodo per la post-registrazione di autenticazione toohello server. Questo processo impedisce ai nodi caricati di rappresentarsi reciprocamente, ad esempio nel caso di un nodo compromesso e che presenta un comportamento dannoso. Dopo la registrazione, la chiave di registrazione hello non viene utilizzata per l'autenticazione nuovamente e viene eliminata dal nodo hello.

È possibile ottenere informazioni hello necessarie per il protocollo di registrazione hello DSC da hello **Gestisci chiavi** pannello nel portale di anteprima di Azure hello. Aprire il pannello facendo clic sull'icona chiave hello in hello **Essentials** pannello per hello account di automazione.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* URL di registrazione è il campo URL hello nel Pannello di gestione delle chiavi hello.
* Chiave di registrazione è hello chiave di accesso primaria o la chiave di accesso secondaria nel Pannello di gestione delle chiavi hello. È possibile usare una delle due chiavi.

Per maggiore sicurezza, è possono rigenerare le chiavi di accesso primarie e secondarie hello di un account di automazione in qualsiasi momento (in hello **Gestisci chiavi** blade) tooprevent nodo future registrazioni chiavi precedente.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Risoluzione dei problemi di caricamento di macchine virtuali di Azure

Automation DSC di Azure consente di caricare macchine virtuali Windows di Azure per la gestione della configurazione. Quinte hello, hello estensione Azure VM Desired State Configuration è usato tooregister hello VM con automazione di Azure DSC. Poiché hello estensione Azure VM DSC viene eseguito in modo asincrono, lo stato di avanzamento di rilevamento e risoluzione dei problemi relativa esecuzione potrebbe essere importante.

> [!NOTE]
> Qualsiasi metodo di caricamento di un tooAzure macchina virtuale Windows Azure DSC di automazione che utilizza l'estensione di configurazione dello stato desiderato di Azure VM hello potrebbe richiedere ora tooan per hello nodo tooshow backup registrato in automazione di Azure. Ciò è dovuto toohello installazione di Windows Management Framework 5.0 in hello VM con l'estensione di macchina virtuale di Azure DSC hello, che è necessario tooonboard hello VM tooAzure DSC di automazione.

tootroubleshoot o una vista stato hello dell'estensione di configurazione dello stato desiderato di macchina virtuale di Azure, nel portale di Azure hello hello passare toohello macchina virtuale viene caricato, quindi fare clic su -> **tutte le impostazioni** -> **estensioni**   ->  **DSC**. Per altri dettagli, è possibile fare clic su **Visualizza stato dettagliato**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Scadenza del certificato e nuova registrazione

Dopo la registrazione di un computer come un nodo DSC in Automation DSC per Azure, esistono una serie di motivi per cui potrebbe essere necessario tooreregister tale nodo nel hello futura:

* Dopo la registrazione, ogni nodo negozia automaticamente un certificato univoco per l'autenticazione che scade dopo un anno. Attualmente, hello protocollo di registrazione di PowerShell DSC automaticamente non è possibile rinnovare i certificati quando essi sono prossime alla scadenza, pertanto è necessario nodi hello tooreregister dopo un anno. Prima di registrare di nuovo, verificare che ogni nodo esegua Windows Management Framework 5.0 RTM. Scadenza del certificato di autenticazione di un nodo, se il nodo hello non è registrato, nodo hello sarà Impossibile toocommunicate con automazione di Azure e verrà contrassegnato come 'Inattiva'. La registrazione eseguita 90 giorni o minore dall'ora di scadenza certificato hello o in qualsiasi momento dopo l'ora di scadenza del certificato hello, verrà generato un nuovo certificato viene generato e utilizzato.
* toochange qualsiasi [i valori di Configuration Manager locale DSC PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) che sono state impostate durante la registrazione iniziale del nodo di hello, ad esempio ConfigurationMode. Attualmente, i valori dell'agente DSC possono essere modificati solo tramite la registrazione. un'eccezione di Hello è hello configurazione nodo assegnata nodo toohello - può essere modificato direttamente in automazione di Azure DSC.

La registrazione può essere eseguita in hello allo stesso modo è stato registrato il nodo hello inizialmente, utilizzando uno dei metodi di caricamento hello descritte in questo documento. Prima di registrare di nuovo, non è necessario toounregister un nodo da Automation DSC per Azure.

## <a name="related-articles"></a>Articoli correlati

* [Panoramica di Automation DSC per Azure](automation-dsc-overview.md)
* [Cmdlet di Automation DSC per Azure](/powershell/module/azurerm.automation/#automation)
* [Prezzi di Automation DSC per Azure](https://azure.microsoft.com/pricing/details/automation/)
