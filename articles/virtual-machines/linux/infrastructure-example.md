---
title: procedura dettagliata dell'infrastruttura di Azure aaaExample | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la distribuzione di un'infrastruttura di esempio in Azure.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a>Procedura dettagliata per un'infrastruttura di esempio di Azure per macchine virtuali Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Questo articolo illustra le modalità di compilazione di un'infrastruttura di applicazione di esempio. Si illustra in dettaglio la progettazione di un'infrastruttura per un negozio online semplice che raggruppa tutte le linee guida hello e decisioni sulla convenzioni di denominazione, i set di disponibilità, le reti virtuali e servizi di bilanciamento del carico e riguarda la distribuzione delle macchine virtuali (VM).

## <a name="example-workload"></a>Carico di lavoro di esempio
Adventure Works Cycles desidera toobuild un'applicazione di negozio online in Azure che è costituito da:

* Due server nginx esegue hello client front-end in un livello web
* Due server nginx che elaborano i dati e gli ordini in un livello applicazione
* Due server MongoDB che fanno parte di un cluster partizionato per l'archiviazione dei dati sui prodotti e degli ordini in un livello di database
* Due controller di dominio di Active Directory per gli account dei clienti e dei fornitori in un livello di autenticazione
* Tutti i server hello si trovano in due subnet:
  * una subnet front-end per i server web hello 
  * una subnet di back-end per i server applicazioni hello, MongoDB cluster e i controller di dominio

![Diagramma dei diversi livelli di infrastruttura dell'applicazione](./media/infrastructure-example/example-tiers.png)

In ingresso sicuro il traffico web deve essere con carico bilanciato tra i server web hello negozio online hello per esaminare i clienti. Ordine di elaborazione del traffico nel modulo hello HTTP richiesta dal web hello server devono essere con bilanciamento del carico tra i server applicazione hello. Inoltre, l'infrastruttura hello deve essere progettata per la disponibilità elevata.

progettazione di Hello risultante deve includere:

* Una sottoscrizione e un account di Azure
* Un unico gruppo di risorse
* Azure Managed Disks
* Una rete virtuale con due subnet
* Set di disponibilità per hello macchine virtuali con un ruolo simile
* Macchine virtuali

Hello tutti precedente queste convenzioni di denominazione:

* Adventure Works Cycles usa come prefisso **[carico di lavoro IT]-[località]-[risorsa di Azure]**
  * Per questo esempio, "**azos**" (archivio online di Azure) è hello il nome del carico di lavoro IT e "**utilizzare**" (Stati Uniti orientali 2) è il percorso di hello
* Le reti virtuali usano AZOS-USE-VN**[numero]**
* I set di disponibilità usano azos-use-as-**[ruolo]**
* I nomi delle macchine virtuali usano azos-use-vm-**[nomevm]**

## <a name="azure-subscriptions-and-accounts"></a>Sottoscrizioni e account di Azure
Adventure Works Cycles è tramite la sottoscrizione dell'organizzazione, denominata Adventure Works Enterprise sottoscrizione, tooprovide fatturazione per il carico di lavoro IT.

## <a name="storage"></a>Archiviazione
Adventure Works Cycles ha determinato che è necessario usare Managed Disks di Azure. Durante la creazione di macchine virtuali, vengono usati entrambi i livelli di archiviazione disponibili:

* **Archiviazione standard** per server web hello, server applicazioni e i controller di dominio e i relativi dischi dati.
* **Archiviazione Premium** per i server di cluster partizionati MongoDB hello e dei dischi dati.

## <a name="virtual-network-and-subnets"></a>Rete virtuale e subnet
Poiché la rete virtuale hello non necessita di rete locale di connettività in corso toohello Adventure lavoro cicli, essi deciso in una rete virtuale solo cloud.

Una rete virtuale solo cloud sono creati con hello seguendo le impostazioni utilizzando hello portale di Azure:

* Nome: AZOS-USE-VN01
* Sede: Stati Uniti orientali 2
* Spazio degli indirizzi della rete virtuale: 10.0.0.0/8
* Prima subnet:
  * Nome: FrontEnd
  * Spazio degli indirizzi: 10.0.1.0/24
* Seconda subnet:
  * Nome: BackEnd
  * Spazio degli indirizzi: 10.0.2.0/24

## <a name="availability-sets"></a>Set di disponibilità
disponibilità elevata di toomaintain di tutti i quattro livelli di relativo archivio online, Adventure Works Cycles decidere su quattro set di disponibilità:

* **Utilizzare azos come web** per i server web hello
* **Utilizzare azos come app** per i server applicazioni hello
* **Utilizzare azos come db** per i server hello cluster partizionati di hello MongoDB
* **azos utilizzare come controller di dominio** hello ai controller di dominio

## <a name="virtual-machines"></a>Macchine virtuali
Adventure Works Cycles scelto hello seguenti nomi per le proprie macchine virtuali di Azure:

* **azos-utilizzo-vm-web01** per il server web prima di hello
* **azos-utilizzo-vm-web02** per server web secondo hello
* **azos-utilizzo-vm-il server app01** per il primo server di applicazione hello
* **azos-utilizzo-vm-app02** per il server applicazioni secondo hello
* **azos-utilizzo-vm-db01** per hello prima MongoDB server hello cluster
* **azos-utilizzo-vm-db02** per hello secondo MongoDB server in cluster hello
* **azos-utilizzo-vm-dc01** per il primo controller di dominio hello
* **azos-utilizzo-vm-dc02** per il secondo controller di dominio hello

Di seguito è riportata la configurazione risultante hello.

![Infrastruttura dell'applicazione finale distribuita in Azure](./media/infrastructure-example/example-config.png)

Questa configurazione include:

* Una rete virtuale solo cloud con due subnet (front-end e back-end)
* Managed Disks di Azure con dischi Standard e Premium
* Quattro set di disponibilità, uno per ogni livello di negozio online hello
* macchine virtuali Hello per i livelli di hello quattro
* Un set esterno con carico bilanciato per il traffico web basato su HTTPS dai server web di hello Internet toohello
* Set per il traffico web crittografato dal server di applicazioni toohello hello web server con un interno carico bilanciato
* Un unico gruppo di risorse
