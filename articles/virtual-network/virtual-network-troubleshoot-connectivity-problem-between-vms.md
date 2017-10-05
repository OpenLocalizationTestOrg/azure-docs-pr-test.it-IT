---
title: "Risoluzione dei problemi di connettività tra macchine virtuali di Azure | Documenti Microsoft"
description: "Informazioni su come risolvere i problemi di connettività tra macchine virtuali di Azure."
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
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Risoluzione dei problemi di connettività tra macchine virtuali di Azure

Si potrebbero riscontrare problemi di connettività tra macchine virtuali di Azure. Questo articolo illustra la procedura per risolvere questo tipo di problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Sintomo

Una macchina virtuale di Azure non è possibile connettersi a un'altra macchina virtuale di Azure.

## <a name="troubleshooting-guidance"></a>Guida alla risoluzione dei problemi 

1. [Controllare se NIC non è configurato correttamente](#step-1-check-if-nic-is-misconfigured)
2. [Verificare se il traffico di rete è bloccato da NSG o UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Verificare se il traffico di rete è bloccato dal firewall della macchina virtuale](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Controllare se un'applicazione o un servizio della macchina virtuale sono in ascolto sulla porta](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Controllare se il problema è causato dall'architettura SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Controllare se il traffico è bloccato da ACL per la macchina virtuale classica](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Controllare che l'endpoint per la macchina virtuale classica sia stato creato](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Impossibile connettersi a una condivisione di rete VM](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Connettività tra reti tra reti virtuali](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi

Seguire questa procedura per risolvere il problema. Controllare se il problema è risolto dopo ogni passaggio. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Passaggio 1: Verificare se NIC non è configurato correttamente

Seguire [come reimpostare l'interfaccia di rete per la macchina virtuale Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Se il problema si verifica dopo aver modificato l'interfaccia di rete, procedere come segue:

**Macchine virtuali multi-NIC**

1. Aggiungere un NIC.
2. Risolvere i problemi nella scheda di rete non valida o rimuovere una scheda di rete non valido.  Readd quindi la scheda NIC.

Per altre informazioni, vedere [Aggiungere o rimuovere interfacce di rete da macchine virtuali](virtual-network-network-interface-vm.md).

**Macchina virtuale con una sola scheda di rete** 

- [Ridistribuire una VM Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Ridistribuire una VM Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Passaggio 2: Verificare se il traffico di rete è bloccato da NSG o UDR

Utilizzare [del flusso di rete IP Watcher verificare](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG flusso registrazione](../network-watcher/network-watcher-nsg-flow-logging-overview.md) per identificare se è presente un gruppo di sicurezza di rete o di una Route definite dall'utente che interferisce con il flusso del traffico.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Passaggio 3: Verificare se il traffico di rete è bloccato dal firewall della macchina virtuale

Disattivare il firewall, quindi testare i risultati. Se il problema viene risolto, verificare le impostazioni del firewall e abilitare di nuovo.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a>Passaggio 4: Controllare se un'applicazione o un servizio della macchina virtuale sono in ascolto sulla porta

È possibile utilizzare uno dei metodi seguenti per controllare se applicazione della macchina virtuale o il servizio è in attesa sulla porta

- Eseguire i comandi seguenti per verificare se il server è in ascolto su quella porta.

**VM Windows**

    netstat –ano

**VM Linux**

    netstat -l

- Eseguire il **Telnet** comando nella macchina virtuale a se stessa per testare la porta. Se il test non riesce, applicazione o il servizio non è configurato per restare in attesa sulla porta.

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a>Passaggio 5: Controllare se il problema è causato dall'architettura SNAT

In alcuni scenari, la macchina virtuale è posizionata dietro una soluzione di bilanciamento di carico che presenta una dipendenza sulle risorse all'esterno di Azure. In questi scenari, eventuali problemi di connessione intermittenti possono essere causati dall'[esaurimento delle porte SNAT](../load-balancer/load-balancer-outbound-connections.md). Per risolvere il problema, creare un indirizzo VIP (o ILPIP per classica) per ogni macchina virtuale che si trova dietro il bilanciamento del carico e protetta con ACL o di gruppo. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a>Passaggio 6: Controllare se il traffico è bloccato da ACL per la macchina virtuale classica

Offre la possibilità di consentire o negare in modo selettivo il traffico per un endpoint di macchina virtuale. Per altre informazioni, vedere [Gestire l'elenco di controllo di accesso su un endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a>Passaggio 7: Controllare che l'endpoint per la macchina virtuale classica sia stato creato

Tutte le macchine virtuali create in Azure utilizzando il modello di distribuzione classica possono comunicare automaticamente tramite un canale di rete privata con altre macchine virtuali nella rete virtuale o nello stesso servizio cloud. Tuttavia, i computer in altre reti virtuali richiedono degli endpoint per indirizzare il traffico di rete in ingresso a una macchina virtuale. Per altre informazioni, vedere [Come configurare gli endpoint](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a>Passaggio 8: Impossibile connettersi a una condivisione di rete VM

Se non si riesce a connettersi a una condivisione di rete VM, il problema può essere causato da schede di rete non disponibile nella macchina virtuale. Per eliminare le schede di interfaccia non disponibili, vedere [Eliminare le schede di interfaccia non disponibili](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Passaggio 9: Connettività di rete virtuale tra

Utilizzare [del flusso di rete IP Watcher verificare](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG flusso registrazione](../network-watcher/network-watcher-nsg-flow-logging-overview.md) per identificare se è presente un gruppo di sicurezza di rete o di una Route definite dall'utente che interferisce con il flusso del traffico. È inoltre possibile convalidare la configurazione della rete virtuale tra [qui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se si necessita ancora di assistenza, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.