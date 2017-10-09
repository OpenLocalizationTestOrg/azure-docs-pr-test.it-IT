---
title: aaaTroubleshoot gruppi di sicurezza di rete - PowerShell | Documenti Microsoft
description: Informazioni su come gruppi di sicurezza di rete tootroubleshoot nella distribuzione di Azure Resource Manager hello del modello con Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Risolvere i problemi relativi ai gruppi di sicurezza di rete tramite Azure PowerShell
> [!div class="op_single_selector"]
> * [Portale di Azure](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Se si sono verificati problemi di connettività di macchina virtuale configurato rete sicurezza gruppi sulla macchina virtuale (VM), in questo articolo fornisce una panoramica delle funzionalità di diagnostica per NSGs toohelp risolvere il problema.

NSGs consentono tipi hello toocontrol di traffico che il flusso da e verso le macchine virtuali (VM). NSGs può essere applicato toosubnets in una rete virtuale di Azure (VNet), le interfacce di rete (NIC) o entrambi. Hello regole efficaci applicate tooa NIC sono un'aggregazione di regole hello esistenti hello NSGs applicato tooa NIC e hello subnet è connesso a. Talvolta le regole nei gruppi di sicurezza di rete possono essere in conflitto tra loro e influire sulla connettività di rete della VM.  

È possibile visualizzare tutte le regole di sicurezza efficace hello dal NSGs, così come applicato nelle schede NIC della macchina virtuale. Questo articolo illustra come problemi di connettività VM tootroubleshoot usando queste regole in hello modello di distribuzione Azure Resource Manager. Se non si ha familiarità con i concetti di rete virtuale e di gruppo, leggere hello [rete virtuale](virtual-networks-overview.md) e [gruppi di sicurezza di rete](virtual-networks-nsg.md) articoli Panoramica.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Utilizzando le regole di sicurezza efficace tootroubleshoot VM il flusso del traffico
scenario di Hello che segue è un esempio di un problema di connessione comuni:

Una macchina virtuale denominata *VM1* fa parte di una subnet denominata *Subnet1* in una rete virtuale denominata *WestUS-VNet1*. Un toohello tooconnect tentativo di VM che utilizzano il protocollo RDP sulla porta TCP 3389 ha esito negativo. NSGs vengono applicate a entrambi hello NIC *VM1 NIC1* e hello subnet *Subnet1*. La porta 3389 tooTCP di traffico è consentita in hello NSG associata con l'interfaccia di rete hello *VM1 NIC1*, tuttavia TCP effettuare il ping ha esito 3389 negativo di porta del tooVM1.

Mentre in questo esempio viene usata la porta TCP 3389, hello i passaggi seguenti può essere utilizzati toodetermine errori di connessione in ingresso e in uscita su qualsiasi porta.

## <a name="detailed-troubleshooting-steps"></a>Procedura di risoluzione dei problemi dettagliata
Completare hello seguendo i passaggi tootroubleshoot NSGs per una macchina virtuale:

1. Avviare un tooAzure di sessione e l'account di accesso di Azure PowerShell. Se non si ha familiarità con Azure PowerShell, leggere hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.
2. Immettere hello comando tooreturn tutte le regole di gruppo applicate tooa NIC denominato seguente *VM1 NIC1* nel gruppo di risorse hello *RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Se non si conosce il nome di hello di una scheda di rete, immettere hello seguente i nomi di comando tooretrieve hello di tutte le schede di rete in un gruppo di risorse: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    testo Hello è riportato un esempio dell'output di hello regole valide per hello restituito *VM1 NIC1* NIC:
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    Tenere presente le seguenti informazioni nell'output di hello hello:
   
   * Esistono due sezioni in **NetworkSecurityGroup**: una è associata a una subnet (*Subnet1*), l'altra a un'interfaccia di rete (*VM1-NIC1*). In questo esempio, un gruppo è stato applicato tooeach.
   * **Associazione** Mostra risorse hello (subnet o NIC) è associata a un gruppo specificato. Se hello risorsa gruppo spostato dissociare immediatamente prima di eseguire questo comando, si potrebbe essere necessario toowait alcuni secondi per hello modifica tooreflect nell'output del comando hello. 
   * i nomi delle regole che sono preceduti Hello *defaultSecurityRules*: viene creato quando di un gruppo, vengono create diverse regole di sicurezza predefinito. Le regole predefinite non possono essere rimosse, tuttavia possono essere sostituite con regole dalla priorità più elevata.
     Hello lettura [Panoramica gruppo](virtual-networks-nsg.md#default-rules) toolearn articolo ulteriori informazioni su gruppo predefinito di regole di sicurezza.
   * **ExpandedAddressPrefix** espande i prefissi di indirizzo hello per tag di gruppo predefiniti. I tag rappresentano più prefissi di indirizzi. Espansione di tag hello può essere utile quando la risoluzione dei problemi di connettività di macchina virtuale da e verso i prefissi di indirizzo specifico. Ad esempio, con peering reti VIRTUALI, i tag VIRTUAL_NETWORK espande tooshow peering prefissi di rete virtuale nell'output precedente hello.
     
     > [!NOTE]
     > Hello regole efficaci Mostra solo comando se un gruppo è associata a una subnet, una scheda di rete o entrambi. Una VM può avere diverse interfacce di rete a cui sono applicati vari gruppi di sicurezza di rete. Per risolvere il problema, eseguire il comando di hello per ogni scheda di rete.
     > 
     > 
3. tooease filtro su un numero elevato di regole di gruppo, immettere hello ulteriormente tootroubleshoot i comandi seguenti: 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    Un filtro per il traffico RDP (porta TCP 3389), viene applicato toohello visualizzazione griglia, come illustrato nella seguente immagine hello:
   
    ![Elenco di regole](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. Come può vedere nella visualizzazione griglia hello, sono presenti entrambi consentono e le regole di negazione per RDP. Hello passaggio 2 Mostra output di hello *DenyRDP* regola è nella subnet toohello NSG applicato hello. Per le regole in entrata, vengono prima elaborate subnet toohello NSGs applicato. Se viene trovata una corrispondenza, l'interfaccia di rete hello NSG applicato toohello non elaborato. In questo caso, hello *DenyRDP* regola dalla subnet hello Blocca RDP toohello VM (**VM1**).
   
   > [!NOTE]
   > Una macchina virtuale può avere più tooit collegato a schede di rete. Ognuno può essere connesso tooa diverse subnet. Poiché i comandi di hello nei passaggi precedenti hello vengono eseguiti su una scheda di rete, è importante tooensure specificato hello NIC si verificano errori di connettività hello per. Se non si è certi, è sempre possibile eseguire i comandi di hello in ogni macchina virtuale di toohello NIC associata.
   > 
   > 
5. tooRDP in VM1, hello modifica *negare RDP (3389)* regola troppo*consentire RDP(3389)* in hello **Subnet1 NSG** gruppo. Verificare che la porta TCP 3389 sia aperta aprendo un toohello connessione RDP macchina virtuale o lo strumento PsPing hello. È possibile approfondire PsPing da lettura hello [PsPing pagina di download](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    È possibile o rimuovere le regole da un gruppo usando hello informazioni nell'output di hello dalla hello comando seguente:
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>Considerazioni
Prendere in considerazione hello seguenti punti durante la risoluzione dei problemi di connettività:

* Regole predefinite di NSG bloccherà l'accesso in ingresso da hello internet e solo Consenti rete virtuale il traffico in ingresso. Le regole devono essere aggiunto esplicitamente tooallow accesso in entrata da Internet, come richiesto.
* Se non sono presenti regole di sicurezza gruppo causando toofail connettività di rete della macchina virtuale, problema di hello può essere dovuto a:
  * Software di firewall in esecuzione all'interno del sistema operativo della macchina virtuale di hello
  * Route configurate per appliance virtuali o traffico locale. Il traffico Internet può essere reindirizzati tooon locali tramite il tunneling forzato. Una connessione RDP/SSH da hello Internet tooyour macchina virtuale potrebbe non funzionare con questa impostazione, a seconda di come hardware di rete locale hello gestisce tale traffico. Hello lettura [risoluzione dei problemi delle route](virtual-network-routes-troubleshoot-powershell.md) toolearn articolo come problemi di route toodiagnose che potrebbero ostacolare hello flusso del traffico in e out di hello macchina virtuale. 
* Se si dispongano di peering reti virtuali, per impostazione predefinita, hello tag VIRTUAL_NETWORK espanderà automaticamente i prefissi tooinclude per il peering reti virtuali. È possibile visualizzare tali prefissi nella hello **ExpandedAddressPrefix** elencare, tootroubleshoot qualsiasi tooVNet correlate a problemi peering di connettività. 
* Le regole di sicurezza efficace vengono visualizzate solo se è che un gruppo associato della macchina virtuale di hello NIC e o una subnet. 
* Se non sono non NSGs associato hello NIC o subnet e si dispone di un indirizzo IP pubblico assegnato tooyour VM, tutte le porte sarà aperte per l'accesso in ingresso e in uscita. Se hello macchina virtuale ha un indirizzo IP pubblico, l'applicazione NSGs toohello NIC o una subnet è consigliabile.  

