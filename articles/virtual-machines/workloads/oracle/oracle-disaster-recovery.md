---
title: aaaOverview di uno scenario di ripristino di emergenza Oracle nell'ambiente Azure | Documenti Microsoft
description: Scenario di ripristino di emergenza per un'istanza di Database Oracle 12c nell'ambiente Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Ripristino di emergenza per un'istanza di Database Oracle 12c in un ambiente Azure

## <a name="assumptions"></a>Presupposti

- Conoscenza degli ambienti Azure e della progettazione di Oracle Data Guard.


## <a name="goals"></a>Obiettivi
- Progettare hello topologia e configurazione che soddisfano i requisiti di ripristino di emergenza di emergenza.

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>Scenario 1: Siti primari e di ripristino di emergenza in Azure

Un cliente ha Oracle database set di backup nel sito primario di hello. Un sito di ripristino di emergenza si trova in un'area diversa. il cliente di Hello utilizza Oracle Data Guard per il ripristino rapido tra questi siti. sito primario di Hello dispone di un database secondario per la creazione di report e altri utilizzi. 

### <a name="topology"></a>Topologia

Di seguito è riportato un riepilogo di hello installazione di Azure:

- Due siti (un sito primario e un sito di ripristino di emergenza)
- Due reti virtuali
- Due database Oracle con Data Guard (primario e standby)
- Due database Oracle con Golden Gate o Data Guard (solo sito primario)
- Due servizi delle applicazioni, uno primario e uno nel sito di ripristino di emergenza hello
- Un *set di disponibilità,* utilizzato per il servizio di database e dell'applicazione nel sito primario di hello
- Uno jumpbox in ogni sito, che limita l'accesso di rete privata toohello e consente solo accesso in ingresso da un amministratore
- Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate
- Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database

![Schermata della pagina di topologia hello ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>Scenario 2: Sito primario locale e sito di ripristino di emergenza in Azure

Il cliente ha una configurazione del database Oracle locale nel sito primario. Il sito di un ripristino di emergenza è in Azure. Oracle Data Guard viene usato per eseguire un ripristino rapido tra questi siti. sito primario di Hello dispone di un database secondario per la creazione di report e altri utilizzi. 

Per questo tipo di configurazione esistono due approcci.

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>Approccio 1: Connessioni dirette tra sedi locali e Azure, che richiedono porte TCP aperte nel firewall hello 

Connessioni dirette non è consigliabile in quanto espongono toohello porte TCP di hello world di fuori.

#### <a name="topology"></a>Topologia

Ecco un riepilogo di hello installazione di Azure:

- Un sito di ripristino di emergenza 
- Una rete virtuale
- Un database Oracle con Data Guard (attivo)
- Servizio di un'applicazione nel sito di ripristino di emergenza hello
- Uno jumpbox, che limita l'accesso di rete privata toohello e consente solo accesso in ingresso da un amministratore
- Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate
- Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database
- Un tooallow/regola dei criteri di gruppo in ingresso porta 1521 (o una porta definita dall'utente)
- Una gruppo/regola dei criteri toorestrict solo hello IP indirizzo o gli indirizzi locali (database o applicazione) tooaccess hello rete virtuale

![Schermata della pagina di topologia hello ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>Approccio 2: VPN da sito a sito
La VPN da sito a sito è un approccio migliore. Per altre informazioni sulla configurazione di una VPN, vedere [Creare una rete virtuale con una connessione VPN da sito a sito usando l'interfaccia della riga di comando](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).

#### <a name="topology"></a>Topologia

Ecco un riepilogo di hello installazione di Azure:

- Un sito di ripristino di emergenza 
- Una rete virtuale 
- Un database Oracle con Data Guard (attivo)
- Servizio di un'applicazione nel sito di ripristino di emergenza hello
- Uno jumpbox, che limita l'accesso di rete privata toohello e consente solo accesso in ingresso da un amministratore
- Un jumpbox, un servizio dell'applicazione, un database e un gateway VPN in subnet separate
- Gruppo di sicurezza di rete applicato nelle subnet dell'applicazione e del database
- Connessione VPN da sito a sito tra rete locale e Azure

![Schermata della pagina di topologia hello ripristino di emergenza](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>Informazioni aggiuntive

- [Progettare e implementare un database Oracle in Azure](oracle-design.md)
- [Configurare Oracle Data Guard](configure-oracle-dataguard.md)
- [Configurare Oracle Golden Gate](configure-oracle-golden-gate.md)
- [Backup e ripristino di Oracle](oracle-backup-recovery.md)


## <a name="next-steps"></a>Passaggi successivi

- [Esercitazione: Creare VM a disponibilità elevata](../../linux/create-cli-complete.md)
- [Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM](../../linux/cli-samples.md)
