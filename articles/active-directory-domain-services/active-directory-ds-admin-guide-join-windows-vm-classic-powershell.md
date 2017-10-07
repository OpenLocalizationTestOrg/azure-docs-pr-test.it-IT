---
title: 'Azure Active Directory Domain Services: Guida all''amministrazione | Microsoft Docs'
description: Un dominio Windows macchina virtuale tooa gestito tramite Azure PowerShell e il modello di distribuzione classica hello.
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>Un dominio Windows Server macchina virtuale tooa gestito con PowerShell
> [!div class="op_single_selector"]
> * [Portale di Azure classico - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Servizi di dominio Active Directory di Azure non supporta attualmente il modello di gestione risorse di hello.
>
>

Questi passaggi mostrano come toocustomize una serie di Azure PowerShell comandi che creare e preconfigurare una macchina virtuale Azure basato su Windows utilizzando un approccio di blocco predefinito. Questi passaggi consentono di creare una macchina virtuale Azure basato su Windows e creare un join tooan dominio gestito di servizi di dominio Active Directory di Azure.

Questi passaggi seguono un approccio basato sul completamento di valori predefiniti per la creazione di set di comandi di Azure PowerShell. Questo approccio può essere utile se si tooPowerShell nuovo o si desidera tooknow toospecify i valori per la corretta configurazione. Gli utenti esperti di PowerShell possono accettare i comandi di hello e sostituire i propri valori per le variabili di hello (righe hello che iniziano con "$").

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

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>Passaggio 3: Guida dettagliata - eseguire il provisioning di macchina virtuale hello e aggiungerla dominio gestito toohello
Di seguito è hello corrispondente Azure PowerShell comando set toocreate questa macchina virtuale, con le righe vuote tra ogni blocco per migliorare la leggibilità.

Specificare le informazioni su toobe macchina virtuale di Windows hello il provisioning.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

Per i valori di InstanceSize hello per D, di dominio Active Directory o macchine virtuali serie G, vedere [macchina virtuale e alle dimensioni dei servizi Cloud per Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

Vengono fornite informazioni di dominio gestiti hello.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Specificare il nome di hello del servizio cloud hello.

    $svcname="Contoso100-test"

Specificare il nome di hello di hello toowhich di rete virtuale hello che VM devono essere unite in join. Verificare che tale dominio gestito AAD-DS hello è disponibile in questa rete virtuale.

    $vnetname="MyPreviewVnet"

Selezionare hello VM immagine toobe utilizzato tooprovision hello macchina virtuale.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Configurare hello VM - nome del set di VM toobe di dimensioni e l'immagine di istanza utilizzata.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Ottenere le credenziali di amministratore locale per hello macchina virtuale. Scegliere una password di amministratore locale sicura.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Ottenere le credenziali per un account utente di dominio gestiti degli amministratori di controller di dominio too'AAD gruppo toojoin VM toohello appartenenti. Non specificare il nome di dominio hello - per istanza, in questo esempio, si specifica "bob" come nome utente hello.

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

Configurare hello VM - specificare il requisito di join dominio & credenziali necessarie.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Impostare una subnet per hello macchina virtuale.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

Facoltativo: Scegliere l'indirizzo IP toohello del dominio hello. Se si imposta gli indirizzi IP hello di hello toobe gestito dominio servizi di dominio Active Directory di Azure di hello server DNS per la rete virtuale hello, questo passaggio non è obbligatorio.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

A questo punto, hello provisioning dominio macchina virtuale di Windows.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Script tooprovision una macchina virtuale di Windows e aggiungerla automaticamente tooan dominio gestito di servizi di dominio di Azure ad
Questo set di comandi di PowerShell crea una macchina virtuale per un server line-of-business che:

* Usa immagine di Windows Server 2012 R2 Datacenter hello.
* È una macchina virtuale molto piccola.
* Nome hello Contoso100-test.
* Viene automaticamente dominio gestito contoso100 di toohello aggiunti a un dominio.
* Viene aggiunto toohello stessa rete virtuale hello gestiti dominio.

Ecco hello macchina virtuale Windows di esempio completo script toocreate hello e aggiungerla automaticamente toohello dominio gestito di servizi di dominio Active Directory di Azure.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Amministrare un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-administer-domain.md)
