---
title: ambiente di test basato su cloud ibrido aaaSimulated | Documenti Microsoft
description: Creare un ambiente cloud ibrido simulato per test per professionisti IT o test di sviluppo, usando due reti virtuali di Azure e una connessione da rete virtuale a rete virtuale.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Configurazione di un ambiente cloud ibrido simulato per l'esecuzione di test
Questo articolo è una guida alla creazione di un ambiente cloud ibrido simulato con Microsoft Azure che usa due reti virtuali di Azure separate. Di seguito è riportata la configurazione risultante hello.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Permette di simulare un ambiente di produzione cloud ibrido e include:

* Una rete locale simulata e semplificata ospitata in una rete virtuale di Azure (rete virtuale di hello esercitazione).
* Una rete virtuale cross-premise simulata ospitata in Azure (TestVNET).
* Una connessione di rete virtuale a tra reti virtuali hello due.
* Un controller di dominio secondario nella rete virtuale di hello TestVNET.

Questa configurazione fornisce una base e un punto di partenza comune da cui è possibile:

* Sviluppare e testare applicazioni in un ambiente cloud ibrido simulato.
* Creare configurazioni di test di computer, alcune all'interno di rete virtuale di esercitazione hello e alcuni in rete virtuale hello TestVNET, toosimulate ibrido basato su cloud carichi di lavoro.

Esistono quattro fasi principali toosetting un ambiente di testing cloud ibrida:

1. Configurare la rete virtuale di hello esercitazione.
2. Creare una rete virtuale cross-premise di hello.
3. Creare la connessione VPN per rete virtuale a hello.
4. Configurare DC2. 

Questa configurazione richiede una sottoscrizione di Azure. Se si ha un abbonamento a MSDN o una sottoscrizione di Visual Studio, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Le macchine virtuali e i gateway di rete virtuale in Azure generano addebiti monetari in caso di esecuzione. Il costo viene addebitato sulla base dell'abbonamento a MSDN o della sottoscrizione a pagamento. Un gateway VPN di Azure viene implementato come set di due macchine virtuali di Azure. costi di hello toominimize, creare l'ambiente di test hello ed eseguire il test e dimostrativi necessari al più presto.
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>Fase 1: Configurare la rete virtuale di hello esercitazione
Utilizzare istruzioni hello in hello [ambiente di test configurazione di Base](https://technet.microsoft.com/library/mt771177.aspx) argomento tooconfigure hello DC1, APP1 e CLIENT1 computer nella rete virtuale di Azure denominato esercitazione hello. 

Avviare un prompt di Azure PowerShell.

> [!NOTE]
> comando set seguenti Hello Usa Azure PowerShell 1.0 e versioni successive.
> 
> 

Eseguire l'accesso tooyour account.

    Login-AzureRMAccount

Ottenere il nome della sottoscrizione tramite hello comando seguente.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Impostare la sottoscrizione di Azure. Utilizzare hello stessa sottoscrizione utilizzata toobuild configurazione di base nella fase 1. Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri, con il nome corretto hello.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

Successivamente, aggiungere una gateway subnet toohello esercitazione rete virtuale della configurazione di base, che sarà utilizzato toohost hello Azure gateway.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

Successivamente, richiedere un pubblico gateway toohello tooassign di indirizzo IP per rete virtuale di hello esercitazione.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

Creare il gateway.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Tenere presente che i nuovi gateway può richiedere 20 minuti o più toocreate.

Da hello portale di Azure nel computer locale, connettersi tooDC1 con credenziali CORP\User1 hello. dominio CORP di tooconfigure hello in modo che utenti e computer di utilizzano i controller di dominio locale per l'autenticazione, eseguire questi comandi da un prompt dei comandi di Windows PowerShell a livello di amministratore in DC1.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Questa è la configurazione corrente.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>Fase 2: Creare la rete virtuale di hello TestVNET
Innanzitutto, creare una rete virtuale di hello TestVNET e proteggerli con un gruppo di sicurezza di rete.

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

Quindi richiesta una toobe di indirizzo IP pubblico allocato toohello gateway per la rete virtuale di hello TestVNET e creare il gateway.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Questa è la configurazione corrente.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>Fase 3: Creare una connessione di rete virtuale a hello
Richiedere all'amministratore di rete o della sicurezza una chiave casuale, crittograficamente complessa, a 32 caratteri, precondivisa. In alternativa, utilizzare informazioni hello [creare una stringa casuale per una chiave precondivisa IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain una chiave già condivisa.

Successivamente, utilizzare questi comandi toocreate hello da rete connessione VPN, che può richiedere alcuni toocomplete ora.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Dopo alcuni minuti, hello devono connettersi.

Questa è la configurazione corrente.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>Fase 4: Configurare DC2.
Creare prima di tutto una macchina virtuale per DC2. Eseguire questi comandi al prompt dei comandi di hello Azure PowerShell nel computer locale.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Successivamente, connettersi toohello nuova macchina virtuale di DC2 da hello portale di Azure.

Configurare quindi il traffico tooallow una regola Windows Firewall per verificare la connettività di base. Da un prompt dei comandi di Windows PowerShell a livello di amministratore in DC2 eseguire questi comandi.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

comando ping Hello dovrebbe restituire quattro risposte dall'indirizzo IP 10.0.0.4. Si tratta di un test di traffico per hello da rete connessione.

Successivamente, aggiungere hello disco dati supplementare in DC2, come un nuovo volume con lettera dell'unità f: hello.

1. Nel riquadro sinistro hello di Server Manager, fare clic su **servizi File e archiviazione**, quindi fare clic su **dischi**.
2. Nel riquadro contenuti hello in hello **dischi** gruppo, fare clic su **disco 2** (con hello **partizione** impostare troppo**sconosciuto**).
3. Fare clic su **Attività**, quindi su **Nuovo volume**.
4. Hello prima pagina della creazione guidata nuovo Volume hello, scegliere **Avanti**.
5. Nel server di selezionare hello hello e pagina su disco, fare clic su **disco 2**, quindi fare clic su **Avanti**. Quando richiesto, fare clic su **OK**.
6. Specifica dimensioni hello della pagina volume hello hello, scegliere **Avanti**.
7. Pagina hello assegnare tooa unità lettera o una cartella, fare clic su **Avanti**.
8. Nella pagina Impostazioni di hello selezionare il file system, fare clic su **Avanti**.
9. Nella pagina Conferma selezioni per hello, fare clic su **crea**.
10. Al termine, fare clic su **Chiudi**.

A questo punto, configurare DC2 come controller di dominio di replica per il dominio corp.contoso.com hello. Eseguire questi comandi dal prompt dei comandi di Windows PowerShell hello in DC2.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Si noti che richiesta toosupply entrambi hello CORP\User1 e password e una password modalità ripristino servizi Directory (DSRM), toorestart DC2.

Ora che hello TestVNET di rete virtuale è il proprio server DNS (DC2), è necessario configurare hello TestVNET rete virtuale toouse questo server DNS.

1. Nel riquadro sinistro di hello di hello portale di Azure, fare clic sull'icona di reti virtuali hello e quindi fare clic su **TestVNET**.
2. In hello **impostazioni** scheda, fare clic su **server DNS**.
3. In **server DNS primario**, tipo **192.168.0.4** tooreplace 10.0.0.4.
4. Fare clic su **Salva**.

Questa è la configurazione corrente. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

L'ambiente cloud ibrido simulato è ora pronto per il testing.

## <a name="next-step"></a>Passaggio successivo
* Configurare un'[applicazione line-of-business basata sul Web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in questo ambiente.

