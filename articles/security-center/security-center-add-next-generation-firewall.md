---
title: aaaAdd un firewall generazione successivo in Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello indicazioni Centro sicurezza di Azure * * aggiungere una successiva generazione Firewall * * e * * traffico Route tramite NGFW solo * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>Aggiungere un firewall di nuova generazione in Centro sicurezza di Azure
Centro sicurezza di Azure potrebbe è consigliabile aggiungere un firewall generazione successivo (NGFW) da un tooincrease partner Microsoft i meccanismi di protezione. Questo documento viene illustrato un esempio di come toodo questo.

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questa non è una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **aggiunge un Firewall generazione successiva**.
   ![Aggiungi un firewall di nuova generazione][1]
2. In hello **aggiunge un Firewall generazione successiva** pannello, selezionare un endpoint.
   ![Selezionare un endpoint][2]
3. Viene visualizzato un secondo pannello **Aggiungi un firewall di nuova generazione**. È possibile scegliere toouse una soluzione esistente se è disponibile oppure è possibile crearne uno nuovo. In questo esempio non sono disponibili soluzioni esistenti ed è necessario creare un firewall di nuova generazione.
   ![Creare un firewall di nuova generazione][3]
4. toocreate un NGFW, selezionare una soluzione hello elenco dei partner integrato. In questo esempio si selezionerà **Check Point**.
   ![Selezionare un firewall di nuova generazione][4]
5. Hello **Check Point** pannello apre fornire informazioni sulla soluzione partner hello. Selezionare **crea** nel pannello informazioni hello.
   ![Pannello di informazioni sul firewall][5]
6. Hello **crea macchina virtuale** apre blade. Immettere le informazioni necessarie toospin rapidamente una macchina virtuale (VM) che esegue hello NGFW. Seguire i passaggi di hello e fornire informazioni NGFW hello necessarie. Selezionare OK tooapply.
   ![Creare una macchina virtuale toorun NGFW][6]

## <a name="route-traffic-through-ngfw-only"></a>Route traffic through NGFW only (Indirizza il traffico solo tramite il firewall di nuova generazione)
Restituire toohello **indicazioni** blade. Dopo l'aggiunta di un firewall di nuova generazione tramite il Centro sicurezza, è stata generata la nuova voce **Indirizza il traffico solo tramite il firewall di nuova generazione**. Questa raccomandazione viene creata solo se il firewall di nuova generazione è installato tramite il Centro sicurezza PC. Se si dispone di endpoint con connessione Internet, il Centro sicurezza PC consiglia di configurare regole di gruppo di sicurezza di rete che impongono il traffico in entrata tooyour VM tramite il NGFW.

1. In hello **pannello indicazioni**selezionare **indirizzare il traffico attraverso NGFW solo**.
   ![Indirizza il traffico solo tramite il firewall di nuova generazione][7]
2. Verrà aperto il pannello hello **indirizzare il traffico attraverso NGFW solo**, in cui sono elencate le macchine virtuali che è possibile indirizzare il traffico. Selezionare una macchina virtuale dall'elenco di hello.
   ![Selezionare una macchina virtuale][8]
3. Un pannello per hello selezionata verrà visualizzata la macchina virtuale, la visualizzazione delle regole in entrata correlate. Una descrizione fornisce altre informazioni sui possibili passaggi successivi. Selezionare **modificare le regole in entrata** tooproceed con la modifica di una regola in ingresso. Hello aspettativa è che **origine** non è stato impostato troppo**qualsiasi** per gli endpoint con connessione Internet hello collegato con hello NGFW. vedere toolearn più sulle proprietà hello della regola in ingresso di hello [regole NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).
   ![Configurare l'accesso toolimit regole][9]
   ![modifica la regola in ingresso][10]

## <a name="see-also"></a>Vedere anche
Questo documento ha illustrato come tooimplement hello raccomandazione Centro sicurezza PC "Aggiungi un Firewall generazione successivo." toolearn ulteriori informazioni su NGFWs e hello soluzione partner punto di controllo, vedere hello informazioni seguenti:

* [Firewall di nuova generazione](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [Check Point vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure criteri di sicurezza.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
