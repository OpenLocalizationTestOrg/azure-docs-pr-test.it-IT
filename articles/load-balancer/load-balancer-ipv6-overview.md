---
title: aaaOverview di IPv6 di bilanciamento del carico di Azure | Documenti Microsoft
description: Informazioni sul supporto IPv6 per Azure Load Balancer e le macchine virtuali con bilanciamento del carico.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: ipv6, azure load balancer, dual stack, ip pubblico, ipv6 nativo, mobili, iot
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Panoramica di IPv6 per Azure Load Balancer

I servizi di bilanciamento del carico con connessione Internet possono essere distribuiti con un indirizzo IPv6. Inoltre la connettività tooIPv4, in questo modo hello seguenti funzionalità:

* End-to-end la connettività IPv6 nativa tra client Internet pubblica e macchine virtuali di Azure (VM) tramite bilanciamento del carico hello.
* Connettività IPv6 nativa end-to-end in uscita tra macchine virtuali e client Internet pubblici abilitati per IPv6.

Hello seguente immagine illustra il funzionamento di IPv6 hello di bilanciamento del carico di Azure.

![Azure Load Balancer con IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

Una volta distribuito, un client di IPv4 o IPv6 abilitato Internet può comunicare con hello pubblica indirizzi IPv4 o IPv6 o nomi host di hello bilanciamento del carico con connessione Internet di Azure. le route del servizio di bilanciamento carico di Hello hello IPv6 pacchetti toohello IPv6 indirizzi privati di macchine virtuali hello utilizzando il servizio NAT (Network address translation). client Internet IPv6 Hello non possono comunicare direttamente con hello indirizzo IPv6 di hello macchine virtuali.

## <a name="features"></a>Funzionalità

Il supporto IPv6 nativo per le macchine virtuali distribuite tramite Azure Resource Manager offre:

1. Servizi di IPv6 con bilanciamento del carico per i client hello Internet IPv6
2. Endpoint IPv6 e IPv4 nativi nelle macchine virtuali ("dual stack")
3. Connessioni IPv6 native in ingresso e in uscita
4. I protocolli supportati, ad esempio TCP, UDP e HTTP(S), consentono un'ampia gamma di architetture di servizi

## <a name="benefits"></a>Vantaggi

Questa funzionalità consente hello seguenti vantaggi chiave:

* Soddisfare normative che richiedono che le nuove applicazioni sia accessibile ai client solo tooIPv6
* Abilita mobile e Internet delle cose (IOT) agli sviluppatori toouse in pila dual macchine virtuali di Azure (IPv4 più IPv6) tooaddress hello mobile crescente & IOT mercati

## <a name="details-and-limitations"></a>Dettagli e limitazioni

Dettagli

* Hello servizio DNS di Azure contiene i record di nome sia IPv4 e IPv6 AAAA e risponde con entrambi i record di bilanciamento del carico hello. client Hello sceglie quale toocommunicate indirizzo (IPv4 o IPv6) con.
* Quando una macchina virtuale viene avviata una connessione tooa pubblica Internet IPv6 connesso, l'indirizzo IPv6 di origine della macchina virtuale di hello è convertito di indirizzo di rete (NAT) toohello indirizzo IPv6 pubblico del servizio di bilanciamento del carico hello.
* Macchine virtuali che eseguono Linux hello del sistema operativo devono essere tooreceive configurato un indirizzo IP IPv6 tramite DHCP. Molte delle immagini Linux hello hello raccolta Azure sono già configurate toosupport IPv6 senza alcuna modifica. Per altre informazioni, vedere [Configurazione di DHCPv6 per VM Linux](load-balancer-ipv6-for-linux.md)
* Se si sceglie toouse probe di integrità di con il bilanciamento del carico, creare un probe IPv4 e usarlo con hello IPv4 e IPv6 endpoint. Se si arresta il servizio di hello nella VM, hello IPv4 sia IPv6 endpoint provengono dalla rotazione.

Limitazioni

* È possibile aggiungere regole di bilanciamento del carico di IPv6 in hello portale di Azure. le regole di Hello possono essere create solo tramite il modello di hello, CLI, PowerShell.
* Non è possibile aggiornare gli indirizzi IPv6 di toouse macchine virtuali esistenti. È necessario distribuire nuove macchine virtuali.
* Può essere assegnato un solo indirizzo IPv6 tooa singola interfaccia di rete in ogni macchina virtuale.
* Impossibile assegnare gli indirizzi IPv6 pubblici Hello tooa macchina virtuale. Possono solo essere assegnati tooa servizio di bilanciamento del carico.
* È possibile configurare la ricerca DNS inversa hello per gli indirizzi IPv6 pubblici.
* Hello macchine virtuali con indirizzi IPv6 hello non può essere membri di un servizio Cloud di Azure. Possono essere collegati tooan rete virtuale di Azure (VNet) e comunicare tra loro tramite gli indirizzi IPv4.
* Gli indirizzi IPv6 privati possono essere distribuiti nelle singole macchine virtuali di un gruppo di risorse, ma non possono essere distribuiti in un gruppo di risorse tramite set di scalabilità.
* Macchine virtuali di Azure non è possibile connettersi tramite le macchine virtuali tooother IPv6, altri servizi di Azure o i dispositivi locali. Essi possono comunicare solo con bilanciamento del carico di Azure hello su IPv6. Possono tuttavia comunicare con queste altre risorse tramite IPv4.
* La protezione del gruppo di sicurezza di rete (NSG) per IPv4 è supportata nelle distribuzioni dual stack (IPv4 + IPv6). NSGs toohello IPv6 endpoint non sono valide.
* endpoint Hello IPv6 hello macchina virtuale non è esposta direttamente toohello internet. Si trova dietro un servizio di bilanciamento del carico. Solo le porte hello specificate nelle regole di bilanciamento del carico hello sono accessibili tramite IPv6.
* Modifica hello parametro IdleTimeout per IPv6 è **attualmente non supportata**. valore predefinito di Hello è 4 minuti.
* Modifica hello parametro loadDistributionMethod per IPv6 è **attualmente non supportata**.
* Gli indirizzi IP IPv6 riservati (dove IPAllocationMethod = statico) sono **attualmente non supportati**.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toodeploy un bilanciamento del carico con IPv6.

* [Disponibilità di IPv6 per area](https://go.microsoft.com/fwlink/?linkid=828357)
* [Distribuire un servizio di bilanciamento del carico con IPv6 usando un modello](load-balancer-ipv6-internet-template.md)
* [Distribuire un servizio di bilanciamento del carico con IPv6 usando Azure PowerShell](load-balancer-ipv6-internet-ps.md)
* [Distribuire un servizio di bilanciamento del carico con IPv6 usando l'interfaccia della riga di comando di Azure](load-balancer-ipv6-internet-cli.md)
