---
title: supporto di gestione risorse di bilanciamento del carico aaaAzure | Documenti Microsoft
description: Usare PowerShell per il bilanciamento del carico con Azure Resource Manager. Uso di modelli per il bilanciamento del carico
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Usare il supporto di Azure Resource Manager per Azure Load Balancer

Gestione risorse di Azure è il framework di gestione Preferiti hello per servizi di Azure. È ora possibile gestire Azure Load Balancer con API e strumenti basati su Azure Resource Manager.

## <a name="concepts"></a>Concetti

Gestione risorse di bilanciamento del carico di Azure contiene hello risorse figlio seguenti:

* Configurazione IP front-end: un bilanciamento del carico può includere uno o più indirizzi IP front-end, anche noti come IP virtuali (indirizzi VIP). In ingresso per il traffico hello fungono da questi indirizzi IP.
* Pool di indirizzi di back-end: questi sono gli indirizzi IP associati alla macchina virtuale hello scheda interfaccia di rete (NIC) toowhich carico verrà distribuito.
* Regole di bilanciamento del carico: una proprietà della regola esegue il mapping di un indirizzo IP front-end specificato e porta set tooa combinazione di indirizzi IP back-end e combinazione di porta. Un bilanciamento del carico singolo può avere più regole di bilanciamento del carico. Ogni regola è una combinazione di un IP e una porta front-end e un IP e una porta back-end associata alle VM.
* Probe – probe abilitare si tookeep traccia dello stato di hello di istanze di macchina virtuale. Se un probe di integrità non riesce, istanza di macchina virtuale hello verrà eseguita automaticamente dalla rotazione.
* Le regole NAT in ingresso: hello di regole NAT che definiscono il traffico in ingresso che passano attraverso IP front-end hello e distribuita toohello nuovamente IP finale.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Modelli di Guida introduttiva

Gestione risorse di Azure consente tooprovision delle applicazioni utilizzando un modello dichiarativo. In un unico modello, è possibile distribuire più servizi con le relative dipendenze. Utilizzare hello stesso modello toorepeatedly distribuire l'applicazione durante ogni fase del ciclo di vita dell'applicazione hello.

I modelli possono includere definizioni per macchine virtuali, reti virtuali, set di disponibilità, interfacce di rete, account di archiviazione, bilanciamenti del carico, gruppi di sicurezza di rete e IP pubblici. Con i modelli è possibile creare tutto il necessario per un'applicazione complessa. file di modello Hello possa essere verificato nel sistema di gestione dei contenuti per il controllo della versione e la collaborazione.

[Altre informazioni sui modelli](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Altre informazioni sulle risorse di rete](../virtual-network/resource-groups-networking.md)

I modelli di avvio rapido che usano Azure Load Balancer sono disponibili in un [repository GitHub](https://github.com/Azure/azure-quickstart-templates) che ospita un set di modelli generati dalla community.

Esempi di modelli:

* [2 macchine virtuali in un bilanciamento del carico e regole di bilanciamento del carico](http://go.microsoft.com/fwlink/?LinkId=544799)
* [2 macchine virtuali in una rete virtuale con un bilanciamento del carico interno e regole di bilanciamento del carico](http://go.microsoft.com/fwlink/?LinkId=544800)
* [2 macchine virtuali in un bilanciamento del carico e configurare le regole NAT in hello LB](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Configurazione del bilanciamento del carico di Azure con PowerShell o l'interfaccia della riga di comando

Introduzione ai cmdlet, agli strumenti da riga di comando e alle API REST di Azure Resource Manager

* [Cmdlet di servizi di rete di Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) può essere utilizzato toocreate un bilanciamento del carico.
* [Come toocreate un bilanciamento del carico con Gestione risorse di Azure](load-balancer-get-started-ilb-arm-ps.md)
* [Utilizzo di hello CLI di Azure con Gestione risorse di Azure](../xplat-cli-azure-resource-manager.md)
* [API REST di bilanciamento del carico](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Passaggi successivi

È anche possibile [iniziare a creare un bilanciamento del carico con connessione Internet](load-balancer-get-started-internet-arm-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento specifico del traffico di rete per il bilanciamento del carico.

Informazioni su come toomanage [impostazioni di timeout TCP per un servizio di bilanciamento del carico di inattività](load-balancer-tcp-idle-timeout.md). Questo è importante quando l'applicazione necessita di connessioni tookeep alive per i server di bilanciamento del carico.
