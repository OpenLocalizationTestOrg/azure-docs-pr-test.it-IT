---
title: aaaUse sicurezza tooenhance indicazioni di Centro sicurezza di Azure | Documenti Microsoft
description: " Informazioni su come criteri di sicurezza toouse e suggerimenti in Centro sicurezza di Azure toohelp attenuare un attacco alla sicurezza. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>Sicurezza di utilizzare il Centro protezione Azure indicazioni tooenhance
Configurare i criteri di sicurezza e quindi implementando consigli hello forniti dal Centro sicurezza di Azure, è possibile ridurre il possibilità di hello di un evento di protezione. Questo articolo illustra come criteri di sicurezza toouse e suggerimenti in Centro sicurezza PC toohelp attenuare un attacco alla sicurezza.

> [!NOTE]
> Questo articolo si basa su ruoli di hello e i concetti introdotti in Centro sicurezza PC hello [Guida alla pianificazione e le operazioni](security-center-planning-and-operations-guide.md). È una buona idea tooreview hello Guida alla pianificazione al prima di continuare.
>
>

## <a name="managing-security-recommendations"></a>Gestione delle raccomandazioni sulla sicurezza
Un criterio di sicurezza definisce il set di hello di controlli che sono consigliati per le risorse nel gruppo di risorse o di sottoscrizione specificato hello. Centro sicurezza PC, definire i criteri in base a requisiti di sicurezza della società tooyour. vedere, più toolearn [impostare criteri di sicurezza del Centro sicurezza PC](security-center-policies.md).

Criteri di sicurezza per i gruppi di risorse vengono ereditati dal livello di sottoscrizione hello.

![Ereditarietà dei criteri di sicurezza][1]

Se è necessario criteri personalizzati in gruppi di risorse specifico, è possibile disabilitare l'ereditarietà nel gruppo di risorse hello. toodisable, impostare l'ereditarietà tooUnique nel pannello dei criteri sicurezza hello e personalizzare i controlli di hello che Centro sicurezza di seguito vengono fornite indicazioni per.

Ad esempio, nel caso di carichi di lavoro che non richiedono criteri di hello SQL Database Transparent Data Encryption (TDE), disattivare hello criteri a livello di sottoscrizione hello e abilitarlo solo nei gruppi di risorse hello in cui è necessario SQL TDE.

> [!NOTE]
> Se si verifica un conflitto tra criteri a livello di sottoscrizione e il criterio a livello di gruppo risorse, il criterio a livello di gruppo risorse hello ha la precedenza.
>
>

Centro sicurezza PC analizza lo stato di sicurezza hello delle risorse di Azure. Quando il Centro sicurezza PC identifica potenziali vulnerabilità di sicurezza, viene creato basate sui controlli hello impostati nei criteri di sicurezza hello. indicazioni Hello consentono di eseguire il processo di hello di configurazione dei controlli di sicurezza hello necessita.

Le raccomandazioni correnti dei criteri nel Centro sicurezza sono incentrate sugli aggiornamenti di sistema, sulla configurazione del sistema operativo, sui gruppi di sicurezza di rete su subnet e sulle macchine virtuali (VM), sul controllo del Database SQL, sul criterio TDE del Database SQL e sui firewall dell'applicazione web. Per una descrizione più aggiornate di hello delle indicazioni di centro di sicurezza, vedere [gestione consigli relativi alla sicurezza del Centro sicurezza PC](security-center-recommendations.md).

## <a name="scenario"></a>Scenario
Questo scenario viene illustrato come toouse Centro sicurezza PC toohelp ridurre il possibilità di hello di problemi di sicurezza significativi Centro sicurezza PC consigli di monitoraggio ed eseguendo l'azione. scenario Hello Usa hello società fittizia Contoso, e presentati in hello Centro sicurezza PC [Guida alla pianificazione e le operazioni](security-center-planning-and-operations-guide.md#security-roles-and-access-controls). i ruoli di Hello rappresentano singoli utenti e gruppi che possono utilizzare attività Centro sicurezza PC tooperform diverse relative alla sicurezza. Hello ruoli sono:

![Ruoli dello scenario][2]

Contoso recentemente eseguita la migrazione alcune delle loro tooAzure risorse locali. Contoso desidera tooimplement e mantenere le protezioni che riducono le attacco alla sicurezza delle vulnerabilità tooa delle risorse nel cloud hello.

## <a name="recommended-solution"></a>Soluzione consigliata
Una soluzione è toouse Centro sicurezza PC tooprevent e rilevare vulnerabilità di sicurezza. Contoso dispone di accesso tooSecurity Center tramite la sottoscrizione di Azure. Hello [livello gratuito](security-center-pricing.md) del Centro sicurezza PC viene abilitato automaticamente in tutte le sottoscrizioni di Azure e la raccolta dei dati è abilitata in tutte le macchine virtuali nella propria sottoscrizione.

David, del reparto di sicurezza informatica di Contoso, configura i **criteri di sicurezza** con il Centro sicurezza. Centro sicurezza PC analizza lo stato di sicurezza hello delle Contoso risorse di Azure. Quando il Centro sicurezza PC identifica potenziali vulnerabilità di sicurezza, viene creato **indicazioni** basata sui controlli hello impostati nei criteri di sicurezza hello.

Jeff, un proprietario del carico di lavoro su cloud, è responsabile delle attività di implementazione e gestione della protezione secondo i criteri di sicurezza di Contoso. Jeff può monitorare indicazioni hello creati protezioni tooapply Centro sicurezza PC. indicazioni Hello in modo semplificato Jeff processo hello di configurazione dei controlli di sicurezza hello necessita.

In ordine per Jeff tooimplement e mantenere le protezioni ed eliminare le vulnerabilità di sicurezza, egli deve:

- monitorare le raccomandazioni di sicurezza presenti nel Centro sicurezza
- valutare le raccomandazioni sulla sicurezza e decidere se applicarle o ignorarle
- applicare le raccomandazioni sulla sicurezza

Seguito toosee passaggi Jeff come utilizza Centro sicurezza PC indicazioni tooguide quest'ultimo processo hello di vulnerabilità nella sicurezza tooeliminate controlli di configurazione.

## <a name="how-tooimplement-this-solution"></a>Come tooimplement questa soluzione
Jeff accede troppo[portale di Azure](https://azure.microsoft.com/features/azure-portal/) e apre hello console Centro sicurezza PC. Come parte del suo giornaliera monitoraggio delle attività, la archivia toosee se sono presenti indicazioni relative alla sicurezza eseguendo hello alla procedura seguente:

1. Jeff seleziona hello **indicazioni** riquadro tooopen hello **indicazioni** blade.
   ![Selezionare hello indicazioni riquadro][3]
2. Jeff esamina hello elenco di suggerimenti. Vede che hello elenco di suggerimenti ordinato in ordine di priorità, dalla priorità toolowest di priorità più alta è fornito da Centro sicurezza PC. Peter decide tooaddress un'indicazione di priorità alta nell'elenco di hello. Seleziona **installa Endpoint Protection** su hello **indicazioni** blade.
3. Hello **installa Endpoint Protection** pannello verrà aperto un elenco di macchine virtuali senza antimalware abilitato. Jeff esamina l'elenco di hello delle macchine virtuali, seleziona tutte le macchine virtuali e quindi seleziona **installare nelle macchine 3 virtuali**.
   ![Installare Endpoint Protection][4]
4. Hello **selezionare Endpoint Protection** pannello apre Jeff fornito con due soluzioni antimalware. Jeff seleziona hello **Microsoft Antimalware** soluzione.
5. Ulteriori informazioni sulla soluzione antimalware hello viene visualizzate. Jeff seleziona **Crea**.
   ![Microsoft antimalware][5]
6. Jeff immette le impostazioni di configurazione necessarie hello sulla hello **installare** blade e seleziona **OK**.

[Microsoft Antimalware](../security/azure-security-antimalware.md) è ora attivo in hello selezionate le macchine virtuali.

Jeff continua toomove a priorità alta hello e consigli di priorità Media, per prendere decisioni sull'implementazione. Jeff fa riferimento a hello [gestione consigli sulla sicurezza](security-center-recommendations.md) indicazioni hello toounderstand e ognuna delle quali esegue se si applica l'articolo.

Jeff apprende che [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md) esegue un monitoraggio seleziona sicurezza di rete di Azure hello e dell'infrastruttura e riceve threat intelligence ed evitare eventuali abusi reclamo di terze parti. Se Jeff fornisce i dettagli di contatto di sicurezza per la sottoscrizione di Azure di Contoso, i contatti di Microsoft Contoso se hello MSRC consente di individuare i dati dei clienti che Contoso ha avuto accesso da un'entità non autorizzata o illegale. Si applica quindi hello seguire Jeff **fornire dettagli di contatto sicurezza** indicazione (una raccomandazione con livello di gravità di supporto nell'elenco di hello di raccomandazioni descritte in precedenza).

1. Seleziona Jeff **fornire dettagli di contatto sicurezza** su hello **indicazioni** pannello, che consente di aprire hello **fornire dettagli di contatto di sicurezza** blade.
2. Jeff seleziona informazioni di contatto tooprovide hello sottoscrizione di Azure in. Viene visualizzato un altro pannello **Specificare i dettagli dei contatti di sicurezza** .
   ![Dettagli del contatto per la sicurezza][6]
3. In hello secondo **fornire dettagli di contatto sicurezza** pannello Jeff immette:

  - indirizzi di posta elettronica di contatto sicurezza Hello separati da virgole (non è presente una limitazione del numero di indirizzi di posta elettronica che è possibile immettere toohello)
  - un numero di telefono del contatto per la sicurezza

4. Jeff inoltre consente di attivare l'opzione hello **invia messaggi di posta elettronica relative agli avvisi** tooreceive messaggi di posta elettronica relative agli avvisi di livello di gravità elevato.
5. Seleziona Jeff **OK** sicurezza hello tooapply contattare sottoscrizione del tooContoso informazioni.

Infine, Davide esamina raccomandazione per priorità bassa hello **vulnerabilità monitora e aggiorna sistema operativo** e determina che questa raccomandazione non è applicabile. Indicazione di hello toodismiss desidera. Jeff Seleziona punti di hello tre visualizzati toohello destra, quindi seleziona **Dismiss**.
   ![Ignorare la raccomandazione][7]

## <a name="conclusion"></a>Conclusione
Il monitoraggio delle raccomandazioni nel Centro sicurezza PC può contribuire a eliminare le vulnerabilità di sicurezza prima che si verifichi un attacco. È possibile evitare problemi di sicurezza applicando e gestendo le protezioni con i criteri di protezione nel Centro sicurezza.

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
