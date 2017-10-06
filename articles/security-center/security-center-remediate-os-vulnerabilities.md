---
title: "le vulnerabilità del sistema operativo aaaRemediate in Centro sicurezza di Azure | Documenti Microsoft"
description: "Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * OS correggere vulnerabilità * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>Risolvere le vulnerabilità del sistema operativo in Centro sicurezza di Azure
Centro sicurezza di Azure ogni giorno analizza il sistema operativo di macchina virtuale (VM) (sistema operativo) per le configurazioni che è possibile apportare hello VM più vulnerabile tooattack ed è consigliabile utilizzare le modifiche di configurazione tooaddress queste vulnerabilità. Centro sicurezza PC consiglia di risolvere le vulnerabilità quando configurazione del sistema operativo della macchina virtuale non corrisponde ad hello regole di configurazione consigliata.

> [!NOTE]
> Per ulteriori informazioni sulle configurazioni di hello specifici da monitorare, vedere hello [elenco delle regole di configurazione consigliata](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-hello-recommendation"></a>Implementare la raccomandazione hello

> [!NOTE]
> Questo documento introduce servizio hello utilizzando un esempio di distribuzione.  Questo argomento non costituisce una guida dettagliata.
>
>

1. In hello **indicazioni** pannello seleziona **vulnerabilità monitora e aggiorna sistema operativo**.
   ![Remediate OS vulnerabilities][1]

    Hello **vulnerabilità monitora e aggiorna sistema operativo** pannello apre ed elenca le macchine virtuali con configurazioni del sistema operativo che non corrispondono a regole di configurazione consigliata hello.  Per ogni macchina virtuale, identifica pannello hello:

   * **REGOLE non è stato** -numero hello di regole hello configurazione del sistema operativo della macchina virtuale non è riuscita.
   * **ORA dell'ultima analisi** - hello data e l'ora che il Centro sicurezza PC ultima verifica disponibilità aggiornamenti configurazione del sistema operativo della macchina virtuale di hello.
   * **STATO** -hello stato corrente della vulnerabilità hello:

     * Apri: vulnerabilità hello è non stata risolta ancora
     * In corso: Vulnerabilità hello attualmente applicato, è necessario alcun intervento da parte dell'utente
     * Risolto: vulnerabilità hello è stato già risolto (quando hello problema è stato risolto, la voce hello è grigio)
   * **GRAVITÀ** -tutte le vulnerabilità sono impostate tooa gravità bassa, vale a dire una vulnerabilità deve essere risolti, ma non richiede attenzione immediata.

2. Selezionare una macchina virtuale. Un pannello per tale macchina virtuale viene aperto e le regole di hello che non sono stato.
   ![Regole di configurazione non riuscite][2]

3. Selezionare una regola. In questo esempio selezioniamo **Le password devono essere conformi ai requisiti di complessità**. Un pannello apre hello non è stato possibile regola e hello impatto che descrive. Esaminare i dettagli di hello e prendere in considerazione le modalità di applicazione delle configurazioni del sistema operativo.
  ![Descrizione per la regola non riuscito di hello][3]

  Centro sicurezza PC utilizza identificatori univoci tooassign di enumerazione di configurazione comuni (CCE) per le regole di configurazione. Hello le seguenti informazioni verrà fornita in questo pannello:

  - NOME: nome della regola
  - GRAVITÀ: valore della gravità di CCE a livello critico, importante o di avviso
  - CCIED - Identificatore univoco CCE per regola hello
  - DESCRIZIONE: descrizione della regola
  - VULNERABILITÀ: spiegazione della vulnerabilità o del rischio in caso di mancata applicazione della regola
  - IMPATTO: impatto sull'azienda quando viene applicata la regola
  - VALORE previsto, ovvero Valore previsto quando il Centro sicurezza PC consente di analizzare la configurazione del sistema operativo VM rispetto regola hello
  - OPERAZIONE di regola - Regola operazione utilizzata dal centro di sicurezza durante l'analisi della configurazione del sistema operativo VM rispetto regola hello
  - Il valore effettivo: Valore restituito dopo l'analisi della configurazione del sistema operativo VM rispetto regola hello
  - RISULTATO DELLA VALUTAZIONE: risultati dell'analisi: riuscita, non riuscita

## <a name="see-also"></a>Vedere anche
In questo articolo ha illustrato come tooimplement hello Centro sicurezza PC indicazione "del sistema operativo di correggere vulnerabilità." È possibile esaminare i set di regole di configurazione di hello [qui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Centro sicurezza PC utilizza identificatori univoci di tooassign CCE (Common Configuration Enumeration) per le regole di configurazione. Visitare hello [CCE](https://nvd.nist.gov/cce/index.cfm) sito per ulteriori informazioni.

toolearn ulteriori informazioni su Centro di sicurezza, vedere hello seguenti risorse:

* [Supported platforms in Azure Security Center](security-center-os-coverage.md) (Piattaforme supportate nel Centro sicurezza di Azure): contiene un elenco di macchine virtuali Windows e Linux supportate.
* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
