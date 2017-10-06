---
title: un firewall applicazione web nel Centro protezione Azure aaaAdd | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello indicazioni Centro sicurezza di Azure * * aggiungere una web application firewall * * e * * finalizzare protezione applicazione * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Aggiungere un Web application firewall al Centro sicurezza di Azure
Centro sicurezza di Azure potrebbe è consigliabile aggiungere un firewall applicazione web (WAF) da un toosecure partner Microsoft di applicazioni web. Questo documento viene illustrato un esempio di come tooapply questa raccomandazione.

Viene visualizzata una raccomandazione WAF per qualsiasi IP pubblico (IP a livello di istanza o IP con carico bilanciato) cui è associato un gruppo di sicurezza di rete con porte Web in ingresso aperte (80, 443).

Centro sicurezza PC consiglia che si provisioning un toohelp WAF difendersi da attacchi di applicazioni web nelle macchine virtuali e sull'ambiente di servizio App di destinazione. Un Ambiente del servizio app è un'opzione del piano di servizio [Premium](https://azure.microsoft.com/pricing/details/app-service/) del Servizio app di Azure che offre un ambiente completamente isolato e dedicato per eseguire in modo sicuro tutte le app del servizio. toolearn ulteriori informazioni su ASE, vedere hello [documentazione dell'ambiente del servizio App](../app-service/app-service-app-service-environments-readme.md).

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questo argomento non costituisce una guida dettagliata.
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello
1. In hello **indicazioni** pannello seleziona **proteggere l'applicazione web tramite firewall applicazione web**.
   ![Proteggere l'applicazione Web][1]
2. In hello **proteggere le applicazioni web tramite firewall applicazione web** pannello selezionare un'applicazione web. Hello **aggiungere una Web Application Firewall** apre blade.
   ![Aggiungere un Web Application Firewall][2]
3. È possibile scegliere toouse un firewall applicazione web esistente se è disponibile oppure è possibile crearne uno nuovo. In questo esempio non sono disponibili WAF esistenti ed è pertanto necessario creare un WAF.
4. toocreate un WAF, selezionare una soluzione hello elenco dei partner integrato. In questo esempio viene selezionato **Barracuda Web Application Firewall**.
5. Hello **Barracuda Web Application Firewall** pannello apre fornire informazioni sulla soluzione partner hello. Selezionare **crea** nel pannello informazioni hello.

   ![Pannello di informazioni sul firewall][3]

6. Hello **nuova Web Application Firewall** pannello viene aperto, in cui è possibile eseguire **configurazione della macchina virtuale** i passaggi e fornire **WAF informazioni**. Selezionare **Configurazione macchina virtuale**.
7. In hello **configurazione della macchina virtuale** pannello, immettere le informazioni necessarie toospin hello della macchina virtuale che esegue hello WAF.
   ![VM configuration][4]
8. Restituire toohello **nuova Web Application Firewall** pannello e selezionare **WAF informazioni**. In hello **WAF informazioni** pannello configuri WAF hello stesso. Passaggio 7 consente di macchina virtuale di hello tooconfigure su quali hello WAF viene eseguito e il passaggio 8 consente hello tooprovision WAF stesso.

## <a name="finalize-application-protection"></a>Finalizza la protezione dell'applicazione
1. Restituire toohello **indicazioni** blade. È stata generata una nuova voce dopo creato WAF hello, chiamato **Finalizza la protezione di applicazione**. Questa voce indica che è necessario che il processo di hello toocomplete di collegare effettivamente i hello WAF all'interno di hello rete virtuale di Azure in modo che consente di proteggere un'applicazione hello.

   ![Finalizza la protezione dell'applicazione][5]

2. Selezionare **Finalizza la protezione dell'applicazione**. Viene visualizzato un nuovo pannello. Si noterà che è un'applicazione web che deve toohave il traffico reindirizzato.
3. Selezionare un'applicazione web hello. Verrà visualizzata una blade che offre i passaggi per la finalizzazione del programma di installazione di hello web application firewall. Completare i passaggi di hello e quindi selezionare **limitare il traffico**. Centro sicurezza PC quindi hello cablaggio remota per l'utente.

   ![Limita il traffico][6]

> [!NOTE]
> È possibile proteggere nel Centro protezione di più applicazioni web tramite l'aggiunta di queste applicazioni tooyour WAF le distribuzioni esistenti.
>
>

log Hello da tale WAF ora sono completamente integrati. Centro sicurezza PC è possibile avviare automaticamente la raccolta e analisi dei log hello in modo che, può verificarsi tooyou gli avvisi di sicurezza importante.

## <a name="next-steps"></a>Passaggi successivi
Questo documento ha illustrato come tooimplement hello raccomandazione Centro sicurezza PC "Aggiungi un'applicazione web". toolearn ulteriori informazioni sul firewall applicazione web, vedere l'esempio hello:

* [Configurazione di un Web application firewall (WAF) per l'ambiente del servizio app](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
