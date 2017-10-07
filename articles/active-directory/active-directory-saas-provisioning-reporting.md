---
title: Creazione di report per applicazioni tooSaaS di provisioning dell'account Azure Active Directory utente automatico | Documenti Microsoft
description: Informazioni su come toocheck hello lo stato dei processi di provisioning dell'account utente automatica e come tootroubleshoot hello provisioning di singoli utenti.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>Esercitazione: creazione di report sul provisioning automatico degli account utente


Azure Active Directory include un [servizio di provisioning dell'account utente](active-directory-saas-app-provisioning.md) che consente di automatizzare hello provisioning deallocare provisioning degli account utente in App SaaS e altri sistemi, a scopo di hello del ciclo di vita delle identità end-to-end gestione. Azure AD supporta connettori per tutte le applicazioni di hello e sistemi nella sezione "In primo piano" hello di hello il provisioning degli utenti preintegrati [raccolta di applicazioni Azure AD](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).

In questo articolo viene descritto come stato hello toocheck di provisioning di processi dopo che sono stati impostati come e un massimo di provisioning hello tootroubleshoot di singoli utenti e gruppi.

## <a name="overview"></a>Panoramica

I connettori di provisioning vengono impostati principalmente e configurata tramite hello [portale di gestione di Azure](https://portal.azure.com), dal seguente hello [fornita documentazione](active-directory-saas-tutorial-list.md) per un'applicazione hello in utente provisioning account desiderata. Dopo averli configurati e averne avviata l'esecuzione, i processi di provisioning per un'applicazione possono essere segnalati tramite uno dei due metodi indicati:

* **Portale di gestione di Azure** -principalmente in questo articolo viene descritto il recupero delle informazioni di report da hello [portale di gestione di Azure](https://portal.azure.com), che fornisce sia un report di riepilogo di provisioning, nonché provisioning dettagliate controllare i registri per una determinata applicazione.

* **Audit API** -Azure Active Directory fornisce inoltre un'API che consente il recupero a livello di codice di hello dettagliate provisioning dei registri di controllo. Vedere [il controllo di Azure Active Directory di riferimento all'API](active-directory-reporting-api-audit-reference.md) per la documentazione specifica toousing questa API. Mentre nell'articolo vengono descritte in modo specifico come toouse hello API, dettaglio tipi hello di provisioning gli eventi registrati nel log di controllo hello.

### <a name="definitions"></a>Definizioni

In questo articolo Usa hello seguenti termini, definiti di seguito:

* **Sistema di origine** -consente la sincronizzazione da repository hello di utenti che hello servizio provisioning di Azure AD. Azure Active Directory è il sistema di origine hello per la maggior parte hello di pre-integrata provisioning connettori, esistono tuttavia alcune eccezioni (esempio: la sincronizzazione in ingresso Workday).

* **Sistema di destinazione** -Sincronizza repository hello di utenti che hello servizio provisioning di Azure AD a. Si tratta in genere un'applicazione SaaS (esempi: Salesforce, ServiceNow, Google Apps, Dropbox for Business), ma in alcuni casi può essere un sistema locale, ad esempio Active Directory (esempio: la sincronizzazione in ingresso Workday tooActive Directory).


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>Recupero di provisioning report dal portale di gestione di Azure hello

tooget informazioni sui report per una determinata applicazione, il provisioning iniziale avviando hello [portale di gestione di Azure](https://portal.azure.com) e l'esplorazione dell'applicazione Enterprise toohello per cui è configurato il provisioning. Ad esempio, se si esegue il provisioning utenti tooLinkedIn Esegui con privilegi elevati, dettagli applicazione toohello del percorso di navigazione hello è:

**Azure Active Directory &gt; Applicazioni aziendali &gt; All applications (Tutte le applicazioni) &gt; LinkedIn Elevate**

Da qui è possibile accedere a report di riepilogo Provisioning hello e registri di controllo di provisioning hello, entrambi descritti di seguito.


### <a name="provisioning-summary-report"></a>Report di riepilogo del provisioning

Hello provisioning report di riepilogo è visibile in hello **Provisioning** per la scheda specificata dell'applicazione. Si trova nella sezione Dettagli sincronizzazione hello sotto **impostazioni**, nonché hello le seguenti informazioni:

* Hello numero totale di utenti e gruppi che sono stati sincronizzati e sono attualmente nell'ambito per il provisioning tra il sistema di origine hello e sistema di destinazione hello.

* Hello ultima hello sincronizzazione è stata eseguita. Le sincronizzazioni in genere vengono eseguite ogni 20-40 minuti, in seguito al totale completamento di una sincronizzazione.

* Eventuale completamento di una sincronizzazione iniziale.

* O meno il processo di provisioning hello è stato messo in quarantena e il motivo di hello per lo stato di quarantena hello è ad esempio (errore toocommunicate con il sistema di destinazione a causa di credenziali di amministratore tooinvalid)

Hello report di riepilogo di provisioning deve essere hello primo luogo admins aspetto toocheck in condizioni operative di hello del processo di provisioning hello.

 ![Report di riepilogo](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>Log di controllo del provisioning
Tutte le attività eseguite dal servizio hello vengono registrate nel log di controllo hello Azure AD, che può essere visualizzato in hello **log di controllo** scheda hello **Provisioning Account** categoria. I tipi di eventi dell'attività registrati includono:

* **Importare eventi** -un evento "import" viene registrato ogni volta che servizio provisioning hello Azure AD recupera informazioni su un singolo utente o gruppo da un sistema di origine o destinazione. Durante la sincronizzazione, gli utenti vengono recuperati dal sistema di origine hello in primo luogo, con risultati hello registrati come eventi "Importa". Hello ID corrispondenti di utenti hello recuperato vengono quindi eseguita una query su hello destinazione sistema toocheck se presenti, con risultati hello anche registrati come "importare" eventi. Questi eventi registrano tutti gli attributi di utente con mapping e i relativi valori che vengono rilevati dal servizio di provisioning hello Azure AD in fase di hello dell'evento hello. 

* **Eventi di regola di sincronizzazione** : questi eventi rapporti sui risultati di hello di regole di mapping di attributi hello e qualsiasi configurato i filtri di ambito, dopo aver importati i dati utente e valutati da sistemi di origine e destinazione hello. Ad esempio, se un utente in un sistema di origine è considerato toobe nell'ambito per il provisioning e toonot sostituto esiste nel sistema di destinazione hello, quindi questo evento registra il fatto che hello utente eseguire il provisioning nel sistema di destinazione hello. 

* **Esportare gli eventi** -un evento "export" viene registrato ogni volta che servizio provisioning hello Azure AD scrive un utente account o gruppo oggetto tooa sistema di destinazione. Questi eventi registrano tutti gli attributi utente e i relativi valori che sono stati scritti da hello servizio provisioning di Azure AD in fase di hello dell'evento hello. Se si è verificato un errore durante la scrittura di hello utente account o gruppo oggetto toohello sistema di destinazione, verrà visualizzato qui.

* **Elaborare gli eventi deposito** -escrows processo si verificano quando hello provisioning del servizio si verifica un errore durante il tentativo di un'operazione e avvia l'operazione di hello tooretry su un intervallo di Backoff di tempo. Ogni volta che un'operazione di provisioning viene ritirata viene registrato un evento "deposito".

Quando si esaminano gli eventi di provisioning per un singolo utente, gli eventi di hello si verificano in genere nell'ordine indicato:

1. Evento di importazione: utente viene recuperato dal sistema di origine hello.

2. Evento di importazione: sistema di destinazione è richiesto toocheck esistenza hello dell'utente hello recuperato.

3. Evento di regola di sincronizzazione: dati utente dai sistemi di origine e di destinazione vengono valutati per l'attributo hello configurata regole di mapping e toodetermine i filtri di ambito dell'azione, se presente, deve essere eseguita.

4. Evento di esportazione: se l'evento di regola di sincronizzazione hello determinato che un'azione deve essere eseguita (ad esempio Add, Update, Delete), quindi i risultati di hello di hello azione vengono registrati in un evento di esportazione.

![Creazione di un utente test di Azure AD](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>Cercare un utente specifico negli eventi di provisioning

Hello caso di utilizzo più comune per i log di controllo di provisioning hello è hello toocheck lo stato di un singolo account utente di provisioning. toolook hello ultimo provisioning di eventi per un utente specifico:

1. Passare toohello **log di controllo** sezione.

2. Da hello **categoria** dal menu **Provisioning Account**.

3. In hello **intervallo di Date** menu, hello selezionare intervallo di date toosearch,

4. In hello **ricerca** barra, immettere l'ID hello dell'utente hello desiderato toosearch per. formato di Hello del valore di ID deve corrispondere a qualsiasi è stata selezionata come hello corrispondenti all'ID primario nella configurazione del mapping dell'attributo hello (ad esempio, userPrincipalName o dipendente numero ID). il valore di ID Hello necessarie saranno visibile nella colonna destinazioni hello.

5. Premere INVIO toosearch. verrà restituita prima Hello provisioning eventi più recente.

6. Se gli eventi vengono restituiti, tenere presente i tipi di attività hello e ha avuto esito positivo o meno. Se viene restituito alcun risultato, significa che utente hello non esiste oppure non è ancora stata rilevata dal processo di provisioning se una sincronizzazione completa non è stato ancora completato hello.

7. Fare clic su singoli eventi dettagli tooview estesi, comprese tutte le proprietà utente che sono state recuperate, valutate o scritte come parte dell'evento hello.


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>Suggerimenti per la visualizzazione hello provisioning i log di controllo

Per facilitare la lettura in hello portale di Azure, selezionare hello **colonne** pulsante e scegliere le colonne:

* **Data** -Mostra hello data hello evento si è verificato.
* **Destinazioni** -Mostra hello app nome e l'ID utente che vengono utilizzati oggetti hello dell'evento hello.
* **Attività** -hello tipo di attività, come descritto in precedenza.
* **Stato** - indica se l'evento hello è o non riuscito.
* **Motivo stato** -un riepilogo di cosa sia accaduto nell'evento di provisioning hello.


## <a name="troubleshooting"></a>Risoluzione dei problemi

provisioning log di controllo e i report di riepilogo Hello svolge un ruolo chiave aiutare gli amministratori di risolvere i problemi di provisioning dell'account utente diversi.

Per informazioni aggiuntive basate su scenario sul tootroubleshoot automatico provisioning degli utenti, vedere [relativi alla configurazione e provisioning utenti tooan applicazione](active-directory-application-provisioning-content-map.md).


## <a name="additional-resources"></a>Risorse aggiuntive

* [Gestione del provisioning degli account utente per app aziendali](active-directory-enterprise-apps-manage-provisioning.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
