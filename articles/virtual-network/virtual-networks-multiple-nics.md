---
title: "una macchina virtuale (versione classica) con più schede di rete con PowerShell aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate e configurare macchine virtuali con più schede di rete con PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Creare una VM (classica) con più schede di interfaccia di rete
È possibile creare macchine virtuali (VM) in Azure e collegare più tooeach (NIC) di interfacce di rete delle macchine virtuali. L'uso di più schede di interfaccia di rete è un requisito per molti dispositivi virtuali di rete, ad esempio le soluzioni di ottimizzazione WAN e la distribuzione di applicazioni. Più schede di interfaccia di rete forniscono anche l'isolamento del traffico tra le schede.

![Più NIC per la macchina virtuale](./media/virtual-networks-multiple-nics/IC757773.png)

Hello illustrata nella figura una macchina virtuale con tre schede di rete, ciascuno connesso tooa diverse subnet.

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Microsoft consiglia di usare Resource Manager per la maggior parte delle distribuzioni più recenti.

* VIP con connessione Internet (distribuzioni classiche) è supportato solo nella scheda di rete. "predefinita" hello È presente un solo indirizzo VIP toohello IP della scheda di rete predefinito. hello
* Attualmente, gli indirizzi IP pubblici a livello di istanza (LPIP) (distribuzioni classiche) non sono supportati per le macchine virtuali a più NIC.
* ordine delle schede NIC hello da Hello all'interno di hello macchina virtuale sarà casuale e potrebbe anche cambiare tra gli aggiornamenti dell'infrastruttura di Azure. Tuttavia, hello gli indirizzi IP e hello corrispondente ethernet MAC rimarranno indirizzi hello stesso. Si supponga ad esempio **scheda Eth1** è l'indirizzo IP 10.1.0.100 e l'indirizzo MAC 00-0D-3A-B0-39-0D; dopo l'aggiornamento dell'infrastruttura di Azure e il riavvio, potrebbe essere diventato troppo**Eth2**, ma hello IP e MAC associazione verrà rimangono hello stesso. Quando un riavvio è avviato dall'utente, hello ordine NIC rimarrà hello stesso.
* Hello indirizzo per ogni scheda di rete in ogni macchina virtuale deve trovarsi in una subnet, più schede di rete in una singola macchina virtuale è ogni possibile assegnare gli indirizzi specificati nella stessa subnet di hello.
* Hello dimensioni della macchina virtuale determina il numero di hello di schede di rete che è possibile creare per una macchina virtuale. Hello riferimento [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM di dimensioni toodetermine articoli quante NIC supporta ogni dimensione della macchina virtuale. 

## <a name="network-security-groups-nsgs"></a>Gruppi di sicurezza di rete (NGS)
In una distribuzione di Gestione risorse, qualsiasi NIC in una macchina virtuale può essere associata a un Gruppo di sicurezza di rete, incluse eventuali NIC in una macchina virtuale che presenta la funzionalità Multi-NIC abilitata. Se una scheda di rete viene assegnato un indirizzo all'interno di una subnet in cui è associato a un gruppo subnet hello, hello regole nel gruppo della subnet hello anche applicano toothat scheda di rete. Nella subnet di addizione tooassociating con NSGs, è anche possibile associare una scheda di rete con un gruppo.

Se una subnet è associata a un gruppo e una scheda di rete all'interno di subnet è singolarmente associata a un gruppo, le regole NSG hello associata vengono applicate **flusso ordine** in base toohello direzione del traffico hello passato interna o esterna Hello scheda di rete:

* **Il traffico in ingresso** la cui destinazione è hello NIC in questione passano innanzitutto attraverso subnet hello, attivare le regole di NSG della subnet hello, prima di passare in hello NIC, quindi attivare le regole di NSG hello NIC.
* **Il traffico in uscita** la cui origine è hello NIC in questione flussi prima fuori dalla scheda di rete, attivare le regole di NSG hello NIC, prima di attraversamento subnet hello, quindi attivare le regole di NSG della subnet hello hello.

Altre informazioni, vedere [gruppi di sicurezza di rete](virtual-networks-nsg.md) e come vengono applicate in base alle associazioni toosubnets, le macchine virtuali e schede di rete...

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>Come tooConfigure un più NIC VM in una distribuzione classica
Hello istruzioni seguenti consentono di creare una VM NIC contenente 3 schede di rete multi: una scheda di rete predefinita e due schede aggiuntive. passaggi di configurazione Hello verranno creata una macchina virtuale che verrà configurata in base toohello servizio configurazione frammento del file seguente:

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


È necessario hello seguenti prerequisiti prima di tentare di comandi di PowerShell hello toorun nell'esempio hello.

* Una sottoscrizione di Azure.
* Una rete virtuale configurata. Per altre informazioni sulle reti virtuali, vedere [Panoramica di Rete virtuale](virtual-networks-overview.md) .
* versione più recente di Hello di Azure PowerShell scaricato e installato. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

toocreate una macchina virtuale con più schede di rete, hello completa immettendo ogni comando in una singola sessione di PowerShell come segue:

1. Selezionare un'immagine di macchina virtuale dalla raccolta immagini della macchina virtuale di Azure. Le immagini cambiano frequentemente e sono disponibili per area geografica. Hello immagine specificata nel seguente esempio hello può modificare o potrebbe non essere disponibile nell'area, pertanto è necessario assicurarsi immagine hello toospecify necessaria.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Creare una configurazione di macchina virtuale.

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Creare account di accesso amministratore predefinito hello.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Aggiungere una configurazione della macchina virtuale toohello schede aggiuntive.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Specificare l'indirizzo IP e subnet di hello per hello scheda NIC del valore predefinito.

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Creare hello VM nella rete virtuale.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > rete virtuale che è possibile specificare Hello deve già esistere (come indicato nei prerequisiti hello). esempio Hello seguente specifica una rete virtuale denominata **multi-VNet**.
    >

## <a name="limitations"></a>Limitazioni
Hello limitazioni seguenti sono applicabile quando si utilizzano più schede di rete:

* È necessario creare VM con più schede di interfaccia di rete nelle reti virtuali di Azure. Non è possibile configurare VM che non si trovano in reti virtuali con più schede di interfaccia di rete.
* Tutte le macchine virtuali in un disponibilità impostare toouse necessità più schede di rete o una singola scheda di rete. Non è possibile combinare VM con più schede di interfaccia di rete e VM con una singola scheda di interfaccia di rete all'interno di un set di disponibilità. Le stesse regole sono valide per le VM in un servizio cloud. Per più macchine virtuali, NIC non sono necessari toohave hello stesso numero di schede di rete, purché ognuna di esse presenta almeno due.
* Non è possibile configurare una VM con una singola scheda di interfaccia di rete con più schede di interfaccia di rete (e viceversa) dopo la distribuzione, senza eliminarla e crearla di nuovo.

## <a name="secondary-nics-access-tooother-subnets"></a>Schede di rete secondarie accedere tooother subnet
Per impostazione predefinita secondaria NIC non verranno configurate con un gateway predefinito, a causa di flusso del traffico toowhich hello in hello NIC secondaria sarà limitato toobe all'interno di hello stessa subnet. Se gli utenti di hello desiderano tooenable secondario NIC tootalk esterno le proprie subnet, sarà necessario tooadd una voce in hello tabella tooconfigure hello gateway di routing come descritto di seguito.

> [!NOTE]
> Le VM create prima di luglio 2015 potrebbero avere un gateway predefinito configurato per tutte le NIC. gateway predefinito Hello per le schede NIC secondario non verrà rimosso fino a quando non vengono riavviate queste macchine virtuali. In sistemi operativi che utilizzano un modello di host vulnerabile routing hello, ad esempio Linux, è possibile interrompere la connettività a Internet se il traffico in ingresso e uscita hello Usa diverse schede di rete.
> 

### <a name="configure-windows-vms"></a>Configurare le macchine virtuali Windows
Supponiamo di utilizzare una macchina virtuale di Windows con due NIC come indicato di seguito:

* Indirizzo IP primario della NIC: 192.168.1.4
* Indirizzo IP secondario della NIC: 192.168.2.5

tabella di routing IPv4 Hello per questa macchina virtuale sarebbe simile al seguente:

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

Route predefinita (0.0.0.0) hello è solo toohello disponibili primario scheda di rete. Non sarà tooaccess in grado di risorse esterno hello subnet per hello secondario NIC, come illustrato di seguito:

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

tooadd predefinito instradare sulla hello secondario NIC, seguire hello passaggi riportati di seguito:

1. Da un prompt dei comandi, eseguire il comando di hello sotto tooidentify hello numero di indice hello NIC secondario:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. Si noti hello seconda voce tabella hello, con un indice pari a 27 (in questo esempio).
3. Dal prompt dei comandi di hello, eseguire hello **aggiungere route** comando come illustrato di seguito. In questo esempio si specifica 192.168.2.1 come gateway predefinito hello per hello NIC secondario:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. connettività tootest, tornare indietro toohello il prompt dei comandi e provare tooping una subnet diversa da hello NIC secondario come int illustrato eh esempio riportato di seguito:
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. È inoltre possibile verificare che il hello toocheck tabella di route appena aggiunti route, come illustrato di seguito:
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>Configurare le macchine virtuali Linux
Per le macchine virtuali Linux, poiché il comportamento predefinito di hello utilizza host vulnerabile routing, è consigliabile che hello secondaria NIC sono flussi tootraffic limitato solo all'interno di hello stessa subnet. Tuttavia, se alcuni scenari richiedono la connettività all'esterno di hello subnet, gli utenti devono attivare tooensure di routing basata su criteri che hello in ingresso e Usa il traffico in uscita hello stessa scheda di rete.

## <a name="next-steps"></a>Passaggi successivi
* Distribuire [Macchine virtuali MultiNIC in uno scenario di applicazione a 2 livelli in una distribuzione di Gestione risorse](virtual-network-deploy-multinic-arm-template.md).
* Distribuire [Macchine virtuali MultiNIC in uno scenario di applicazione a 2 livelli in una distribuzione classica](virtual-network-deploy-multinic-classic-ps.md).

