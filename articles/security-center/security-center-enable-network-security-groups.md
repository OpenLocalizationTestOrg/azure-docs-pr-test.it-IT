---
title: Gruppi di sicurezza di rete nel Centro protezione Azure aaaEnable | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * abilitare rete sicurezza gruppi * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Abilitare i gruppi di sicurezza di rete nel Centro sicurezza di Azure
Se non è già disponibile, il Centro sicurezza di Azure consiglia l'abilitazione di un gruppo di sicurezza di rete. NSGs contiene un elenco di regole di elenco di controllo di accesso (ACL) che consentono o negano il traffico di rete tooyour istanze di macchina virtuale in una rete virtuale. I gruppi di sicurezza di rete possono essere associati a subnet o singole istanze VM in una subnet. Quando un gruppo è associata a una subnet, regole ACL hello si applicano le istanze VM hello tooall nella subnet. Inoltre, il traffico tooan singole macchine Virtuali è possibile limitare ulteriormente l'associazione di un gruppo direttamente toothat macchina virtuale. vedere più toolearn [che cos'è un gruppo di sicurezza di rete (gruppo)?](../virtual-network/virtual-networks-nsg.md)

Se non si dispone di NSGs abilitata, il Centro sicurezza PC presenta due indicazioni tooyou: abilitare dei gruppi di sicurezza di rete su subnet e attivare dei gruppi di sicurezza di rete nelle macchine virtuali. Si sceglie il livello, subnet o macchina virtuale, tooapply NSGs.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questa non è una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **abilitare gruppi di sicurezza di rete** in subnet o su macchine virtuali.
   ![Abilitare i gruppi di sicurezza di rete][1]
2. Verrà aperto il pannello hello **configurare gruppi di sicurezza rete mancante** per le subnet o per le macchine virtuali, a seconda della raccomandazione hello selezionato. Selezionare una subnet o tooconfigure una macchina virtuale un gruppo in.

   ![Configurare i gruppi di sicurezza di rete per la subnet][2]

   ![Configurare i gruppi di sicurezza di rete per le macchine virtuali][3]
3. In hello **scegliere gruppo di sicurezza di rete** pannello selezionare un gruppo esistente oppure **Crea nuovo** toocreate un gruppo.

   ![Scegli un gruppo di sicurezza di rete][4]

Se si crea un gruppo, seguire i passaggi di hello in [come NSGs toomanage utilizzando hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate un gruppo e impostare le regole di sicurezza.

## <a name="see-also"></a>Vedere anche
In questo articolo ha illustrato come tooimplement hello Centro sicurezza PC indicazione "abilitare gruppi di sicurezza rete" per le macchine virtuali o subnet. toolearn ulteriori informazioni su attivazione NSGs, vedere l'esempio hello:

* [Che cos'è un gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)
* [Come NSGs toomanage utilizzando hello portale di Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) -ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
