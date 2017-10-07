---
title: "Gestione identità ibride Active Directory aaaAzure considerazioni di progettazione: determinare le attività di gestione identità ibride | Documenti Microsoft"
description: "Con il controllo di accesso condizionale, Azure Active Directory verifica specifiche condizioni hello selezionate per l'autenticazione utente hello e prima di consentire l'accesso toohello applicazione. Quando queste condizioni sono soddisfatte, l'utente di hello è autenticato e accesso toohello applicazione consentita."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a>Pianificare il ciclo di vita dell’identità ibrida
Identità è una funzionalità di base di hello di enterprise mobility e applicazione strategia di accesso. Se si accede sul dispositivo mobile di tooyour o applicazione SaaS, l'identità è hello toogaining chiave accesso tooeverything. Al livello più alto, una soluzione di gestione delle identità comprende unificazione e la sincronizzazione tra il repository di identità che include l'automazione e la centralizzazione processo hello di provisioning delle risorse. soluzione di identità Hello deve essere un'identità centralizzata in locale e nel cloud e inoltre usare una forma di autenticazione centralizzata di identità federativa toomaintain e in modo sicuro condividere e collaborare con aziende e utenti esterni. Risorse compreso tra i sistemi operativi e applicazioni toopeople in o associato, un'organizzazione. Struttura organizzativa può essere modificata tooaccommodate hello provisioning criteri e procedure.

È inoltre importante toohave una soluzione di identità pensati tooempower gli utenti fornendo con tookeep esperienze self-service li produttivi. La soluzione di identità è più affidabile se Abilita single sign-on per gli utenti di tutte le risorse di hello che devono accedere a tutti gli amministratori livelli possono utilizzare le procedure standard per la gestione delle credenziali dell'utente. Alcuni livelli di amministrazione possono essere ridotti o eliminati, a seconda della gamma hello di hello provisioning soluzione di gestione. È inoltre possibile distribuire funzionalità di amministrazione in aziende diverse, manualmente o automaticamente e in totale sicurezza. Ad esempio, un amministratore di dominio può essere utilizzato solo a persone hello e risorse in tale dominio. L'utente può eseguire attività amministrative e di provisioning, ma è toodo non autorizzato le attività di configurazione, ad esempio la creazione di flussi di lavoro.

## <a name="determine-hybrid-identity-management-tasks"></a>Determinare le attività di gestione di un'identità ibrida
La distribuzione delle attività amministrative nell'organizzazione migliora l'accuratezza di hello e l'efficienza dell'amministrazione e migliora il saldo di hello del carico di lavoro hello di un'organizzazione. Di seguito sono pivot hello che definiscono un sistema di gestione di identità affidabili.

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

attività di gestione identità ibride toodefine, è necessario comprendere alcune caratteristiche essenziali di organizzazione hello che adozione di identità ibride. È importante toounderstand hello corrente i repository utilizzati per le origini di identità. Conoscendo i principali elementi, si dispone di requisiti fondamentali hello e in base che è necessario tooask più granulare a domande che comporti tooa migliori decisioni di progettazione per la soluzione di identità.  

Quando si definiscono questi requisiti, verificare che almeno hello di seguito sono risposte alle domande

* Opzioni di provisioning: 
  
  * Soluzione con identità ibrida hello supporta un solido account accesso sistema di gestione e provisioning?
  * Come vengono utenti, gruppi e le password verranno toobe gestito?
  * È la gestione del ciclo di vita delle identità hello reattiva? 
    * Quanto dura la sospensione dell'account per l'aggiornamento delle password?
* Gestione delle licenze: 
  
  * Hello gestione delle licenze handle soluzione identità ibrida?
    * In caso affermativo, quali funzionalità sono disponibili?
* Gestione delle licenze basate su gruppo handle soluzione hello fa? 
  
      - In caso affermativo, è possibile tooassign un tooit gruppo di sicurezza? 
       - In caso affermativo, verrà directory cloud hello automaticamente assegnare licenze tooall hello membri del gruppo di hello? 
        - Cosa accade se un utente viene successivamente aggiunti o rimossi dal gruppo di hello, verrà una licenza automaticamente assegnata o rimosso come appropriata? 
* Integrazione con provider di identità di terze parti:
* Questa soluzione ibrida può essere integrata con identità di terze parti provider tooimplement single sign-on?
* È possibile toounify tutti hello provider di identità diversi in un sistema di identità coesiva?
* In caso affermativo, che caratteristiche presentano e quali funzionalità offrono?

## <a name="synchronization-management"></a>Gestione della sincronizzazione
Uno degli obiettivi di hello di gestione identità, toobring in grado di toobe tutti i provider di identità di hello e mantenerli sincronizzati. Mantenere i dati di hello sincronizzati in base a un provider di identità master autorevole. In uno scenario di identità ibrido, con un modello di Gestione sincronizzazione, gestire tutte le identità di utenti e dispositivi in un server locale e sincronizzare gli account hello e, facoltativamente, cloud toohello le password. Hello utente immette la stessa password locale come egli in cloud hello e, hello la password di accesso, viene verificato dalla soluzione di identità hello hello. Questo modello usa uno strumento di sincronizzazione di directory.

![](./media/hybrid-id-design-considerations/Directory_synchronization.png)Assicurarsi di sincronizzazione di hello tooproper progettazione della soluzione di identità ibrida che hello domande seguenti sono disponibili: • quali sono le soluzioni di sincronizzazione hello disponibili per la soluzione con identità ibrida hello?
• Quali sono hello l'accesso single sign sulle funzionalità disponibili?
• Opzioni hello per federazione delle identità tra B2B e B2C?

## <a name="next-steps"></a>Passaggi successivi
[Determinare la strategia di adozione di una soluzione per la gestione di un'identità ibrida](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

