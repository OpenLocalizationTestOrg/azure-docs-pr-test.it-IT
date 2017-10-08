---
title: indirizzi IP privati aaaConfigure per le macchine virtuali (classico) - CLI di Azure 1.0 | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per le macchine virtuali (classico) utilizzando hello Azure interfaccia della riga di comando (CLI) 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Configurare gli indirizzi IP privati per una macchina virtuale (classico) utilizzando hello Azure CLI 1.0

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione classica hello. È anche possibile [gestire un indirizzo IP privato statico nel modello di distribuzione di gestione risorse di hello](virtual-networks-static-private-ip-arm-cli.md).

Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Come toospecify un indirizzo IP privato statico di indirizzi durante la creazione di una macchina virtuale
una nuova macchina virtuale denominata toocreate *DNS01* in un nuovo servizio cloud denominato *TestService* a seconda dello scenario hello precedente, seguire questi passaggi:

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.
2. Eseguire hello **servizio di azure creare** servizio cloud di hello toocreate di comando.
   
        azure service create TestService --location uscentral
   
    Output previsto:
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Eseguire hello **azure creare una macchina virtuale** comando toocreate hello macchina virtuale. Si noti il valore di hello per un indirizzo IP privato statico. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    Output previsto:
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (o --location)**. Area di Azure in cui verrà creato hello macchina virtuale. Per questo scenario, *centralus*.
   * **-n (o --vm-name)**. Nome di hello VM toobe creato.
   * **-w (o --virtual-network-name)**. Nome della rete virtuale in cui verrà creato hello VM hello. 
   * **-S (o --static-ip)**. Indirizzo IP privato statico per hello macchina virtuale.
   * **TestService**. Nome del servizio cloud hello in cui verrà creato hello macchina virtuale.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**. Immagine utilizzata toocreate hello macchina virtuale.
   * **adminuser**. Amministratore locale per la macchina virtuale di Windows hello.
   * **AdminP@ssw0rd**. Password dell'amministratore locale per la macchina virtuale di Windows hello.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale
IP privato statico di tooview hello informazioni sull'indirizzo di hello macchina virtuale creata con lo script hello precedente, eseguire il comando CLI di Azure seguente hello e osservare il valore di hello per *StaticIP rete*:

    azure vm static-ip show DNS01

Output previsto:

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale
tooremove hello indirizzo IP privato statico aggiunta toohello VM hello allo script precedente, hello esecuzione comando CLI di Azure seguente:

    azure vm static-ip remove DNS01

Output previsto:

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>Come tooadd un tooan IP statico privato macchina virtuale esistente
tooadd un statico privato IP indirizzo toohello macchina virtuale creata utilizzando lo script hello sopra, Run il seguente comando:

    azure vm static-ip set DNS01 192.168.1.101

Output previsto:

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .
* Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).

