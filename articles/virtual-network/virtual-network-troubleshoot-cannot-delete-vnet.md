---
title: aaaCannot eliminare una rete virtuale in Azure | Documenti Microsoft
description: "Informazioni su come tootroubleshoot hello problema in cui non è possibile eliminare una rete virtuale in Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Risoluzione dei problemi: Impossibile toodelete una rete virtuale in Azure

È possibile ricevere errori quando si tenta di toodelete una rete virtuale in Microsoft Azure. Questo articolo fornisce la risoluzione dei problemi toohelp passaggi risolvere il problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Guida alla risoluzione dei problemi 

1. [Verificare se un gateway di rete virtuale è in esecuzione nella rete virtuale hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Verificare se un gateway applicazione è in esecuzione nella rete virtuale hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Controllare se il servizio di dominio Azure Active Directory è abilitato nella rete virtuale hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Controllare se la rete virtuale hello è connesso tooother risorse](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Controllare se una macchina virtuale è ancora in esecuzione nella rete virtuale hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Controllare se la rete virtuale hello è bloccata nella migrazione](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>Verificare se un gateway di rete virtuale è in esecuzione nella rete virtuale hello

rete virtuale hello tooremove, è necessario rimuovere prima il gateway di rete virtuale hello.

Per le reti virtuali classiche, visitare toohello **Panoramica** pagina della rete virtuale classica di hello nel portale di Azure hello. In hello **le connessioni VPN** sezione, se il gateway hello è in esecuzione nella rete virtuale hello, verrà visualizzato hello IP indirizzo del gateway hello. 

![Verificare se il gateway è in esecuzione](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Per le reti virtuali, visitare toohello **Panoramica** pagina della rete virtuale hello. Controllare **i dispositivi connessi** per gateway di rete virtuale hello.

![Controllo dispositivo connesso hello](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Prima di poter rimuovere gateway hello, rimuovere innanzitutto qualsiasi **connessione** oggetti nel gateway hello. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>Verificare se un gateway applicazione è in esecuzione nella rete virtuale hello

Passare toohello **Panoramica** pagina della rete virtuale hello. Controllare hello **i dispositivi connessi** per il gateway applicazione hello.

![Controllo dispositivo connesso hello](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

Se è presente un gateway applicazione, è necessario rimuovere prima di poter eliminare la rete virtuale hello.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Controllare se il servizio di dominio Azure Active Directory è abilitato nella rete virtuale hello

Se hello servizi di dominio Active Directory è abilitata e connessa toohello rete virtuale, è possibile eliminare questa rete virtuale. 

![Controllo dispositivo connesso hello](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable hello servizio, seguire questi passaggi:

1. Passare toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nel riquadro sinistro hello selezionare **Active Directory**.
3. Selezionare la directory di Azure Active Directory (Azure AD) hello con Active Directory Domain Services abilitato.
4. Seleziona hello **configura** scheda.
5. In **servizi di dominio**, modificare hello **Abilita servizi di dominio per questa directory** opzione troppo**n**.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Controllare se la rete virtuale hello è connesso tooother risorse

Controllare i collegamenti del circuito, le connessioni e i peering di rete virtuale, Uno di questi può causare un toofail l'eliminazione di rete virtuale. 

Hello ordine consigliata l'eliminazione è come segue:

1. Connessioni del gateway
2. Gateway
3. Indirizzi IP
4. Peering di rete virtuale
5. Ambiente del servizio app

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Controllare se una macchina virtuale è ancora in esecuzione nella rete virtuale hello

Assicurarsi che nessuna macchina virtuale sia nella rete virtuale hello.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Controllare se la rete virtuale hello è bloccata nella migrazione

Se la rete virtuale hello è bloccata in uno stato di migrazione, non può essere eliminata. Esecuzione della migrazione hello tooabort comando hello e quindi eliminare la rete virtuale di hello.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>Passaggi successivi

- [Rete virtuale di Azure](virtual-networks-overview.md)
- [Domande frequenti sulla rete virtuale di Azure](virtual-networks-faq.md)