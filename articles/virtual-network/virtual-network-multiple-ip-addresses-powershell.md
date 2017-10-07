---
title: gli indirizzi IP aaaMultiple per macchine virtuali di Azure - PowerShell | Documenti Microsoft
description: "Informazioni su come tooassign più gli indirizzi IP macchina virtuale tooa mediante PowerShell | Gestore delle risorse."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>Assegnare più indirizzi IP macchine toovirtual mediante PowerShell

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

In questo articolo viene illustrato come una macchina virtuale (VM) durante la distribuzione Azure Resource Manager hello toocreate modello tramite PowerShell. Impossibile assegnare più indirizzi IP tooresources creato tramite il modello di distribuzione classica hello. ulteriori informazioni sui modelli di distribuzione di Azure, leggere hello toolearn [comprendere i modelli di distribuzione](../resource-manager-deployment-model.md) articolo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Creare una macchina virtuale con più indirizzi IP

passaggi di Hello che seguono viene illustrato come toocreate un esempio di macchina virtuale con più IP risolve, come descritto nello scenario di hello. Modificare i valori delle variabili come necessario per l'implementazione.

1. Aprire un prompt dei comandi di PowerShell e completato hello rimanenti passaggi in questa sezione all'interno di una singola sessione di PowerShell. Se si dispone già di PowerShell installato e configurato, hello completato i passaggi in hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.
2. Account di accesso tooyour con hello `login-azurermaccount` comando.
3. Sostituire *myResourceGroup* e *westus* con un nome e una località di propria scelta. Creare un gruppo di risorse. Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. Creare una rete virtuale (VNet) e la subnet in hello stesso percorso del gruppo di risorse hello:

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. Creare un gruppo di sicurezza di rete e una regola. Hello NSG protegge hello VM utilizzando le regole in entrata e in uscita. In questo caso viene creata una regola in entrata per la porta 3389 che consente connessioni desktop remoto in ingresso.

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. Definire una configurazione IP primaria hello per hello scheda di rete. Indirizzo tooa modifica 10.0.0.4 nella subnet hello è stato creato, se non è stato utilizzato il valore di hello definito in precedenza. Prima di assegnare un indirizzo IP statico, è consigliabile verificare che non sia già in uso. Immettere il comando hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`. Se è disponibile l'indirizzo di hello, hello output restituisce *True*. Se non è disponibile, hello output restituisce *False* e un elenco di indirizzi disponibili. 

    In seguito comandi, hello **sostituire < replace-con-your-univoco-name > con toouse di nome DNS univoco hello.** nome di Hello deve essere univoco tra tutti gli indirizzi IP pubblici all'interno di un'area di Azure. Questo è un parametro facoltativo. Può essere rimosso se si desidera solo tooconnect toohello VM utilizzando l'indirizzo IP pubblico hello.

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    Quando si assegna più tooa di configurazioni IP NIC, una configurazione deve essere assegnata come hello *-primaria*.

    > [!NOTE]
    > Per gli indirizzi IP pubblici è prevista una tariffa nominale. ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione. informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.

7. Definire configurazioni IP secondarie di hello per hello scheda di rete. È possibile aggiungere o rimuovere le configurazioni in base alle esigenze. Ogni configurazione IP deve avere un indirizzo IP privato assegnato. Ogni configurazione può avere facoltativamente un indirizzo IP pubblico assegnato.

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. Creare hello NIC e associare tooit di configurazioni IP tre hello:

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >Anche se tutte le configurazioni vengono assegnate tooone NIC in questo articolo, è possibile assegnare più IP configurazioni tooevery NIC associata toohello macchina virtuale. modalità di lettura di una macchina virtuale con più schede di rete, toocreate toolearn hello [creare una macchina virtuale con più schede di rete](virtual-network-deploy-multinic-arm-ps.md) articolo.

9. Creare VM hello immettendo hello seguenti comandi:

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. Toohello macchina virtuale del sistema operativo di indirizzi IP privati di Aggiungi hello completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo. Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.

## <a name="add"></a>Aggiungere tooa di indirizzi IP VM

È possibile aggiungere pubblica e privata IP indirizzi tooa NIC completando i passaggi di hello che seguono. Hello esempi in hello nelle sezioni che seguono si presuppone che si dispone di una macchina virtuale con le configurazioni IP hello tre descritte in hello [scenario](#Scenario) in questo articolo, ma non è necessario eseguire.

1. Aprire un prompt dei comandi di PowerShell e completato hello rimanenti passaggi in questa sezione all'interno di una singola sessione di PowerShell. Se si dispone già di PowerShell installato e configurato, hello completato i passaggi in hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.
2. Modificare hello "valori" hello dopo il nome di toohello $Variables di hello NIC desiderato tooadd IP indirizzo tooand hello risorsa gruppo e il percorso hello in che NIC esiste:

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Se non si conosce il nome di hello di hello NIC desiderato toochange, immettere i seguenti comandi hello, quindi modificare i valori hello variabili precedenti hello:

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. Creare una variabile e impostarlo toohello esistente NIC digitando hello comando seguente:

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. In hello seguenti comandi, modificare *MyVNet* e *MySubnet* toohello nomi di hello hello rete virtuale e subnet, è connessa al. Immettere hello comandi tooretrieve hello rete virtuale e subnet oggetti hello a che connessa:

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    Se non si conosce hello rete virtuale o una subnet nome hello a che connessa, immettere hello comando seguente:
    ```powershell
    $MyNIC.IpConfigurations
    ```
    Nell'output di hello, cercare toohello di testo simili output di esempio riportato di seguito:
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    In questo output *MyVnet* è hello rete virtuale e *MySubnet* è hello subnet hello è connessa al.

5. Completare i passaggi di hello in uno di hello le sezioni, in base ai requisiti seguenti:

    **Aggiungere un indirizzo IP privato**

    tooadd un tooa di indirizzo IP privato NIC, è necessario creare una configurazione IP. Hello seguente comando crea una configurazione con un indirizzo IP statico 10.0.0.7. Quando si specifica un indirizzo IP statico, deve essere un indirizzo per subnet hello inutilizzato. È consigliabile testare tooensure indirizzo hello è disponibile tramite l'immissione di hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` comando. Se l'indirizzo IP hello è disponibile, hello output restituisce *True*. Se non è disponibile, hello output restituisce *False*e un elenco di indirizzi disponibili.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).

    Aggiungere hello private IP indirizzo toohello macchina virtuale sistema operativo completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.

    **Aggiungere un indirizzo IP pubblico**

    Associando un tooeither di risorsa indirizzo IP pubblico, una nuova configurazione IP o una configurazione IP esistente, viene aggiunto un indirizzo IP pubblico. Completare i passaggi di hello nelle sezioni che seguono, hello necessari.

    > [!NOTE]
    > Per gli indirizzi IP pubblici è prevista una tariffa nominale. ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione. informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.
    >

    - **Associare hello pubblica risorsa tooa nuovo IP configurazione degli indirizzi IP**
    
        Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato. È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova. toocreate uno nuovo, immettere hello comando seguente:
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        una nuova configurazione IP con un indirizzo IP privato statico e hello associata toocreate *myPublicIp3* indirizzo IP pubblico risorsa degli indirizzi, immettere hello comando seguente:

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Associare hello pubblica risorsa tooan esistente IP configurazione degli indirizzi IP**

        Una risorsa di indirizzo IP pubblica può essere solo la configurazione IP tooan associato che non ha ancora associata. È possibile determinare se una configurazione IP è un indirizzo IP pubblico associato immettendo hello comando seguente:

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        Viene visualizzato il seguente toohello simili di output:

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        Poiché hello **PublicIpAddress** colonna per *IpConfig 3* è vuoto, nessuna risorsa dell'indirizzo IP pubblica è tooit attualmente associato. È possibile aggiungere un esistente pubblica IP indirizzo risorsa tooIpConfig-3 o immettere hello toocreate comando uno di seguito:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        Immettere hello comando risorsa toohello configurazione IP esistente denominato di indirizzo IP pubblico di tooassociate hello seguente *IpConfig 3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Impostare hello NIC con configurazione IP nuovo hello immettendo hello comando seguente:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. Visualizzare gli indirizzi IP privati hello e hello pubblica IP indirizzo risorse assegnato toohello NIC immettendo hello comando seguente:

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. Aggiungere hello private IP indirizzo toohello macchina virtuale sistema operativo completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo. Non aggiungere hello pubblica IP indirizzo toohello del sistema operativo.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
