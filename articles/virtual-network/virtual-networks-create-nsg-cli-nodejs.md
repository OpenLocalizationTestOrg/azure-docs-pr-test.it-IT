---
title: -i gruppi di sicurezza di rete aaaCreate 1.0 CLI di Azure | Documenti Microsoft
description: Informazioni su come toocreate e distribuire i gruppi di sicurezza di rete utilizzando hello Azure CLI 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a>Creare gruppi di protezione utilizzando hello Azure CLI 1.0 di rete


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI 

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello: 

- [Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -CLI la prossima generazione per modello di distribuzione di gestione risorse hello 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [creare NSGs nel modello di distribuzione classica hello](virtual-networks-create-nsg-classic-cli.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente. 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Come toocreate hello NSG per hello subnet front-end
toocreate denominato di un gruppo denominato *front-end di NSG* a seconda dello scenario hello precedente, procedura hello riportata di seguito.

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.
   
        azure config mode arm
   
    Output previsto:
   
        info:    New mode is arm
3. Eseguire hello **rete azure creare** comando toocreate un gruppo.
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    Output previsto:
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    Parametri
   
   * **-g (o --resource-group)**. Nome del gruppo di risorse hello in cui verrà creato hello gruppo. Per questo scenario, *TestRG*.
   * **-l (o --location)**. Area di Azure in cui hello nuovo gruppo verrà creato. Per questo scenario, *westus*.
   * **-n (o --nome)**. Nome per hello nuovo gruppo. Per questo scenario, *NSG-FrontEnd*.
4. Eseguire hello **regola gruppo di rete di azure creare** toocreate comando una regola che consenta l'accesso tooport 3389 (RDP) da hello Internet.
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    Output previsto:
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    Parametri
   
   * **-a (o --nsg-name)**. Nome del gruppo hello in cui hello regola verrà creata. Per questo scenario, *NSG-FrontEnd*.
   * **-n (o --nome)**. Nome nuova regola hello. Per questo scenario, *rdp-rule*.
   * **-c (o --access)**. Livello di accesso per la regola di hello (Deny o Consenti).
   * **-p (o --protocol)**. Protocollo (Tcp, Udp o *) per la regola di hello.
   * **-r (o--direction)**. Direzione di connessione (Inbound o Outbound).
   * **-y (o --priority)**. Priorità per la regola di hello.
   * **-f (o --source-address-prefix)**. Prefisso dell'indirizzo di origine in CIDR o con tag predefiniti.
   * **-o (o --source-port-range)**. Porta o intervallo di porte di origine.
   * **-e (o --destination-address-prefix)**. Prefisso dell'indirizzo di destinazione in CIDR o con tag predefiniti.
   * **-u (o --destination-port-range)**. Porta o intervallo di porte di destinazione.    
5. Eseguire hello **regola gruppo di rete di azure creare** toocreate comando una regola che consenta l'accesso tooport 80 (HTTP) da hello Internet.
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    Output previsto:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. Eseguire hello **set di subnet della rete virtuale azure rete** subnet front-end di comando toolink hello NSG toohello.
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    Output previsto:
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Come toocreate hello NSG per hello nuovamente terminare subnet
toocreate denominato di un gruppo denominato *back-end di NSG* a seconda dello scenario hello precedente, procedura hello riportata di seguito.

1. Eseguire hello **rete azure creare** comando toocreate un gruppo.
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    Output previsto:
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. Eseguire hello **regola gruppo di rete di azure creare** toocreate comando una regola che consenta l'accesso tooport 1433 (SQL) dalla subnet front-end hello.
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    Output previsto:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. Eseguire hello **regola gruppo di rete di azure creare** toocreate comando una regola che nega l'accesso toohello Internet da.
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    Output previsto:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. Eseguire hello **set di subnet della rete virtuale azure rete** comando toolink hello NSG toohello nuovamente terminare subnet.
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    Output previsto:
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

