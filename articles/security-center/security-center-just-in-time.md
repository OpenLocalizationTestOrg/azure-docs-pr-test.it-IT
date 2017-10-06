---
title: aaaJust nella macchina virtuale ora accedere nel Centro protezione di Azure | Documenti Microsoft
description: "Questo documento illustra la modalità in-time VM in consente di Centro protezione Azure controllare accedere tooyour Azure le macchine virtuali."
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
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Gestire l'accesso alle macchine virtuali con la funzionalità JIT (Just-in-Time)

Solo nella macchina virtuale ora (VM) accesso può essere utilizzato toolock verso il basso il traffico in entrata tooyour macchine virtuali di Azure, riducendo l'esposizione tooattacks fornendo un accesso semplice tooconnect tooVMs quando necessario.

> [!NOTE]
> Hello solo nella funzione di tempo è in anteprima e disponibile nel livello Standard del Centro sicurezza PC hello.  Vedere [prezzi](security-center-pricing.md) toolearn ulteriori informazioni su Centro sicurezza di livelli di prezzo.
>
>

## <a name="attack-scenario"></a>Scenario di attacco

Attacchi di forza bruta attacchi comunemente porte di gestione di destinazione come un tooa di accesso toogain significa macchina virtuale. Se ha esito positivo, un utente malintenzionato può assumere il controllo hello VM e stabilire un mercato nel proprio ambiente.

Attacco di forza bruta tooa esposizione tooreduce unidirezionale è toolimit hello periodo di tempo che una porta è aperta. Porte di gestione eseguire non è necessario toobe aprire in qualsiasi momento. È necessario toobe aprire mentre si toohello connesso macchina virtuale, ad esempio tooperform di sono attività di gestione o manutenzione. Quando è abilitata in-time, viene utilizzato il Centro sicurezza PC [Network Security Group](../virtual-network/virtual-networks-nsg.md) regole (gruppo), che limitano l'accesso a porte toomanagement in modo che non possono essere assegnati da utenti malintenzionati.

![Scenario Just-in-Time][1]

## <a name="how-does-just-in-time-access-work"></a>Come funziona l'accesso Just-in-Time?

Quando è abilitata in-time, il Centro sicurezza PC protegge il traffico in entrata tooyour macchine virtuali di Azure tramite la creazione di una regola di gruppo. Selezionare le porte hello in hello VM toowhich verrà bloccato il traffico in ingresso verso il basso. Queste porte sono controllate da hello solo nella soluzione di tempo.

Quando un utente richiede accesso tooa macchina virtuale, il Centro sicurezza PC controlla tale utente hello [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md) delle autorizzazioni per l'accesso in scrittura per hello risorse di Azure. Se dispongono delle autorizzazioni di scrittura, hello richiesta viene approvata e il Centro sicurezza PC configura automaticamente hello rete sicurezza gruppi di porte di gestione del traffico toohello di tooallow in ingresso per hello di tempo specificato. Dopo il tempo di hello è scaduto, il Centro sicurezza PC Ripristina lo stato precedente hello NSGs tootheir.

> [!NOTE]
> L'accesso Just-in-Time alle macchine virtuali in Centro sicurezza attualmente supporta solo le macchine virtuali distribuite tramite Azure Resource Manager. informazioni su hello classic e modelli di distribuzione di gestione delle risorse, vedere toolearn [Azure Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Uso dell'accesso Just-in-Time

Hello **immediatamente nell'accesso alla VM ora** riquadro hello **Centro sicurezza PC** pannello viene visualizzato il numero di hello di macchine virtuali configurate per solo nel tempo accesso e hello il numero di richieste di accesso approvato effettuate in hello ultima settimana.

Hello seleziona **immediatamente nell'accesso in fase di VM** riquadro e hello **immediatamente nell'accesso in fase di VM** apre pannello.

![Riquadro Accesso Just-In-Time alla VM][2]

Hello **immediatamente nell'accesso in fase di VM** pannello fornisce informazioni sullo stato di hello delle macchine virtuali:

- **Configurato** -macchine virtuali che sono stati configurati toosupport just-in-accesso in fase di macchina virtuale. dati Hello presentati per hello settimana scorsa e includono per ogni VM hello numerose richieste approvate, data dell'ultimo accesso e l'ora e dell'ultimo utente.
- **Consigliata** - Macchine virtuali che possono supportare l'accesso Just-In-Time, ma che non sono state configurate a tale scopo. È consigliabile abilitare il controllo dell'accesso Just-In-Time per queste macchine virtuali. Vedere [Abilitare l'accesso Just-In-Time alle macchine virtuali](#enable-just-in-time-vm-access).
- **Nessuna raccomandazione** -motivi che possono causare una macchina virtuale non toobe consigliati sono:
  - Mancante NSG - hello solo nella soluzione ora richiede un toobe NSG sul posto.
  - Macchina virtuale classica - L'accesso Just-in-Time alle macchine virtuali in Centro sicurezza attualmente supporta solo le macchine virtuali distribuite tramite Azure Resource Manager. Una distribuzione classica non è supportata da hello solo nella soluzione di tempo.
  - Altro - una macchina virtuale si trova in questa categoria se hello in-time soluzione è stata disattivata in Criteri di sicurezza hello di sottoscrizione hello o un gruppo di risorse hello o tale hello VM manca un indirizzo IP pubblico e non dispone di un gruppo sul posto.

## <a name="configuring-a-just-in-time-access-policy"></a>Configurazione dei criteri di accesso Just-In-Time

hello tooselect macchine virtuali che si desidera tooenable:

1. In hello **immediatamente nell'accesso alla VM ora** blade, seleziona hello **consigliato** scheda.

  ![Abilitare l'accesso Just-in-Time][3]

2. In **macchine virtuali**, selezionare le macchine virtuali hello che si desidera tooenable. In questo modo un tooa Avanti VM di segno di spunta.
3. Selezionare **Abilita JIT in VM**.
4. Selezionare **Salva**.

### <a name="default-ports"></a>Porte predefinite

È possibile visualizzare porte predefinite hello che centro di sicurezza è consigliabile specificare in-time.

1. In hello **immediatamente nell'accesso alla VM ora** blade, seleziona hello **consigliato** scheda.

  ![Visualizzare le porte predefinite][6]

2. In **Macchine virtuali** selezionare una macchina virtuale. In questo modo un segno di spunta successivo toohello macchina virtuale e quindi apre hello **configurazione di accesso VM JIT** blade. Questo pannello consente di visualizzare le porte predefinite hello.

### <a name="add-ports"></a>Aggiungere porte

Da hello **configurazione di accesso VM JIT** pannello, è possibile anche aggiungere e configurare una nuova porta su cui si desidera hello tooenable solo nella soluzione di tempo.

1. In hello **configurazione di accesso VM JIT** pannello seleziona **Aggiungi**. Verrà visualizzata hello **Aggiungi configurazione della porta** blade.

  ![Configurazione delle porte][7]

2. In **Aggiungi configurazione della porta** pannello identificare hello porta, il tipo di protocollo, tempo di richiesta gli IP di origine e numero massimo consentita.

  Consentito gli IP di origine sono hello accesso consentito tooget gli intervalli IP durante una richiesta approvata.

  Tempo massimo della richiesta è l'intervallo di tempo massimo di hello che possa essere aperta una porta specifica.

3. Selezionare **OK**.

## <a name="requesting-access-tooa-vm"></a>La richiesta di accesso tooa VM

toorequest accesso tooa VM:

1. In hello **immediatamente nell'accesso alla VM ora** blade, seleziona hello **configurata** scheda.
2. In **macchine virtuali**, selezionare le macchine virtuali hello che si desidera tooenable accesso. In questo modo un tooa Avanti VM di segno di spunta.
3. Selezionare **Richiedi accesso**. Verrà visualizzata hello **richiedere l'accesso** blade.

  ![Richiesta di accesso tooa VM][4]

4. In hello **richiedere l'accesso** pannello è configurare per ogni tooopen porte hello di macchina virtuale con indirizzo IP di origine hello hello porta è aperta intervallo di tempo hello tooand per cui hello porta è aperta. È possibile richiedere l'accesso toohello solo a porte configurate in hello solo nei criteri di tempo. Ogni porta ha un tempo massimo consentito, derivato da hello solo nei criteri di tempo.
5. Selezionare **Open ports** (Apri porte).

## <a name="editing-a-just-in-time-access-policy"></a>Modifica dei criteri di accesso Just-In-Time

È possibile modificare una macchina virtuale esistente solo nei criteri di tempo aggiungendo e configurando un nuovo tooopen porta per la macchina virtuale o mediante la modifica di qualsiasi altro parametro porta tooan correlate già protetta.

In ordine tooedit esistente solo nei criteri di tempo di una macchina virtuale, hello **configurata** scheda viene usata:

1. In **macchine virtuali**, selezionare una macchina virtuale tooadd tooby una porta facendo clic su punti hello tre all'interno di riga hello per la macchina virtuale. Verrà aperto un menu.
2. Selezionare **modifica** nel menu hello. Verrà visualizzata hello **configurazione di accesso VM JIT** blade.

  ![Modificare i criteri][8]

3. In hello **configurazione di accesso VM JIT** pannello, è possibile modificare le impostazioni esistenti di hello di una porta già protetta facendo clic su una porta specifica, o è possibile selezionare **Aggiungi**. Verrà visualizzata hello **Aggiungi configurazione della porta** blade.

  ![Aggiungere una porta][7]

4. In **Aggiungi configurazione della porta** pannello identificare porta hello, tipo di protocollo, gli indirizzi IP di origine consentiti e tempo massimo della richiesta.
5. Selezionare **OK**.
6. Selezionare **Salva**.

## <a name="auditing-just-in-time-access-activity"></a>Controllo delle attività di accesso Just-in-Time

È possibile ottenere informazioni approfondite sulle attività delle macchine virtuali tramite la funzionalità Ricerca log. registri tooview:

1. In hello **immediatamente nell'accesso alla VM ora** blade, seleziona hello **configurata** scheda.
2. In **macchine virtuali**, selezionare un informazioni tooview VM su facendo clic su punti hello tre all'interno di riga hello per la macchina virtuale. Verrà aperto un menu.
3. Selezionare **Log attività** nel menu hello. Verrà visualizzata hello **log attività** blade.

![Selezionare il log attività][9]

Hello **log attività** pannello fornisce una visualizzazione filtrata di operazioni precedenti per la macchina virtuale con data, ora e sottoscrizione.

![Visualizzare il log attività][5]

È possibile scaricare informazioni sul log hello selezionando **fare clic qui toodownload tutti gli elementi di hello in formato CSV**.

Modificare i filtri di hello e selezionare **applica** toocreate una ricerca e log.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Uso dell'accesso Just-In-Time alle macchine virtuali tramite PowerShell

In ordine toouse Ciao solo tempi di una soluzione tramite PowerShell, assicurarsi di avere hello [più recente](/powershell/azure/install-azurerm-ps) versione di Azure PowerShell.
Al termine dell'operazione, è necessario hello tooinstall [più recente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Centro sicurezza di Azure dalla raccolta di PowerShell hello.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>Configurazione dei criteri Just-In-Time per una macchina virtuale

tooconfigure un solo nei criteri di tempo in una macchina virtuale specifica, è necessario toorun questo comando nella sessione di PowerShell: Set-ASCJITAccessPolicy.
Seguire hello cmdlet documentazione toolearn altre.

### <a name="requesting-access-tooa-vm"></a>La richiesta di accesso tooa VM

una macchina virtuale specifica che è protetta con tooaccess hello solo nella soluzione di tempo, è necessario toorun questo comando nella sessione di PowerShell: ASCJITAccess Invoke.
Seguire hello cmdlet documentazione toolearn altre.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato descritto come in-time accesso macchina virtuale in Centro sicurezza PC consente accesso tooyour Azure è possibile controllare le macchine virtuali.

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

- [L'impostazione di criteri di sicurezza](security-center-policies.md) -informazioni come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
- [Gestione delle raccomandazioni di sicurezza](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.
- [Il monitoraggio dello stato di sicurezza](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.
- [La gestione e risponde avvisi toosecurity](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere.
- [Monitoraggio di soluzioni per i partner](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
- [Domande frequenti su Centro sicurezza PC](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
- [Blog sulla sicurezza di Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
