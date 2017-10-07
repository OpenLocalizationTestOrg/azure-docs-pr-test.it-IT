---
title: "problemi di connettività aaaTroubleshooting tra macchine virtuali di Azure | Documenti Microsoft"
description: "Informazioni su come tooTroubleshoot hello problemi di connettività tra macchine virtuali di Azure."
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
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Risoluzione dei problemi di connettività tra macchine virtuali di Azure

Si potrebbero riscontrare problemi di connettività tra macchine virtuali di Azure. Questo articolo fornisce la risoluzione dei problemi toohelp passaggi risolvere il problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Sintomo

Una macchina virtuale di Azure non può connettersi tooanother macchina virtuale di Azure.

## <a name="troubleshooting-guidance"></a>Guida alla risoluzione dei problemi 

1. [Controllare se NIC non è configurato correttamente](#step-1-check-if-nic-is-misconfigured)
2. [Verificare se il traffico di rete è bloccato da NSG o UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Verificare se il traffico di rete è bloccato dal firewall della macchina virtuale](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Controllare se VM app o un servizio è in attesa sulla porta hello](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Controllare se il problema di hello è causato da SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Verifica se il traffico viene bloccato per gli elenchi ACL per hello VM classico](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Controllare se viene creato endpoint hello per hello VM classico](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Condivisione di rete VM non è possibile tooconnect tooa](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Connettività tra reti tra reti virtuali](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi

Seguire questi problema hello tootroubleshoot di passaggi. Controllare se il problema di hello è risolto dopo ogni passaggio. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Passaggio 1: Verificare se NIC non è configurato correttamente

Seguire [come tooreset interfaccia di rete per la macchina virtuale Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Se il problema di hello si verifica dopo aver modificato l'interfaccia di rete (NIC) hello, seguire questi passaggi:

**Macchine virtuali multi-NIC**

1. Aggiungere un NIC.
2. Risolvere i problemi di hello nelle hello errato NIC o rimuovere errato scheda di rete.  Quindi readd hello scheda di rete.

Per ulteriori informazioni, vedere [tooor interfacce di rete Aggiungi rimuovere dalle macchine virtuali](virtual-network-network-interface-vm.md).

**Macchina virtuale con una sola scheda di rete** 

- [Ridistribuire una VM Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Ridistribuire una VM Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Passaggio 2: Verificare se il traffico di rete è bloccato da NSG o UDR

Utilizzare [del flusso di rete IP Watcher verificare](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG flusso registrazione](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se è presente un gruppo di sicurezza di rete o di una Route definite dall'utente che interferisce con il flusso del traffico.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Passaggio 3: Verificare se il traffico di rete è bloccato dal firewall della macchina virtuale

Disattivare il firewall hello e quindi il risultato di hello del test. Se viene risolto il problema di hello, convalidare le impostazioni di hello firewall hello e abilitare di nuovo.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>Passaggio 4: Controllare se VM app o un servizio è in attesa sulla porta hello

È possibile utilizzare uno dei seguenti metodi toocheck se l'applicazione della macchina virtuale o il servizio è in ascolto sulla porta hello hello

- Eseguire hello seguenti comandi toocheck se hello server è in ascolto su tale porta.

**VM Windows**

    netstat –ano

**VM Linux**

    netstat -l

- Eseguire hello **Telnet** comando hello porta hello tootest tooitself di macchina virtuale. Se hello test non riesce, applicazione o il servizio non è configurato toolisten sulla porta hello.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>Passaggio 5: Verificare se il problema di hello è causato da SNAT

In alcuni scenari, hello VM è posizionato dietro una soluzione di bilanciamento di carico che presenta una dipendenza sulle risorse all'esterno di Azure. In questi scenari, se si verificano problemi di connessione intermittenti, hello problema potrebbe essere causato da [esaurimento delle porte SNAT](../load-balancer/load-balancer-outbound-connections.md). problema hello tooresolve, creare un VIP (o ILPIP per classica) per ogni macchina virtuale di bilanciamento del carico hello e proteggere con ACL o di gruppo. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>Passaggio 6: Verificare se il traffico viene bloccato per gli elenchi ACL per hello classic VM

Un ACL fornisce hello possibilità tooselectively consentire o negare il traffico per un endpoint della macchina virtuale. Per ulteriori informazioni, vedere [Gestisci hello ACL su un endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>Passaggio 7: Verifica se viene creato endpoint hello per hello VM classico

Tutte le macchine virtuali create in Azure utilizzando il modello di distribuzione classica hello possono comunicare automaticamente tramite un canale di rete privata con altre macchine virtuali in hello che stesso servizio o della rete virtuale del cloud. Tuttavia, i computer in altre reti virtuali richiedono endpoint toodirect hello rete in ingresso traffico tooa computer macchina virtuale. Per ulteriori informazioni, vedere [come tooset degli endpoint](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>Passaggio 8: Condivisione di rete VM tooa tooconnect Impossibile

Nel caso di condivisione di rete VM non è possibile tooconnect tooa, problema di hello può essere causato da schede di rete non disponibile in hello macchina virtuale. toodelete hello schede di rete non disponibile, vedere [come toodelete hello schede di rete non disponibile](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Passaggio 9: Connettività di rete virtuale tra

Utilizzare [del flusso di rete IP Watcher verificare](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG flusso registrazione](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se è presente un gruppo di sicurezza di rete o di una Route definite dall'utente che interferisce con il flusso del traffico. È inoltre possibile convalidare la configurazione della rete virtuale tra [qui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.
