---
title: gli utenti di Azure Active Directory aaaLicense nel portale di Azure classico hello | Documenti Microsoft
description: "Descrizione delle licenze di Microsoft Azure Active Directory, come funziona, la modalità di avvio tooget e le procedure consigliate, inclusi Office 365, Microsoft Intune e Azure Active Directory Premium e le edizioni Basic"
services: active-directory
keywords: Licenze di Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>Che cos'è Microsoft Azure Active Directory licenze nel portale di Azure classico hello?

> [!div class="op_single_selector"]
> * [Istruzioni del portale di Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Informazioni sul portale di Azure classico](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) è una soluzione e piattaforma IDaaS (Identity as a Service) di Microsoft. Azure AD è disponibile un numero di versioni funzionali e tecnici che vanno da Azure AD gratuito, è disponibile con qualsiasi servizio Microsoft quali Office 365, Dynamics, Microsoft Intune e Azure (Azure AD non genera eventuali addebiti di consumo in questa modalità), tooAzure AD a pagamento, versioni, ad esempio Enterprise Mobility Suite (EMS), Azure AD Premium e Basic, come Azure multi-Factor Authentication (MFA). Come molti servizi online Microsoft, la maggior parte delle versioni a pagamento di Azure AD sono fornite tramite diritti per utente in quanto sono in Office 365, Microsoft Intune e Azure AD. In questi casi, acquisto hello è rappresentato con una o più sottoscrizioni e ogni sottoscrizione include un numero di pre-acquisto di licenze nel tenant. I diritti utente si realizzano mediante l'assegnazione delle licenze, creare un collegamento tra l'utente hello e prodotto di hello, che consente di componenti del servizio per l'utente hello, hello e utilizzo di un di hello prepagato licenze.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per modalità tooassign i ruoli di amministratore in Azure AD salve center, vedere [licenza se stessi e per gli utenti in Azure AD](active-directory-licensing-get-started-azure-portal.md).

[Provare Azure AD Premium](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Portale di amministrazione di Azure AD è una parte di hello portale di Azure classico. Anche se l'uso di Azure AD non richiede l'acquisto di Azure, l'accesso a questo portale richiede una sottoscrizione di Azure attiva o una [sottoscrizione di valutazione di Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

Per una panoramica estesa delle funzionalità del servizio Azure AD, vedere [Cos'è Azure AD](active-directory-whatis.md).
[Ulteriori informazioni sui livelli di servizio Azure AD](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Le sottoscrizioni di Azure prepagato sono diverse: mentre rappresentata anche nella directory, queste sottoscrizioni abilitare la creazione di risorse di Azure ed eseguirne il mapping tooyour il metodo di pagamento. Sono non disponibili in questo caso associati a una sottoscrizione di hello conteggi di licenze. Associazione degli utenti con sottoscrizione hello, accedere toomanaging sottoscrizione alle risorse degli utenti hello, è necessario concedere loro autorizzazioni toooperate sottoscrizione toohello eseguito il mapping delle risorse di Azure.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Come funzionano le licenze di Azure AD?
I servizi di Azure AD basati su licenza o diritti funzionano attivando una sottoscrizione nel tenant di directory/servizio di Azure AD. Una volta hello sottoscrizione è attiva funzionalità del servizio di hello può essere gestito dagli amministratori o servizi di directory e utilizzati dagli utenti con licenza.

Quando si acquistano o attivare Enterprise Mobility Suite, Azure AD Premium o Azure AD Basic, la directory viene aggiornati con sottoscrizione di hello, incluso il periodo di validità e licenze prepagato. Le informazioni di sottoscrizione, inclusi lo stato, successivo evento del ciclo di vita e il numero di hello di licenze disponibili o assegnate è disponibili tramite hello portale di Azure classico nella scheda licenze hello per directory specifica hello. Questo è anche toobest sul posto toomanage le assegnazioni delle licenze.

Ogni sottoscrizione è costituita da uno o più piani di servizio, ogni hello mapping incluso il livello funzionale del tipo di servizio hello. ad esempio, Azure AD, Azure MFA, Microsoft Intune, Exchange Online o SharePoint Online. La gestione delle licenze Azure AD NON richiede la gestione del livello del piano di servizio. Questa è diversa da Office 365 a cui si basa su questa modalità di configurazione avanzata toomanage access tooincluded services. Azure AD si basa su nella configurazione del servizio, le funzionalità tooenable e gestire le singole autorizzazioni.

In generale, informazioni sulla sottoscrizione di Azure AD viene gestiti tramite hello portale di Azure classico, nella scheda licenze hello per directory specifica hello. Sottoscrizioni di Azure Active Directory, con l'eccezione hello di Azure AD Premium, non vengono visualizzati nel portale di Office hello.

> [!IMPORTANT]
> Azure AD Premium e Basic, nonché le sottoscrizioni di Enterprise Mobility Suite, sono tenant di directory/tootheir ristretto il provisioning. Le sottoscrizioni non possono essere suddivisi tra le directory o utenti tooentitle utilizzati in altre directory. Lo spostamento tra le directory di una sottoscrizione, è possibile ma richiede l'invio di un ticket di supporto o annullamento e acquistare nuovamente nel caso di hello di acquisti diretti.
>
> Al momento dell'acquisto di Azure AD o Enterprise Mobility Suite tramite contratti multilicenza l'attivazione della sottoscrizione verrà eseguita automaticamente quando il contratto di hello include altri Microsoft Online services, ad esempio Office 365.
>
>

Azure AD le funzionalità a pagamento breadth hello span della directory hello. Tra gli esempi sono inclusi:

* L'assegnazione basata su gruppo tooapplications, che viene attivato in un'applicazione hello specifico che si sta gestendo.
* Avanzate e funzionalità di gestione di gruppi self-service non sono disponibili nella sezione Configurazione directory hello o gruppo specifico di hello.
* Report sulla sicurezza Premium sono disponibili nella scheda di Reporting hello
* Individuazione di applicazioni cloud viene visualizzato nella hello portale di Azure con identità.

### <a name="assigning-licenses"></a>Assegnazione delle licenze
Pur ottenere una sottoscrizione che tutti occorre tooconfigure a pagamento di funzionalità, tramite Azure Active Directory le funzionalità a pagamento richiede la distribuzione di singoli utenti di destra toohello licenze. In generale, tutti gli utenti devono avere accesso tooor che viene gestita mediante un annuncio di Azure a pagamento di funzionalità devono essere assegnato una licenza. Un'assegnazione di licenze è un mapping tra un utente e un servizio acquistato, ad esempio Azure AD Premium, Basic o Enterprise Mobility Suite.

Gestire quali utenti nella directory devono disporre di una licenza è semplice. Può essere eseguita tramite l'assegnazione di regole per l'assegnazione tramite il portale di amministrazione di Azure AD hello tooa gruppo toocreate o mediante l'assegnazione delle licenze direttamente toohello individui destra tramite un portale, PowerShell o le API. Durante l'assegnazione gruppo di licenze tooa, tutti i membri del gruppo verranno assegnati una licenza. Se gli utenti vengono aggiunti o rimossi dal gruppo hello saranno licenza hello assegnati o rimossi. L'assegnazione del gruppo può utilizzare qualsiasi tooyou disponibile Gestione di gruppo ed è coerenza con l'assegnazione basata su gruppo tooapplications. Questo approccio, è possibile impostare le regole in modo che tutti gli utenti nella directory vengono assegnati automaticamente, assicurarsi che tutti gli utenti con titolo appropriato hello dispone di una licenza o delegare anche hello decisione tooother responsabili dell'organizzazione hello.

Con l'assegnazione delle licenze in base al gruppo, qualsiasi utente manca una località di utilizzo erediterà il percorso di directory hello durante l'assegnazione. Questo percorso può essere modificato dall'amministratore di hello in qualsiasi momento. Nei casi in cui hello automatizzata non è riuscita a causa di assegnazione tooerror, hello le informazioni utente in tipo di licenza che riflette tale stato.

## <a name="getting-started-with-azure-ad-licensing"></a>Introduzione alle licenze di Azure AD
Introduzione AD Azure è semplice. è anche possibile creare la directory come parte di iscrizione tooa gratuita di Azure. [Altre informazioni sulla registrazione come organizzazione](sign-up-organization.md). esempio Hello consentono di verificare che la directory è meglio allineata con altri servizi Microsoft, si può essere utilizzato o si pianifica la tooconsume e gli obiettivi prefissati per ottenere il servizio di hello.

Queste sono le procedure consigliate:

* Se si usa già uno qualsiasi dei servizi aziendali di Microsoft, è già disponibile una directory di Azure AD. In questo caso, è necessario continuare toouse hello stessa directory per altri servizi, in modo che Gestione delle identità di core, il provisioning e ibridi SSO, può essere utilizzata in tutti i servizi di hello. Gli utenti avranno un'esperienza di accesso singolo e trarranno vantaggio dalla funzionalità più complesse in tutti i servizi di hello. Di conseguenza, se si decide di toobuy un annuncio di Azure a pagamento del servizio per i dipendenti, è consigliabile utilizzare hello questo stesso toodo directory.
* Se si intende toouse Azure AD per un set diverso di utenti (partner, clienti e così via) o se si desidera che i servizi di Azure AD tooevaluate e toodo in isolamento del servizio di produzione, o se si desidera utilizzare un ambiente sandbox toosetup per i servizi, è consigliabile creare innanzitutto una nuova directory tramite il portale di hello Azure di Azure classico. [Ulteriori informazioni sulla creazione di una nuova directory di Azure AD nel portale di Azure classico hello](active-directory-licensing-directory-independence.md). nuova directory Hello verrà creato con l'account come utente esterno con autorizzazioni di amministratore globale. Quando si accede di Azure classico toohello portale con questo account, si verrà toosee in grado di questa directory e accedere a tutte le attività di amministrazione di directory. È consigliabile creare un account locale con privilegi appropriati toomanage altri servizi Microsoft (quelle non accessibili tramite hello portale di Azure classico). [Altre informazioni sulla creazione di account utente in Azure AD](active-directory-create-users.md).

> [!NOTE]
> Azure AD supporta "utenti esterni", ovvero gli account utente di un'istanza di Azure AD creati utilizzando un account Microsoft (MSA) o un'identità di Azure AD da un'altra directory. Mentre ci sono occupati estendere questa funzionalità in tutti i servizi aziendali Microsoft, ora questi account non sono supportati in alcune delle esperienze di servizi hello; ad esempio, il portale di amministrazione di Office 365 hello non supporta attualmente questi utenti. Di conseguenza, gli utenti esterni con account Microsoft non sarà portale di amministrazione di Office 365 hello tooaccess in grado di affatto, mentre gli utenti esterni da altre directory di Azure AD verranno ignorati. In quest'ultimo caso hello, account locale dell'utente solo hello, hello Azure AD o Office 365 directory in cui è stato originariamente creato utente hello, possono essere accessibili tramite queste esperienze.
>
>

Come indicato, Azure AD dispone di diverse versioni di pagamento. Queste versioni dispongono di alcune piccole differenze in merito alla disponibilità di acquisto:

| Prodotto | EA/VL | Apri | CSP | Diritti di utilizzo MPN | Acquisto diretto | Versione di valutazione |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Selezionare una o più versioni di valutazione delle licenza
 In tutti i casi, è possibile attivare una sottoscrizione di valutazione di Azure AD Premium o Enterprise Mobility Suite selezionando hello specifica versione di valutazione di desiderate nella scheda licenze hello nella directory. Entrambe le versioni di valutazione includono una sottoscrizione di 30 giorni con 100 licenze.

![Piani di licenza per le versioni di valutazione di Azure Active Directory](./media/active-directory-licensing-what-is/trial_plans.png)

![Piani di licenza per le versioni di valutazione di Enterprise Mobility Suite](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Piani di licenza per le versioni di valutazione attive](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Assegnare licenze
Una volta sottoscrizione hello è attivo, occorre assegnare una licenza tooyourself e hello browser tooensure la visualizzazione di tutte le funzionalità di aggiornamento. passaggio successivo Hello è licenze tooassign le funzionalità di Azure AD a pagamento utenti toohello che saranno necessario tooaccess o essere inclusi in. Come accennato in precedenza in "Assegnazione licenze," hello migliore modo toodo questo è il gruppo di hello tooidentify che rappresenta i destinatari hello desiderato e assegnarlo toohello licenza; In questo modo, gli utenti che vengono aggiunti o rimossi dal gruppo hello durante il ciclo di vita verranno assegnati tooor rimosso dalla licenza hello.

un gruppo di licenze tooa tooassign o singoli utenti, selezionare il piano di licenza tooassign desiderato e fare clic su hello **assegnare** hello barra dei comandi.

![Piani di licenza per le versioni di valutazione attive](./media/active-directory-licensing-what-is/assign_licenses.png)

Una volta in hello assegnazione finestra di dialogo per il piano selezionato hello, è possibile selezionare gli utenti e aggiungendoli toohello **assegnare** colonna hello destra. È possibile scorrere l'elenco di utenti hello o cercare utenti specifici tramite ricerca hello vetro su hello in alto a destra della griglia utente hello. gruppi tooassign, selezionare "Gruppi" hello **Mostra** menu e quindi fare clic su pulsante di controllo hello per le assegnazioni di hello toorefresh destra hello che vengono visualizzati.

![L'assegnazione delle licenze toogroups](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

È possibile utilizzare o pagina tramite i gruppi e aggiungerli toohello **assegnare** colonna hello allo stesso modo. È possibile utilizzare questi tooassign una combinazione di utenti e gruppi in un'unica operazione. toocomplete hello processo di assegnazione, fare clic sul pulsante di controllo hello in hello nell'angolo inferiore destro della pagina hello.

![Messaggio di stato per l’assegnazione di licenze](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Quando viene assegnato un gruppo, i relativi membri ereditano licenze hello entro 30 minuti, ma in genere entro 1-2 minuti.

Durante l'assegnazione delle licenze di Azure AD, possono verificarsi errori di assegnazione, ma sono relativamente rari. I potenziali errori di assegnazione sono limitati a:

* Conflitto di assegnazione - quando un utente è stata precedentemente assegnato una licenza che non è compatibile con la licenza corrente di hello. In questo caso, l'assegnazione di nuova licenza hello richiederà la rimozione di hello precedente.
* Le licenze disponibili superate - quando il numero di hello degli utenti in gruppi assegnati supera le licenze disponibili, lo stato di assegnazione degli utenti hello rifletterà tooassign un errore a causa di toomissing licenze.

### <a name="view-assigned-licenses"></a>Visualizzare licenze assegnate
Una visualizzazione di riepilogo delle licenze assegnate incluso sottoscrizione disponibile assegnato e successivo ciclo di vita dell'evento vengono visualizzati in hello **licenze** scheda.

![Visualizza hello numero di licenze assegnate](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Un elenco dettagliato degli utenti e dei gruppi assegnati, con lo stato di assegnazione e il percorso (diretto o ereditato da uno o più gruppi), è disponibile esplorando un piano di licenza.

![Visualizzazione dettagliata delle licenze assegnate per un piano di licenza](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Rimuovere le licenze è facile quanto assegnarle. Se è stata direttamente assegnata utente hello o per un gruppo assegnato, è possibile rimuovere la licenza hello selezionando il tipo di licenza di hello, selezionando **rimuovere**aggiunta utente hello o un elenco di gruppi toohello remove e confermare l'azione di hello. In alternativa, è possibile aprire un tipo di licenza, selezionare hello utente o gruppo specifico e toccare **rimuovere** hello barra dei comandi. tooend ereditarietà di un utente di una licenza da un gruppo, rimuovere semplicemente utente hello dal gruppo hello.

### <a name="extending-trials"></a>Estendere le versioni di valutazione
Le estensioni di valutazione per i clienti sono disponibili come self-service tramite il portale di Office 365 hello. Un amministratore del cliente può passare toohello [portale di Office](https://portal.office.com/#Billing) (accesso dipende dalle autorizzazioni per il portale di Office hello) e selezionare la versione di valutazione di Azure AD Premium. Fare clic su hello **estendere versione di valutazione** collegamento e seguire le istruzioni di hello. Sarà necessario tooenter una carta di credito, ma non ti verrà addebitata.

![Estensione di una versione di valutazione di licenze nel portale di Office hello](./media/active-directory-licensing-what-is/extend_license_trial.png)

I clienti possono inoltre richiedere un'estensione della versione di valutazione inviando una richiesta di supporto. Un amministratore del cliente può passare il portale di Office 365 toohello [pagina supporto](http://aka.ms/extendAADtrial) (accesso dipende dalle autorizzazioni per la pagina di supporto Office hello). In questa pagina selezionare "Sottoscrizioni e versioni di valutazione" in Funzionalità e "Domande sulla versione di valutazione" in Sintomo. Immettere infine le informazioni in circostanze hello

![Estensione di una versione di valutazione di licenza tramite una richiesta di supporto](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Passaggi successivi
Ora è pronto tooconfigure e usare alcune funzionalità di Azure AD Premium.

* [Reimpostazione della password self-service](active-directory-manage-passwords.md)
* [Gestione di gruppi self-service](active-directory-accessmanagement-self-service-group-management.md)
* [Stato di Azure AD Connect](active-directory-aadconnect-health.md)
* [Gruppo assegnazione tooapplications](active-directory-manage-groups.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Acquisto diretto di licenze di Azure AD Premium](http://aka.ms/buyaadp)
