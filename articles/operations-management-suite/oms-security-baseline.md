---
title: aaaOperations protezione del gruppo di gestione e di base di soluzioni di controllo | Documenti Microsoft
description: "Questo documento viene illustrato come toouse OMS Security and Audit soluzione tooperform una valutazione della linea di base di tutti i computer monitorati a scopo di conformità e sicurezza."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Valutazione baseline nella soluzione Sicurezza e controllo di Operations Management Suite
Questo documento consente di toouse [soluzione di controllo e protezione di Operations Management Suite (OMS)](operations-management-suite-overview.md) valutazione della linea di base tooaccess funzionalità hello stato sicuro le risorse monitorati.

## <a name="what-is-baseline-assessment"></a>Informazioni sulla valutazione baseline
Microsoft, insieme ad altre organizzazioni del settore e governative in tutto il mondo, definisce una configurazione di Windows che rappresenta distribuzioni server a sicurezza elevata. Questa configurazione è un set di chiavi del Registro di sistema, impostazioni dei criteri di controllo e impostazioni di criteri di sicurezza, oltre ai valori consigliati di Microsoft per queste impostazioni. Questo set di regole è noto come baseline sicurezza. La funzionalità per la valutazione baseline della soluzione Sicurezza e controllo di OMS consente di analizzare con facilità tutti i computer per verificarne la conformità. 

Esistono tre tipi di regole:

* **Regole del Registro di sistema**: verificare che le chiavi del Registro di sistema siano impostate in modo corretto.
* **Regole dei criteri di controllo**: regole relative ai criteri di controllo.
* **Le regole dei criteri di sicurezza**: le regole relative alle hello le autorizzazioni utente nel computer di hello.

> [!NOTE]
> Lettura [tooassess Usa OMS protezione hello base di configurazione della sicurezza](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) per una breve panoramica di questa funzionalità.
> 
> 

## <a name="security-baseline-assessment"></a>Valutazione baseline sicurezza
È possibile esaminare la valutazione della linea di base di sicurezza corrente per tutti i computer monitorati da OMS sicurezza e controllo tramite il dashboard di hello.  Eseguire hello del dashboard di valutazione della linea di base passaggi tooaccess hello sicurezza seguenti:

1. In hello **Microsoft Operations Management Suite** dashboard principale, fare clic su **Security and Audit** riquadro.
2. In hello **Security and Audit** dashboard, fare clic su **valutazione della linea di base** in **domini di sicurezza**. Hello **valutazione della linea di base della sicurezza** dashboard viene visualizzato come illustrato nella seguente immagine hello:
   
    ![Valutazione baseline di Sicurezza e controllo di OMS](./media/oms-security-baseline/oms-security-baseline-fig1.png)

Questo dashboard è suddiviso in tre aree principali:

* **Computer rispetto toobaseline**: in questa sezione fornisce un riepilogo del numero di hello di computer che erano accessibili e percentuale di computer passato valutazione hello hello. Offre inoltre 10 computer hello superiore e il risultato di hello percentuale per la valutazione di hello.
* **Stato regole richiesto**: in questa sezione è hello toobring intento di hello non è stato possibile regole in base alla gravità e le regole in base al tipo di non riuscita. Esaminando toohello primo grafico che è possibile identificare rapidamente se non è riuscita hello la maggior parte delle regole sono fondamentali, o non. Offre inoltre un elenco di regole con esito negativo 10 superiore hello e alla gravità. grafico secondo Hello Mostra il tipo di hello di regola non riuscita durante la valutazione di hello. 
* **Computer privi di valutazione della linea di base**: in questa sezione elenco computer hello che non erano accessibili a causa di incompatibilità di sistema toooperating o errori. 

### <a name="accessing-computers-compared-toobaseline"></a>L'accesso a computer confrontati toobaseline
In teoria, tutti i computer siano essere conforme alla valutazione della linea di base della sicurezza hello. È tuttavia previsto che in alcune circostanze non tutti i computer siano conformi. Come parte del processo di gestione di hello sicurezza, è importante tooinclude revisione computer hello che non è stato possibile toopass tutti i test di valutazione di sicurezza. Toovisualize un modo rapido per l'opzione hello **computer ai quali accede** si trova in hello **computer confrontati toobaseline** sezione. Verrà visualizzato come illustrato nella seguente schermata hello hello Registro ricerca risultati visualizzazione hello dell'elenco dei computer:

![Risultati per computer a cui è stato eseguito l'accesso](./media/oms-security-baseline/oms-security-baseline-fig2.png)

il risultato di ricerca Hello viene visualizzato in un formato di tabella, in cui hello prima colonna ha il nome di computer hello e secondo colore hello con numero di hello di regole che non è riuscita. Fare clic su informazioni di hello tooretrieve sul tipo di hello di regola non riuscita, numero hello di regole non riuscite oltre a nome computer hello. Verrà visualizzato un toohello simile di risultati illustrato nella seguente immagine hello:

![Dettagli dei risultati per computer a cui è stato eseguito l'accesso](./media/oms-security-baseline/oms-security-baseline-fig3.png)

In questo risultato ricerca hello totale di regole a cui si accede, hello numero di regole critiche che non è riuscita, hello regole per gli avvisi e hello regole informazioni non riuscita.

### <a name="accessing-required-rules-status"></a>Accesso allo stato delle regole necessarie
Dopo aver ottenuto informazioni hello riguardanti hello di numero percentuale di computer che passato valutazione hello, è opportuno tooobtain ulteriori informazioni sulle regole di cui hanno esito negativo in base toohello criticità. In questo modo, visualizzazione tooprioritize i computer nei quali devono essere risolti prima tooensure siano conformi nella valutazione successiva hello. Passare il mouse su una parte essenziale di hello del grafico hello nella hello **non riuscito di regole in base alla gravità** in riquadro **stato regole richiesto** e farvi clic sopra. Verrà visualizzato un toohello simile di risultati seguente schermata:

![Dettagli delle regole non riuscite per gravità](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

In questo risultato log viene visualizzato il tipo di hello di regola di base che non è riuscita, descrizione hello di questa regola e ID di enumerazione di configurazione comuni (CCE) hello di questa regola di sicurezza. Questi attributi deve essere sufficiente tooperform toofix un'azione correttiva il problema nel computer di destinazione hello.

> [!NOTE]
> Per ulteriori informazioni sul CCE, accesso hello [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm).
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a>Accesso ai computer senza valutazione baseline
OMS supporta membro del dominio hello e profilo di base di Controller di dominio in Windows Server 2008 R2 fino tooWindows Server 2012 R2. La baseline di Windows Server 2016 non è ancora definitiva e verrà aggiunta non appena pubblicata. Tutti gli altri sistemi operativi analizzati tramite OMS Security and Audit valutazione della linea di base viene visualizzata sotto hello **computer privi di valutazione della linea di base** sezione.

## <a name="see-also"></a>Vedere anche
In questo documento sono disponibili informazioni sulla valutazione baseline della Sicurezza e controllo di OMS. toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:

* [Panoramica di Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite](oms-security-responding-alerts.md)
* [Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo](oms-security-monitoring-resources.md)

