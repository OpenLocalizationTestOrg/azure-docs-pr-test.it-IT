---
title: una macchina virtuale di Windows con PowerShell aaaCreate | Documenti Microsoft
description: Creare macchine virtuali di Windows Azure PowerShell e il modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>Creare una macchina virtuale Windows con PowerShell e hello modello di distribuzione classica
> [!div class="op_single_selector"]
> * [Portale di Azure - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Questi passaggi mostrano come toocustomize una serie di Azure PowerShell comandi che creare e preconfigurare una macchina virtuale Azure basato su Windows utilizzando un approccio di blocco predefinito. È possibile utilizzare questo processo tooquickly creare un set di comandi per una nuova macchina virtuale basato su Windows ed espandere una distribuzione esistente o toocreate più comando che imposta rapidamente creare un ambiente di pro IT o di sviluppo/test personalizzati.

Questi passaggi seguono un approccio basato sul completamento di valori predefiniti per la creazione di set di comandi di Azure PowerShell. Questo approccio può essere utile se si è tooPowerShell nuovo o si desidera tooknow toospecify i valori per la corretta configurazione. Gli utenti esperti di PowerShell possono accettare i comandi di hello e sostituire i propri valori per le variabili di hello (righe hello che iniziano con "$").

Se non è già fatto, utilizzare le istruzioni hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell nel computer locale. Quindi, aprire un prompt dei comandi di Windows PowerShell.

## <a name="step-1-add-your-account"></a>Passaggio 1: Aggiungere l'account
1. Al prompt di PowerShell hello digitare **Add-AzureAccount** e fare clic su **invio**. 
2. Digitare l'indirizzo di posta elettronica hello associati alla sottoscrizione Azure e fare clic su **continua**. 
3. Digitare la password dell'account hello. 
4. Fare clic su **Accedi**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Passaggio 2: Impostare l'account di archiviazione e la sottoscrizione
Impostare la sottoscrizione di Azure e l'account di archiviazione, eseguire questi comandi al prompt dei comandi di Windows PowerShell hello. Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri, con nomi corretti hello.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

È possibile ottenere il nome di sottoscrizione corretta hello dalla proprietà SubscriptionName hello output di hello hello **Get-AzureSubscription** comando. È possibile ottenere un nome account di archiviazione corretto hello da hello proprietà Label dell'output di hello di hello **Get AzureStorageAccount** comando dopo aver eseguito hello **Select-AzureSubscription** comando.

## <a name="step-3-determine-hello-imagefamily"></a>Passaggio 3: Determinare hello family
Successivamente, è necessario toodetermine hello family o valore dell'etichetta per hello immagine specifica corrispondente toohello desiderato toocreate macchina virtuale di Azure. È possibile ottenere l'elenco di hello dei valori di proprietà ImageFamily disponibili con questo comando.

    Get-AzureVMImage | select ImageFamily -Unique

Di seguito sono riportati alcuni esempi di valori ImageFamily per i computer basati su Windows:

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1,
* Windows Server 2016 Technical Preview 4
* SQL Server 2012 SP1 Enterprise in Windows Server 2012

Se si trova l'immagine di hello che si sta cercando, aprire una nuova istanza dell'editor di testo hello di scelta o hello PowerShell Integrated Scripting Environment (ISE). Copiare l'esempio hello in nuovo file di testo hello o hello PowerShell ISE, sostituendo il valore di proprietà ImageFamily hello.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

In alcuni casi, il nome di immagine hello è hello proprietà etichetta anziché hello family valore. Se non è possibile trovare l'immagine di hello che si sta cercando di utilizzare la proprietà ImageFamily hello, elenco immagini hello tramite la proprietà etichetta con questo comando.

    Get-AzureVMImage | select Label -Unique

Se si trova l'immagine a destra hello con questo comando, aprire una nuova istanza dell'editor di testo hello di scelta o hello PowerShell ISE. Copiare l'esempio hello in nuovo file di testo hello o hello PowerShell ISE, sostituendo il valore di etichetta hello.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>Passaggio 4: compilare il set di comandi
Compilare il resto di hello del comando di impostare copiando set appropriato di hello di blocchi di sotto del nuovo file di testo o hello ISE inserimento dei valori di variabile hello e rimuovendo hello < e > caratteri. Vedere hello due [esempi](#examples) alla fine di hello di questo articolo per avere un'idea del risultato finale hello.

Avviare il set di comandi scegliendo uno dei due seguenti blocchi di comandi (obbligatorio).

Opzione 1: specificare un nome di macchina virtuale e una dimensione.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Opzione 2: specificare un nome, la dimensione e il nome del set di disponibilità.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

Per i valori di InstanceSize hello per D, di dominio Active Directory o macchine virtuali serie G, vedere [macchina virtuale e alle dimensioni dei servizi Cloud per Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

> [!NOTE]
> Se si dispone di un contratto Enterprise Agreement con Software Assurance e prevede tootake sfruttare hello Windows Server [vantaggio di utilizzare ibrida](https://azure.microsoft.com/pricing/hybrid-use-benefit/), aggiungere il **- LicenseType** toohello parametro  **Nuovo AzureVMConfig** cmdlet, passando il valore di hello **Windows_Server** per hello tipico caso di utilizzo.  Verificare se che si sta utilizzando un'immagine che è stato caricato; è possibile utilizzare un'immagine dalla raccolta hello standard con il vantaggio di utilizzare ibrida hello.
> 
> 

Facoltativamente, per un computer Windows autonomo, specificare la password e account di amministratore locale hello.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

Scegliere una password complessa. toocheck il livello di attendibilità, vedere [controllo Password: utilizzo di password complesse](https://www.microsoft.com/security/pc-security/password-checker.aspx).

Facoltativamente, hello tooadd Windows computer tooan dominio Active Directory esistente, specificare l'account amministratore locale hello e password, hello dominio e nome hello e la password di un account di dominio.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Per altre opzioni di pre-configurazione per le macchine virtuali basate su Windows, vedere la sintassi di hello per hello **Windows** e **WindowsDomain** nei set di parametri [ Aggiungere-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).

Facoltativamente, assegnare la macchina virtuale di hello un indirizzo IP specifico, noto come un DIP statico.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

È possibile verificare la disponibilità di uno specifico indirizzo IP con:

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

Facoltativamente, assegnare hello tooa specifiche subnet per macchina virtuale in una rete virtuale di Azure.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

Facoltativamente, aggiungere una macchina virtuale toohello di dati singolo disco.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Per un controller di dominio Active Directory, impostare $hcaching troppo "None".

Facoltativamente, aggiungere hello tooan esistente con bilanciamento del carico set della macchina virtuale per il traffico esterno.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

Infine, scegliere uno di questi blocchi di comando obbligatorio per la creazione di macchine virtuali hello.

Opzione 1: Creare una macchina virtuale hello in un servizio cloud esistente.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

nome breve di Hello del servizio cloud hello è nome hello che compare in elenco hello dei servizi Cloud nel portale di Azure hello o nell'elenco di hello di gruppi di risorse nel portale di Azure hello.

Opzione 2: Creare una macchina virtuale hello in un servizio cloud esistente e la rete virtuale.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>Passaggio 5: eseguire il set di comandi
Esaminare i set di comandi di Azure PowerShell hello compilato in un editor di testo o hello PowerShell ISE composta da più blocchi di comandi del passaggio 4. Assicurarsi di aver specificato tutte le variabili di hello necessita e che dispongono di valori corretti di hello. Assicurarsi inoltre che siano stati rimossi tutti i caratteri di hello < e >.

Se si utilizza un editor di testo, il comando di hello copia impostare toohello Appunti e quindi fare doppio clic su prompt dei comandi di Windows PowerShell aperto. Verrà rilasciare il set di comandi hello come una serie di comandi di PowerShell e creare la macchina virtuale di Azure. In alternativa, eseguire il comando hello impostato in hello PowerShell ISE.

Se si crea nuovamente questa macchina virtuale o una simile, è possibile:

* Salvare questo set di comandi come file di script di PowerShell (*.ps1).
* Salvare questo comando imposta come un runbook di automazione di Azure in hello **gli account di automazione** sezione di hello portale di Azure.

## <a id="examples"></a>Esempi:
Di seguito sono riportati due esempi di attenendosi alla procedura hello sopra toobuild i set di comandi di PowerShell di Azure che creano le macchine virtuali Azure basato su Windows.

### <a name="example-1"></a>Esempio 1
È necessario un PowerShell comando impostato toocreate hello iniziale macchina virtuale per un controller di dominio Active Directory:

* Usa immagine di Windows Server 2012 R2 Datacenter hello.
* Nome hello AZDC1.
* Sia un computer autonomo.
* Disponga di un disco dati aggiuntivo di 20 GB.
* È l'indirizzo IP statico hello 192.168.244.4.
* È nella subnet back-end hello della rete virtuale di hello AZDatacenter.
* Non è nel servizio cloud Azure TailspinToys hello.

Di seguito è hello corrispondente Azure PowerShell comando set toocreate questa macchina virtuale, con le righe vuote tra ogni blocco per migliorare la leggibilità.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>Esempio 2
È necessario un PowerShell set di comandi toocreate una macchina virtuale per un server di line-of-business che:

* Usa immagine di Windows Server 2012 R2 Datacenter hello.
* Nome hello LOB1.
* È un membro del dominio corp.contoso.com hello.
* Disponga di un disco dati aggiuntivo di 200 GB.
* È nella subnet front-end hello della rete virtuale di hello AZDatacenter.
* Non è nel servizio cloud Azure TailspinToys hello.

Di seguito è hello corrispondente Azure PowerShell comando set toocreate questa macchina virtuale.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>Passaggi successivi
Se è necessario un disco del sistema operativo sono maggiore di 127 GB, è possibile [espandere l'unità del sistema operativo hello](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

