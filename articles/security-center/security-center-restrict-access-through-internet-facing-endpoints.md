---
title: accesso aaaRestrict tramite gli endpoint con connessione Internet nel Centro sicurezza di Azure | Documenti Microsoft
description: "Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * limitare l'accesso tramite endpoint * * è connessa a Internet."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Limitare l'accesso tramite endpoint con connessione Internet in Centro sicurezza di Azure
Il Centro sicurezza di Azure consiglia di limitare l'accesso tramite endpoint con connessione Internet se uno dei gruppi di sicurezza di rete contiene una o più regole in ingresso che consentono l'accesso da "qualsiasi" indirizzo IP di origine. Apertura accesso troppo "any" può attivare gli utenti malintenzionati tooaccess le risorse. Centro sicurezza PC verrà consiglia di modificare queste regole in entrata toorestrict accesso toosource indirizzi IP che effettivamente richiedono l'accesso.

Questa raccomandazione viene generata per qualsiasi porta Web con "any" come origine.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione. Questa non è una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **pannello indicazioni**selezionare **limitare l'accesso tramite endpoint per Internet**.

   ![Restrict access through Internet facing endpoint (Limita accesso tramite endpoint con connessione Internet)][1]
2. Verrà aperto il pannello hello **limitare l'accesso tramite endpoint per Internet**. Questo pannello elenca hello le macchine virtuali (VM) con le regole in entrata che creano un potenziale problema di sicurezza. Selezionare una macchina virtuale.

   ![Selezionare una macchina virtuale][2]
3. Hello **NSG** pannello Visualizza le informazioni di gruppo di sicurezza di rete, le regole in entrata correlate, e hello associati macchina virtuale. Selezionare **modificare le regole in entrata** tooproceed con la modifica di una regola in ingresso.

   ![Pannello Gruppo di sicurezza di rete][3]
4. In hello **sicurezza regole connessioni in entrata** pannello selezionare hello tooedit regola in ingresso. In questo esempio selezioniamo **Consenti Web**.

   ![Regole di sicurezza in ingresso][4]

   Si noti che è anche possibile selezionare **regole predefinite** set hello toosee di regole predefinite contenute NSGs tutti. non è possibile eliminare le regole predefinite di Hello ma, poiché vengono assegnati una priorità più bassa, possono essere sostituite dalle regole di hello creati. Altre informazioni sulle [regole predefinite](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Regole predefinite][5]
5. In hello **AllowWeb** pannello hello di modificare le proprietà della regola in ingresso di hello in modo che hello **origine** è un indirizzo IP o un blocco di indirizzi IP. vedere toolearn più sulle proprietà hello della regola in ingresso di hello [regole NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Modificare la regola in ingresso][6]

## <a name="see-also"></a>Vedere anche
In questo articolo ha illustrato come tooimplement hello Centro sicurezza PC indicazione "limitare l'accesso tramite endpoint per Internet." toolearn ulteriori informazioni su attivazione NSGs e regole, vedere l'esempio hello:

* [Che cos'è un gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)
* [Come NSGs toomanage utilizzando hello portale di Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md)-informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md)-informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md)-informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md)-domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/)-ottenere informazioni e notizie sicurezza di Azure hello.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
