---
title: aaaGet avviato con licenze in Azure Active Directory | Documenti Microsoft
description: Come Azure Active Directory licenze funziona come tooget iniziare a usare le procedure consigliate
services: active-directory
keywords: Licenze di Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Concessione di licenze a se stessi e agli utenti in Azure Active Directory

> [!div class="op_single_selector"]
> * [Istruzioni del portale di Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Informazioni sul portale di Azure classico](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) è una soluzione e piattaforma IDaaS (Identity as a Service) di Microsoft. Azure AD è offerta in varie edizioni di servizio:

* Azure Active Directory Free, disponibile con qualsiasi servizio Microsoft, come Office 365, Dynamics, Microsoft Intune o Azure. Azure AD non genera alcun addebito di utilizzo in questa modalità.

* Edizioni a pagamento di Azure AD, ad esempio:
  - Enterprise Mobility + Security 
  - Azure AD Premium (P1 e P2)
  - Azure AD Basic
  - Azure Multi-Factor Authentication

Come molti servizi online Microsoft, la maggior parte delle versioni a pagamento di Azure AD sono fornite tramite diritti per utente in quanto sono in Office 365, Microsoft Intune e Azure AD. In questi casi, acquisto hello è rappresentato da una o più sottoscrizioni e ogni sottoscrizione include alcune licenze prepurchased nel tenant. I diritti per utente vengono ottenuti tramite una delle azioni seguenti:

* Assegnazione di una licenza. 
* Creazione di un collegamento tra l'utente di hello e prodotto hello.
* Abilitazione di componenti del servizio per l'utente hello hello.
* Utilizzo di un di hello prepagato licenze.

[Provare Azure AD Premium](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Per una panoramica estesa delle funzionalità del servizio Azure AD, vedere [Informazioni su Azure Active Directory](active-directory-whatis.md). Per altre informazioni, vedere la [pagina Contratti di servizio](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Le sottoscrizioni di pagamento di Azure abilitano la creazione di risorse di Azure e quindi eseguirne il mapping tooyour il metodo di pagamento. Non sono associati alla sottoscrizione di hello non conteggi di licenze. Quando si concede che un toooperate di autorizzazione utente alle risorse di Azure mappata toohello sottoscrizione, sono associate hello sottoscrizione e possono gestire le risorse di sottoscrizione.

## <a name="how-does-azure-active-directory-licensing-work"></a>Come funzionano le licenze di Azure Active Directory?

I servizi di Azure AD basati su licenza funzionano attivando una sottoscrizione nel tenant di servizio di Azure AD. Dopo la sottoscrizione di hello è attiva, funzionalità del servizio di hello gestiti dagli amministratori di Azure AD e utilizzati dagli utenti con licenza.

### <a name="manage-subscription-information"></a>Gestire le informazioni sulla sottoscrizione

All'acquisto di Enterprise Mobility + Security, Azure AD Premium o Azure AD Basic, il tenant verrà aggiornato con una sottoscrizione di hello, incluso il periodo di validità e prepagato licenze. Le informazioni di sottoscrizione, tra cui hello numero di licenze assegnate o disponibile, sono disponibile tramite il portale di Azure hello: in **Azure Active Directory**aprire hello **licenze** riquadro hello directory specifica. Hello **licenze** pannello anche è hello toomanage sul posto migliore le assegnazioni delle licenze.

Ogni sottoscrizione è costituita da uno o più piani di servizio, ad esempio Azure AD, Multi-Factor Authentication, Intune, Exchange Online o SharePoint Online.  La gestione delle licenze di Azure AD *non* richiede la gestione del livello del piano di servizio. Office 365 è diversa perché si basa su questa modalità di configurazione avanzata toomanage access tooincluded services. Azure Active Directory si basa sulle funzionalità di configurazione in condizioni operative tooenable e gestire le singole autorizzazioni.

> [!IMPORTANT]
> Azure AD Premium, Azure AD Basic ed Enterprise Mobility + sottoscrizioni di sicurezza sono tenant di directory/tootheir ristretto il provisioning. Le sottoscrizioni non possono essere suddivisi tra le directory o utenti tooentitle utilizzati in altre directory. Lo spostamento di una sottoscrizione tra directory è possibile, ma richiede l'invio di un ticket di supporto o l'annullamento e il riacquisto nel caso di acquisti diretti.
>
> Quando Azure AD o Enterprise Mobility + Security acquistati tramite una sottoscrizione di Volume Licensing e quando il contratto di hello include altri Microsoft Online services (ad esempio, Office 365), l'attivazione avviene automaticamente. 

### <a name="assign-licenses"></a>Assegnare licenze

Anche se ottenere una sottoscrizione è che tutto è necessario tooconfigure a pagamento di funzionalità, è ancora necessario distribuire licenze per Azure AD a pagamento toousers funzionalità. Tutti gli utenti devono avere accesso tooor che viene gestita mediante un annuncio di Azure a pagamento di funzionalità devono essere assegnato una licenza. Un'assegnazione di licenza consiste nell'associazione di un utente a un servizio acquistato, ad esempio Azure AD Premium o Basic oppure Enterprise Mobility + Security.


Per gestire gli utenti presenti nella directory che devono disporre di una licenza, è possibile eseguire una di queste operazioni: 

* L'assegnazione delle licenze toogroups in hello [portale di Azure](active-directory-licensing-whatis-azure-portal.md).
* L'assegnazione delle licenze direttamente toousers tramite il portale di hello, PowerShell o le API. 

Quando si sta assegnando gruppo tooa licenze, tutti i membri del gruppo vengono assegnati una licenza. Se gli utenti vengono aggiunti o rimossi dal gruppo di hello, licenza hello viene assegnato o rimosso. L'assegnazione del gruppo può utilizzare qualsiasi tooyou disponibile Gestione di gruppo e sia coerenza con l'assegnazione basata su gruppo tooapplications.

È possibile utilizzare [assegnazione delle licenze in base al gruppo](active-directory-licensing-whatis-azure-portal.md) tooset le regole come illustrato di seguito hello:
* Tutti gli utenti nella directory ottengono automaticamente una licenza
* Tutti gli utenti con titolo appropriato hello Ottiene una licenza
* È possibile delegare hello decisione tooother responsabili dell'organizzazione hello (tramite [gruppi self-service](active-directory-accessmanagement-self-service-group-management.md))

Per informazioni dettagliate su toogroups di assegnazione di licenza, tra cui avanzate scenari e Office 365 licenze scenari, vedere [assegnare licenze toousers tramite l'appartenenza di gruppo in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Introduzione alle licenze di Azure AD

Iniziare a usare Azure AD è semplice. È sempre possibile creare la propria directory come parte di una registrazione a una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/offers/ms-azr-0044p/).

Hello procedure consigliate seguenti contribuisce a garantire che il tenant è allineato con altri servizi Microsoft che stia utilizzando e con gli obiettivi per il servizio hello:

- Se si sta già usando uno dei servizi aziendali di hello da Microsoft, hai già un tenant di Azure AD. È utile toouse hello che stesso tenant per altri servizi in modo che Gestione delle identità di core, il provisioning e ibrida single sign-on (SSO), possono essere utilizzati in tutti i servizi di hello. Con single sign-on, gli utenti vantaggio dalle funzionalità avanzate di hello in tutti i servizi di hello. Pertanto, se si decide di toobuy un servizio di Azure AD a pagamento per i dipendenti, è consigliabile utilizzare hello stesso tenant nuovo.

- È consigliabile utilizzare un nuovo tenant nel portale di Azure hello se si prevede di:
  - Usare Azure AD per un diverso set di utenti, ad esempio partner o clienti.
  - Valutare i servizi di Azure AD in modo indipendente dal servizio di produzione.
  - Configurare un ambiente sandbox per i servizi.

  nuova directory Hello viene creato con l'account come un utente esterno con autorizzazioni di amministratore globale. Quando si accede toohello portale di Azure con questo account, è possibile vedere questo tenant e accedere a tutte le attività amministrative.

> [!NOTE]
> Azure AD supporta gli "utenti guest", ovvero gli account utente di un tenant di Azure AD creati usando un account Microsoft o un'identità di Azure AD da un altro tenant. portale di amministrazione di Office 365 Hello attualmente non supporta questi utenti. Gli utenti guest con account Microsoft non sono portale di amministrazione di Office 365 hello tooaccess in grado di affatto, mentre gli utenti guest dagli altri tenant Azure AD vengono ignorati. In quest'ultimo caso hello, hello solo account locale dell'utente, in Azure AD hello o tenant di Office 365 in cui è stato originariamente creato utente di hello, è accessibile.

### <a name="select-one-or-more-license-trials"></a>Selezionare una o più versioni di valutazione delle licenza

È possibile attivare una sottoscrizione di valutazione di Azure AD Premium o Enterprise Mobility + Security in **Azure Active Directory** &gt; **Avvio rapido**.

![Selezionare una versione di valutazione](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Licenze di valutazione sono disponibili in hello **licenze** blade.

### <a name="assign-licenses-toousers-and-groups"></a>Assegnare licenze toousers e gruppo

Dopo la sottoscrizione di hello è attiva, è necessario assegnare una licenza tooyourself. Aggiornare quindi hello tooensure di browser di visualizzare tutte le funzionalità di hello. passaggio successivo Hello è tooassign licenze toohello utenti devono accedere alle funzionalità di Azure AD toopaid. Come descritto in [assegnare licenze](#assign-licenses), un modo semplice tooassign licenze è gruppo hello tooidentify che rappresenta hello desiderano destinatari e assegnare tooit licenza hello. In questo modo, gli utenti che vengono aggiunti o rimossi dal gruppo hello durante il ciclo di vita vengono assegnati o rimossi da licenza di hello, rispettivamente.

> [!NOTE]
> Alcuni servizi Microsoft non sono disponibili in tutte le posizioni. Prima di può essere assegnata una licenza utente tooa, messaggio per l'amministratore deve specificare hello **località di utilizzo** proprietà per utente hello. È possibile impostare questa proprietà in **utente** &gt; **profilo** &gt; **impostazioni** in hello portale di Azure. Quando si utilizza l'assegnazione del gruppo di licenze, qualsiasi utente il cui percorso di utilizzo non è specificato eredita percorso hello della directory di hello.

tooassign una licenza, in **Azure Active Directory** &gt; **licenze** &gt; **tutti i prodotti**, selezionare uno o più prodotti, quindi **Assegnare** hello barra dei comandi.

![Selezionare un tooassign di licenza](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

È possibile utilizzare hello **utenti e gruppi** toochoose pannello più utenti o gruppi o servizio toodisable piani nel prodotto hello. Utilizzare la casella di ricerca hello in toosearch superiore per i nomi utente e gruppo.

![Selezionare un utente o un gruppo per l'assegnazione di licenze](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Quando si desidera assegnare un gruppo di licenze tooa, può richiedere del tempo prima che tutti gli utenti ereditano licenza hello, in base al numero di hello di utenti nel gruppo di hello. È possibile controllare lo stato di elaborazione hello in hello **gruppo** pannello, hello **licenze** riquadro.

![Stato di assegnazione delle licenze](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Durante l'assegnazione di licenze di Azure AD, possono verificarsi errori di assegnazione, che però sono relativamente rari quando si gestiscono prodotti Azure AD ed Enterprise Mobility + Security. I potenziali errori di assegnazione sono limitati a:
- Conflitto di assegnazione: quando un utente è stato precedentemente assegnato una licenza che non è compatibile con la licenza corrente di hello. In questo caso, l'assegnazione di nuova licenza hello richiede la rimozione di hello corrente.
- Superato le licenze disponibili: quando il numero di hello degli utenti in gruppi assegnati supera le licenze disponibili hello, lo stato di assegnazione di un utente riflette tooassign un errore a causa di toomissing licenze.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Licenze per Collaborazione B2B di Azure AD

Collaborazione B2B consente agli utenti guest tooinvite in Azure AD tenant tooprovide accesso tooAzure AD servizi e le risorse di Azure si rende disponibile.  

Non è previsto alcun addebito per invitare gli utenti B2B e assegnando loro tooan applicazione in Azure AD. Le applicazioni too10 per guest 3 report di base e di utente sono anche gratuito per gli utenti di collaborazione B2B. Se l'utente guest dispone di licenze appropriate assegnate nel tenant di Azure AD del partner di hello, essi verrà anche licenza in quelle in uso.

Non è obbligatorio, ma se si desidera tooprovide accedere alle funzionalità di Azure AD toopaid, devono avere la licenza agli utenti guest B2B con le licenze di Azure Active Directory appropriate. Un tenant con Azure Active Directory a pagamento licenza invitare possa assegnare diritti utente di collaborazione B2B utenti guest tooan cinque aggiuntive invitati toohello tenant. Per scenari e informazioni, vedere [Linee guida sulla Collaborazione B2B di Azure Active Directory](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Visualizzare licenze assegnate

In **Azure Active Directory** &gt; **Licenze** &gt; **Tutti i prodotti** è visualizzato un riepilogo delle licenze assegnate e disponibili.

![Visualizzare il riepilogo delle licenze](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Quando si seleziona un prodotto specifico, è disponibile un elenco dettagliato di utenti e gruppi assegnati. Hello **utenti con licenza** sono elencati tutti gli utenti che attualmente utilizzano una licenza e se la licenza hello è stata assegnata direttamente toohello utente o se viene ereditato da un gruppo.

![Visualizzare i dettagli delle licenze](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Analogamente, hello **concesso in licenza gruppi** sono elencati tutti i gruppi di licenze toowhich sono state assegnate. Selezionare un utente o gruppo hello di tooopen **licenze** pannello, che mostra tutte le licenze assegnate toothat oggetto.

### <a name="remove-a-license"></a>Rimuovere una licenza

tooremove una licenza, visitare toohello utente o gruppo e aprire hello **licenze** riquadro. Selezionare hello licenza e fare clic su **rimuovere**.

![Rimuovere una licenza](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Impossibile rimuovere direttamente ereditate da utente hello da un gruppo di licenze. In alternativa, è possibile rimuovere utente hello dal gruppo di hello da cui si sta ereditando licenza hello.

### <a name="extend-trials"></a>Estendere le versioni di valutazione

Le estensioni di valutazione per i clienti sono disponibili come iscriversi tramite il portale di Office 365 hello Self-Service. Un amministratore del cliente è possibile passare il portale di Office toohello (accesso dipende dalle autorizzazioni per il portale di Office hello) e selezionare una versione di valutazione di Azure AD Premium hello. Facendo clic su hello **estendere versione di valutazione** collegamento Avvia il processo di estensione hello. È necessaria una carta di credito, ma non viene addebitata alcuna somma.

![Estendere una versione di valutazione di hello portale di Azure](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Passaggi successivi

altre informazioni sulle toolearn avanzate scenari per la gestione delle licenze tramite i gruppi, leggere l'articolo di hello [gruppo tooa di assegnazione licenze](active-directory-licensing-group-assignment-azure-portal.md).

Informazioni su come tooconfigure e utilizzare altre AD Azure le funzionalità a pagamento:

* [Reimpostazione della password self-service](active-directory-manage-passwords.md)
* [Gestione di gruppi self-service](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Acquisto diretto di licenze di Azure AD Premium](http://aka.ms/buyaadp)
