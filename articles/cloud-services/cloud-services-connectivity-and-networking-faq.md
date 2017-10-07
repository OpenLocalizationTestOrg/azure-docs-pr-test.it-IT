---
title: problemi di rete e aaaConnectivity per domande frequenti sui servizi Cloud di Microsoft Azure | Documenti Microsoft
description: "Questo articolo vengono elencati hello domande frequenti sulla connettività e rete per servizi Cloud di Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemi di connettività e rete per Servizi cloud di Azure: domande frequenti

Questo articolo include le domande frequenti relative ai problemi di connettività e rete per [Servizi cloud di Microsoft Azure](https://azure.microsoft.com/services/cloud-services). È anche possibile consultare hello [pagina dimensione di macchina virtuale di servizi Cloud](cloud-services-sizes-specs.md) per informazioni sulle dimensioni.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Non è possibile riservare un indirizzo IP in un servizio cloud con più indirizzi VIP
Innanzitutto, assicurarsi che tale istanza di macchina virtuale hello che si sta tentando di IP hello tooreserve per sia attivata. In secondo luogo, verificare che si sta utilizzando indirizzi IP riservati per entrambi hello le distribuzioni di gestione temporanea e produzione. **Non** modificare le impostazioni di hello durante l'aggiornamento di distribuzione hello.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Come si usa Desktop remoto quando si ha un gruppo di sicurezza di rete?
Aggiungere regole toohello NSG che consentano il traffico sulle porte **3389** e **20000**.  Desktop remoto usa la porta **3389**.  Le istanze del servizio cloud sono con carico bilanciato, pertanto non è possibile controllare direttamente quale tooconnect istanza di.  Hello *RemoteForwarder* e *RemoteAccess* gli agenti di gestire il traffico RDP e consentire hello client toosend un cookie RDP e specificare tooconnect una singola istanza di.  Hello *RemoteForwarder* e *RemoteAccess* agenti richiedono tale porta **20000** aperto, che può essere bloccato se si dispone di un gruppo.

## <a name="can-i-ping-a-cloud-service"></a>È possibile eseguire il ping di un servizio cloud?

No, non tramite il normale hello "ping" / protocollo ICMP. Hello protocollo ICMP non è consentito tramite bilanciamento del carico di Azure hello.

tootest connettività, è consigliabile eseguire un ping di porta. Mentre Ping.exe utilizza ICMP, altri strumenti, ad esempio PSPing Nmap e telnet consentono tootest connettività tooa specifica la porta TCP.

Per ulteriori informazioni, vedere [utilizzare Ping porta anziché ICMP tootest connettività macchina virtuale di Azure](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>Come impedire la ricezione migliaia di accessi da indirizzi IP sconosciuti che indicano una qualche forma di attacco dannoso toohello servizio cloud?
Azure implementa un tooprotect di sicurezza di rete su più livelli relativo servizi della piattaforma dagli attacchi distributed denial of service (DDoS). Hello sistema difesa DDoS Azure fa parte di Continua processo di monitoraggio Azure, che viene costantemente migliorato tramite il test di penetrazione. È progettato questo sistema di difesa DDoS toowithstand attacchi non solo da hello esterno ma anche da altri tenant di Azure. Per altre informazioni, vedere [Microsoft Azure Network Security](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf) (Sicurezza di rete di Microsoft Azure).

È anche possibile creare un blocco di avvio attività tooselectively alcuni indirizzi IP specifici. Per altre informazioni, vedere [Bloccare un indirizzo IP specifico](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Quando si tenta di tooRDP toomy l'istanza del servizio cloud, viene visualizzato il messaggio hello, "account utente di hello è scaduto."
È possibile ricevere il messaggio di errore hello "questo account utente scaduta" quando si ignora una data di scadenza hello configurato nelle impostazioni di RDP. È possibile modificare la data di scadenza hello dal portale hello attenendosi alla procedura seguente:
1. Accedi toohello Console di gestione di Azure (https://manage.windowsazure.com), passare servizio cloud tooyour e selezionare hello **configura** scheda.
2. Selezionare **Remoto**.
3. Modificare hello "scade" Data e quindi salvare la configurazione hello.

È ora deve essere in grado di tooRDP tooyour macchina.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Perché LoadBalancer non bilancia il carico del traffico in modo uniforme?
Per informazioni sul funzionamento del servizio di bilanciamento del carico interno, vedere [Azure Load Balancer new distribution mode](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/) (Nuova modalità di distribuzione di Azure Load Balancer).

algoritmo di distribuzione Hello usato è una tupla con 5 (origine IP, porta di origine, IP di destinazione, la porta di destinazione, tipo di protocollo) Server tooavailable di traffico toomap hash. La persistenza viene mantenuta solo all'interno di una sessione di trasporto. I pacchetti hello sarà stessa sessione TCP o UDP indirizzate toohello istanza stesso Data Center IP (DIP) dietro l'endpoint con carico bilanciato hello. Quando il client di hello chiude e riapre la connessione hello o avvia una nuova sessione da hello stesso indirizzo IP di origine, la porta di origine hello viene modificata e provoca hello traffico toogo tooa DIP endpoint diversi.
