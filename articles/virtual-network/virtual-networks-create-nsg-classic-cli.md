---
title: "aaaHow toocreate NSGs in modalità classica con hello CLI di Azure | Documenti Microsoft"
description: "Informazioni su come toocreate e distribuire NSGs in modalità classica utilizzando hello CLI di Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a>Come NSGs toocreate (classico) nell'hello CLI di Azure
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione classica hello. È anche possibile [creare NSGs nel modello di distribuzione di gestione risorse di hello](virtual-networks-create-nsg-arm-cli.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, è innanzitutto necessario generare ambiente di test hello da [la creazione di una rete virtuale](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Come toocreate hello NSG per hello subnet front-end
toocreate denominato di un gruppo denominato **front-end di NSG** a seconda dello scenario hello precedente, procedura hello riportata di seguito.

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello  **`azure config mode`**  comando tooswitch tooclassic modalità come illustrato di seguito.
   
        azure config mode asm
   
    Output previsto:
   
        info:    New mode is asm
3. Eseguire hello  **`azure network nsg create`**  comando toocreate un gruppo.
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    Output previsto:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Parametri
   
   * **-l (o --location)**. Area di Azure in cui hello nuovo gruppo verrà creato. Per questo scenario, *westus*.
   * **-n (o --nome)**. Nome per hello nuovo gruppo. Per questo scenario, *NSG-FrontEnd*.
4. Eseguire hello  **`azure network nsg rule create`**  toocreate comando una regola che consenta l'accesso tooport 3389 (RDP) da hello Internet.
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    Output previsto:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    Parametri
   
   * **-a (o --nsg-name)**. Nome del gruppo hello in cui hello regola verrà creata. Per questo scenario, *NSG-FrontEnd*.
   * **-n (o --nome)**. Nome nuova regola hello. Per questo scenario, *rdp-rule*.
   * **-c (o --action)**. Livello di accesso per la regola di hello (Deny o Consenti).
   * **-p (o --protocol)**. Protocollo (Tcp, Udp o *) per la regola di hello.
   * **-r (o --type)**. Direzione di connessione (Inbound o Outbound).
   * **-y (o --priority)**. Priorità per la regola di hello.
   * **-f (o --source-address-prefix)**. Prefisso dell'indirizzo di origine in CIDR o con tag predefiniti.
   * **-o (o --source-port-range)**. Porta o intervallo di porte di origine.
   * **-e (o --destination-address-prefix)**. Prefisso dell'indirizzo di destinazione in CIDR o con tag predefiniti.
   * **-u (o --destination-port-range)**. Porta o intervallo di porte di destinazione.
5. Eseguire hello  **`azure network nsg rule create`**  toocreate comando una regola che consenta l'accesso tooport 80 (HTTP) da hello Internet.
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    Output previsto:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. Eseguire hello  **`azure network nsg subnet add`**  subnet front-end di comando toolink hello NSG toohello.
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    Output previsto:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Come toocreate hello NSG per hello nuovamente terminare subnet
toocreate denominato di un gruppo denominato *back-end di NSG* a seconda dello scenario hello precedente, procedura hello riportata di seguito.

1. Eseguire hello  **`azure network nsg create`**  comando toocreate un gruppo.
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    Output previsto:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Parametri
   
   * **-l (o --location)**. Area di Azure in cui hello nuovo gruppo verrà creato. Per questo scenario, *westus*.
   * **-n (o --nome)**. Nome per hello nuovo gruppo. Per questo scenario, *NSG-FrontEnd*.
2. Eseguire hello  **`azure network nsg rule create`**  toocreate comando una regola che consenta l'accesso tooport 1433 (SQL) dalla subnet front-end hello.
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    Output previsto:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. Eseguire hello  **`azure network nsg rule create`**  toocreate comando una regola che nega l'accesso toohello Internet.
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    Output previsto:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. Eseguire hello  **`azure network nsg subnet add`**  comando toolink hello NSG toohello nuovamente terminare subnet.
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    Output previsto:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

