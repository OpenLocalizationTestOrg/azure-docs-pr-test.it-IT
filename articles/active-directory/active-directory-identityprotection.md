---
title: Azure Active Directory Identity Protection | Microsoft Docs
description: "Informazioni su come Azure AD Identity Protection consente di limitare la possibilità di un utente malintenzionato di sfruttare un'identità o un dispositivo compromesso e di proteggere un'identità o un dispositivo che in precedenza è stato sospettato o ritenuto essere compromesso."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: mtillman
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e66d033d95efccf53ea2de889b5811fe2eafb76a
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2018
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

Azure Active Directory Identity Protection è una funzionalità dell'edizione Azure AD Premium P2 che consente di:

- Rilevare le potenziali vulnerabilità per le identità dell'organizzazione

- Configurare risposte automatizzate alle azioni sospette rilevate correlate alle identità dell'organizzazione  

- Esaminare gli eventi imprevisti sospetti ed eseguire l'azione appropriata per risolverli   


## <a name="getting-started"></a>Introduzione

Microsoft protegge le identità basate sul cloud da oltre un decennio. Con Azure Active Directory Identity Protection, è possibile usare nell'ambiente gli stessi sistemi di protezione usati da Microsoft per proteggere le identità.

La maggior parte delle violazioni della sicurezza si verifica quando utenti malintenzionati ottengono l'accesso a un ambiente impadronendosi dell'identità di un utente. Nel corso degli anni, gli utenti malintenzionati hanno messo a punto tecniche sempre più efficaci per sfruttare le violazioni di terze parti e sferrare sofisticati attacchi di phishing. L'accesso a un account utente, anche quelli con privilegi limitati, permette agli utenti malintenzionati di accedere immediatamente a risorse aziendali importanti in modo relativamente semplice tramite il movimento laterale.

Di conseguenza, è necessario:

- Proteggere tutte le identità indipendentemente dal livello di privilegi

- Impedire in modo proattivo l'uso improprio delle identità compromesse

Trovare le identità compromesse non è un compito facile. Azure Active Directory usa l'euristica e gli algoritmi adattivi di apprendimento automatico per rilevare anomalie ed eventi imprevisti sospetti che indicano identità potenzialmente compromesse. Sulla base di tali dati, Identity Protection genera report e avvisi che consentono di valutare i problemi rilevati e di adottare le azioni di correzione o mitigazione appropriate.

Azure Active Directory Identity Protection è ben più di un semplice strumento di monitoraggio e reporting. Per proteggere le identità dell'organizzazione, è possibile configurare criteri basati sul rischio che rispondano automaticamente ai problemi rilevati quando viene raggiunto un livello di rischio specificato. Questi criteri, con altri controlli di accesso condizionale forniti da Azure Active Directory e da EMS, possono eseguire il blocco automatico o avviare azioni di correzione adattive, incluse la reimpostazione della password e l'applicazione dell'autenticazione a più fattori.


#### <a name="identity-protection-capabilities"></a>Funzionalità di Identity Protection

**Rilevamento di vulnerabilità e di account rischiosi:**  

* Raccomandazioni personalizzate per migliorare il comportamento di sicurezza in generale evidenziando le vulnerabilità.
* Calcolo dei livelli di rischio di accesso.
* Calcolo dei livelli di rischio utente.


**Analisi degli eventi di rischio:**

* Invio di notifiche per gli eventi di rischio.
* Analisi degli eventi di rischio con informazioni rilevanti e contestuali.
* Flussi di lavoro di base per tenere traccia delle analisi.
* Accesso semplificato ad azioni di correzione come la reimpostazione della password.

**Criteri di accesso condizionale basati sul rischio:**

* Criteri per mitigare gli accessi rischiosi con il blocco degli accessi o le richieste di autenticazione a più fattori
* Criteri per bloccare o proteggere gli account utente rischiosi.
* Criteri per richiedere la registrazione degli utenti per l'autenticazione a più fattori



## <a name="identity-protection-roles"></a>Ruoli di Identity Protection

Per bilanciare il carico delle attività di gestione per l'implementazione di Identity Protection, è possibile assegnare più ruoli. Azure AD Identity Protection supporta 3 ruoli di directory:

| Ruolo                         | Operazione consentita                          | Operazione non consentita
| :--                          | ---                                |  ---   |
| Amministratore globale         | Accesso completo a Identity Protection, implementazione di Identity Protection| |
| Amministratore della sicurezza       | Accesso completo a Identity Protection | Implementazione di Identity Protection, reimpostazione delle password per un utente |
| Ruolo con autorizzazioni di lettura per la sicurezza              | Accesso in sola lettura a Identity Protection | Implementazione di Identity Protection, correzione degli utenti, configurazione dei criteri, reimpostazione delle password |




Per altri dettagli, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Rilevamento

### <a name="vulnerabilities"></a>Vulnerabilità

Azure Active Directory Identity Protection analizza la configurazione e rileva le vulnerabilità che possono avere effetto sulle identità dell'utente. Per altri dettagli, vedere [Vulnerabilità rilevate da Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Eventi di rischio

Azure Active Directory usa l'euristica e algoritmi adattivi di apprendimento automatico per rilevare azioni sospette correlate alle identità dell'utente. Il sistema crea un record per ogni azione sospetta rilevata. Questi record sono denominati anche eventi di rischio.  
Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md).


## <a name="investigation"></a>Analisi
L'esperienza con Identity Protection inizia in genere dal relativo dashboard.

![Correzione](./media/active-directory-identityprotection/1000.png "Correzione")

Il dashboard consente di accedere a:

* Report, ad esempio **Utenti contrassegnati per il rischio**, **Eventi di rischio** e **Vulnerabilità**
* Impostazioni come la configurazione dei **criteri di sicurezza**, delle **notifiche** e della **registrazione per l'autenticazione a più fattori**

Si tratta in genere del punto di partenza dell'analisi, ovvero del processo di analisi di attività, log e altre informazioni rilevanti relative a un evento di rischio per decidere se sono necessarie procedure di correzione o mitigazione, se e come l'identità è stata compromessa e come è stata usata l'identità compromessa.

È possibile collegare le attività di analisi alle [notifiche](active-directory-identityprotection-notifications.md) che Azure Active Directory Protection invia per posta elettronica.

Le sezioni seguenti forniscono altre informazioni e i passaggi relativi a un'analisi.  


## <a name="risky-sign-ins"></a>Accessi a rischio

Azure Active Directory rileva i [tipi di eventi di rischio](active-directory-reporting-risk-events.md#risk-event-types) in tempo reale e offline. Ogni evento di rischio in tempo reale rilevato per un accesso di un utente rientra nel concetto logico degli accessi a rischio. Un accesso a rischio è indicativo di un tentativo di accesso che potrebbe non essere stato eseguito dal legittimo proprietario di un account utente.


### <a name="sign-in-risk-level"></a>Livello di rischio di un accesso

Il livello di rischio di un accesso è un'indicazione (Alto, Medio o Basso) della probabilità che un tentativo di accesso non sia stato eseguito dal legittimo proprietario di un account utente.

### <a name="mitigating-sign-in-risk-events"></a>Mitigazione degli eventi di rischio di accesso

La mitigazione è un'azione che consente di limitare la possibilità che un utente malintenzionato sfrutti un'identità o un dispositivo compromesso senza ripristinare l'identità o il dispositivo a uno stato sicuro. La mitigazione non risolve gli eventi di rischio di accesso precedenti associati all'identità o al dispositivo.

Per attenuare automaticamente gli accessi a rischio, è possibile configurare criteri di rischio per gli accessi. Usando questi criteri, si tiene conto del livello di rischio dell'utente o dell'accesso per bloccare gli accessi rischiosi o richiedere all'utente di eseguire l'autenticazione a più fattori. Queste azioni possono impedire a un utente malintenzionato di sfruttare un'identità rubata per causare danni e permettono di guadagnare tempo per proteggere l'identità.

### <a name="sign-in-risk-security-policy"></a>Criteri di sicurezza per il rischio di accesso
I criteri di rischio di accesso sono criteri di accesso condizionale che valutano il rischio associato a un accesso specifico e applicano le azioni di mitigazione in base a condizioni e regole predefinite.

![Criteri di rischio di accesso](./media/active-directory-identityprotection/1014.png "Criteri di rischio di accesso")

Azure AD Identity Protection consente di gestire le azioni di mitigazione degli accessi rischiosi seguendo questa procedura:

* Impostare gli utenti e i gruppi a cui vengono applicati i criteri:

    ![Criteri di rischio di accesso](./media/active-directory-identityprotection/1015.png "Criteri di rischio di accesso")
* Impostare la soglia del livello di rischio di accesso, bassa, media o alta, che attiva il criterio:

    ![Criteri di rischio di accesso](./media/active-directory-identityprotection/1016.png "Criteri di rischio di accesso")
* Impostare i controlli da applicare quando viene attivato il criterio:  

    ![Criteri di rischio di accesso](./media/active-directory-identityprotection/1017.png "Criteri di rischio di accesso")
* Cambiare lo stato dei criteri:

    ![Registrazione MFA](./media/active-directory-identityprotection/403.png "Registrazione MFA")
* Esaminare e valutare l'impatto di una modifica prima di attivarla:

    ![Criteri di rischio di accesso](./media/active-directory-identityprotection/1018.png "Criteri di rischio di accesso")

#### <a name="what-you-need-to-know"></a>Informazioni importanti
È possibile configurare un criterio di sicurezza per il rischio di accesso per richiedere l'autenticazione a più fattori:

![Criteri di rischio di accesso](./media/active-directory-identityprotection/1017.png "Criteri di rischio di accesso")

Tuttavia, per motivi di sicurezza, questa impostazione funziona soltanto per gli utenti che sono già stati registrati per l'autenticazione a più fattori. Se la condizione per richiedere l'autenticazione a più fattori risulta soddisfatta per un utente che non è ancora registrato per l'autenticazione a più fattori, tale utente viene bloccato.

Se si vuole richiedere l'autenticazione a più fattori per gli accessi rischiosi, è consigliabile procedere nel modo indicato di seguito:

1. Abilitare il [criterio di registrazione per l'autenticazione a più fattori](#multi-factor-authentication-registration-policy) per gli utenti interessati.
2. Richiedere agli utenti interessati di accedere in una sessione non rischiosa per eseguire la registrazione per l'autenticazione a più fattori

L'esecuzione di questa procedura assicura che, in caso di accesso rischioso, venga richiesta l'autenticazione a più fattori.

#### <a name="best-practices"></a>Procedure consigliate
La scelta di una soglia **alta** riduce la frequenza di attivazione dei criteri e riduce al minimo l'impatto sugli utenti.  

Tuttavia, esclude dai criteri gli accessi contrassegnati per il rischio con una soglia **bassa** o **media**. Questa scelta può non impedire a un utente malintenzionato di sfruttare un'identità compromessa.

Quando si impostano i criteri:

* Escludere gli utenti non hanno o non possono avere l'autenticazione a più fattori
* Escludere gli utenti con impostazioni locali in cui abilitare i criteri non è pratico, ad esempio per la mancanza di accesso al supporto tecnico
* Escludere gli utenti che possono generare molti falsi positivi, ad esempio sviluppatori o analisti della sicurezza
* Usare una soglia **alta** durante il rollout iniziale dei criteri o se è necessario ridurre al minimo gli avvisi visualizzati dagli utenti finali.
* Usare una soglia **bassa** se l'organizzazione richiede una maggiore sicurezza. La scelta di una soglia **bassa** introduce richieste di accesso aggiuntive per l'utente, ma garantisce una maggiore sicurezza.

L'impostazione predefinita consigliata per la maggior parte delle organizzazioni è la configurazione di una regola per una soglia **media** , che permette di bilanciare usabilità e sicurezza.

I criteri di rischio di accesso:

* Vengono applicati a tutto il traffico tramite browser e agli accessi che usano l'autenticazione moderna.
* Non vengono applicati alle applicazioni che usano protocolli di sicurezza meno recenti disabilitando l'endpoint WS-Trust in corrispondenza dell'IDP federato, ad esempio ADFS.

La pagina **Eventi di rischio** nella console di Identity Protection contiene un elenco di tutti gli eventi:

* Visualizzare a quali eventi sono stati applicati i criteri
* Esaminare l'attività e determinare se l'azione è stata appropriata o meno

Per una panoramica dell'esperienza utente correlata, vedere:

* [Ripristino di un accesso rischioso](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Accesso rischioso bloccato](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Esperienze di accesso con Azure AD Identity Protection](active-directory-identityprotection-flows.md)  

**Per aprire la relativa finestra di dialogo di configurazione**:

- Nel pannello **Azure AD Identity Protection** fare clic su **Criteri di rischio di accesso** nella sezione **Configura**.

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1014.png "Criteri di rischio utente")



## <a name="users-flagged-for-risk"></a>Utenti contrassegnati per il rischio

Tutti gli [eventi di rischio](active-directory-identity-protection-risk-events.md) attivi rilevati da Azure Active Directory per un utente rientrano nel concetto logico del rischio utente. Un utente contrassegnato per il rischio è indicativo di un account utente che potrebbe essere stato compromesso.

![Utenti contrassegnati per il rischio](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Livello di rischio utente

Il livello di rischio utente può essere Alto, Medio o Basso e indica la probabilità che l'identità dell'utente sia stata compromessa. Viene calcolato in base agli eventi di rischio utente associati all'identità di un utente.

Lo stato di un evento di rischio può essere **attivo** o **chiuso**. Solo gli eventi di rischio **attivi** vengono conteggiati nel calcolo del livello di rischio utente.

Il livello di rischio utente viene calcolato usando le informazioni seguenti:

* Eventi di rischio attivi che interessano l'utente.
* Livello di rischio di tali eventi.
* Eventuali azioni di correzione intraprese o meno.

![Rischi utente](./media/active-directory-identityprotection/1031.png "Rischi utente")

È possibile usare i livelli di rischio utente per creare criteri di accesso condizionale che bloccano l'accesso degli utenti a rischio o per fare in modo che modifichino la password in modo sicuro.

### <a name="closing-risk-events-manually"></a>Chiusura manuale degli eventi di rischio

Nella maggior parte dei casi, per chiudere automaticamente gli eventi di rischio si procede con azioni di correzione come la reimpostazione della password di protezione. Tuttavia, questo potrebbe non essere sempre possibile.  
Ad esempio quando:

* Un utente con eventi di rischio attivi è stato eliminato
* Un'analisi rivela che un evento di rischio segnalato è stato eseguito dall'utente legittimo

Dal momento che gli eventi di rischio **attivi** vengono conteggiati nel calcolo del rischio utente, potrebbe essere necessario ridurre il livello di rischio chiudendo manualmente gli eventi di rischio.  
Nel corso dell'analisi è possibile eseguire una qualsiasi di queste azioni per modificare lo stato di un evento di rischio:

![Azioni](./media/active-directory-identityprotection/34.png "Azioni")

* **Risolvi** : se è stata eseguita l'azione di correzione appropriata all'esterno di Identity Protection dopo l'analisi di un evento di rischio e si ritiene che l'evento sia da considerare chiuso, contrassegnarlo come risolto. Gli eventi risolti impostano lo stato dell'evento di rischio come chiuso e l'evento di rischio non viene più conteggiato nel rischio utente.
* **Contrassegna come falso positivo** : in alcuni casi è possibile analizzare un evento di rischio e scoprire che è stato erroneamente contrassegnato come rischioso. È possibile ridurre il numero di tali occorrenze contrassegnando l'evento di rischio come falso positivo. Questo permetterà agli algoritmi di Machine Learning di migliorare la classificazione di eventi simili in futuro. Lo stato dell'evento falso positivo viene impostato come **chiuso** e non viene più conteggiato nel rischio utente.
* **Ignora** : se non sono state intraprese azioni di correzione, ma si vuole rimuovere l'evento di rischio dall'elenco attivo, è possibile contrassegnarlo come da ignorare e il relativo stato verrà impostato come chiuso. Gli eventi ignorati non vengono conteggiati nel rischio utente. Questa opzione deve essere usata solo in circostanze particolari.
* **Riattiva**: gli eventi di rischio che sono stati chiusi manualmente mediante **Risolvi**, **Contrassegna come falso positivo** o **Ignora**, possono essere riattivati impostando nuovamente lo stato dell'evento su **Attivo**. Gli eventi di rischio riattivati vengono conteggiati nel calcolo del livello di rischio utente. Gli eventi di rischio chiusi tramite correzione, ad esempio la reimpostazione della password di protezione, non possono essere riattivati.

**Per aprire la relativa finestra di dialogo di configurazione**:

1. Nel pannello **Azure AD Identity Protection** fare clic su **Eventi di rischio** in **Ricerca causa**.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1002.png "Reimpostazione manuale della password")
2. Nell'elenco **Eventi di rischio** fare clic su un rischio.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1003.png "Reimpostazione manuale della password")
3. Nel pannello dei rischi fare clic con il pulsante destro del mouse su un utente.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1004.png "Reimpostazione manuale della password")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Chiusura manuale di tutti gli eventi di rischio per un utente
Invece di chiudere manualmente i singoli eventi di rischio per un utente, Azure Active Directory Identity Protection offre anche un metodo per chiudere tutti gli eventi per un utente con un solo clic.

![Azioni](./media/active-directory-identityprotection/2222.png "Azioni")

Quando si fa clic su **Dismiss all events**(Ignora tutti gli eventi), tutti gli eventi vengono chiusi e l'utente interessato non è più a rischio.

### <a name="remediating-user-risk-events"></a>Correzione di eventi di rischio utente

Una correzione è un'azione che consente di proteggere un'identità o un dispositivo che in precedenza è stato sospettato o ritenuto essere compromesso. Un'azione di correzione ripristina l'identità o il dispositivo a uno stato sicuro e risolve gli eventi di rischio precedenti associati all'identità o al dispositivo.

Per correggere gli eventi di rischio utente, è possibile:

* Eseguire una reimpostazione della password di protezione per correggere manualmente gli eventi di rischio utente
* Configurare criteri di sicurezza per il rischio utente per mitigare o correggere automaticamente gli eventi di rischio utente
* Ricreare l'immagine del dispositivo infetto  

#### <a name="manual-secure-password-reset"></a>Reimpostazione manuale della password di protezione
La reimpostazione della password di protezione un'azione di correzione efficace per molti eventi di rischio. Quando viene eseguita, permette di chiudere automaticamente gli eventi di rischio e ricalcolare il livello di rischio utente. È possibile usare il dashboard di Identity Protection per avviare una reimpostazione della password per un utente rischioso.

La finestra di dialogo correlata fornisce due metodi diversi per reimpostare una password:

**Reimposta password**: selezionare **Richiedi all'utente di reimpostare la password** per consentirgli di eseguire il ripristino automatico se è registrato per l'autenticazione a più fattori. Durante l'accesso successivo all'utente verrà richiesto di risolvere correttamente una richiesta di autenticazione a più fattori e quindi di modificare la password. Questa opzione non è disponibile se l'account utente non è già registrato per l'autenticazione a più fattori.

**Password provvisoria**: selezionare **Genera una password provvisoria** per annullare immediatamente la password esistente e creare una nuova password provvisoria per l'utente. Inviare la nuova password provvisoria a un indirizzo di posta elettronica alternativo dell'utente o al responsabile dell'utente. La password è provvisoria, quindi verrà richiesto all'utente di modificarla al momento dell'accesso.

![Criteri](./media/active-directory-identityprotection/1005.png "Criteri")

**Per aprire la relativa finestra di dialogo di configurazione**:

1. Nel pannello **Azure AD Identity Protection** fare clic su **Utenti contrassegnati per il rischio**.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1006.png "Reimpostazione manuale della password")
2. Dall'elenco di utenti selezionare un utente con almeno un evento di rischio.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1007.png "Reimpostazione manuale della password")
3. Nel pannello dell'utente fare clic su **Reimposta password**.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1008.png "Reimpostazione manuale della password")

### <a name="user-risk-security-policy"></a>Criteri di sicurezza per il rischio utente
I criteri di sicurezza per il rischio utente sono criteri di accesso condizionale che valutano il livello di rischio per un utente specifico e applicano azioni di correzione e mitigazione dei rischi in base a regole e condizioni predefinite.

![Criteri di rischio utente](./media/active-directory-identityprotection/1009.png "Criteri di rischio utente")

Azure AD Identity Protection consente di gestire le azioni di mitigazione e correzione per gli utenti contrassegnati per il rischio seguendo questa procedura:

* Impostare gli utenti e i gruppi a cui vengono applicati i criteri:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1010.png "Criteri di rischio utente")
* Impostare la soglia del livello di rischio utente, bassa, media o alta, che attiva il criterio:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1011.png "Criteri di rischio utente")
* Impostare i controlli da applicare quando viene attivato il criterio:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1012.png "Criteri di rischio utente")
* Cambiare lo stato dei criteri:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/403.png "Registrazione MFA")
* Esaminare e valutare l'impatto di una modifica prima di attivarla:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1013.png "Criteri di rischio utente")

La scelta di una soglia **alta** riduce la frequenza di attivazione dei criteri e riduce al minimo l'impatto sugli utenti.
Esclude tuttavia dai criteri gli utenti contrassegnati per il rischio con una soglia **bassa** o **media**. Questa scelta può non garantire la protezione delle identità o dei dispositivi in precedenza sospettati di essere compromessi o noti come compromessi.

Quando si impostano i criteri:

* Escludere gli utenti che possono generare molti falsi positivi, ad esempio sviluppatori o analisti della sicurezza
* Escludere gli utenti con impostazioni locali in cui abilitare i criteri non è pratico, ad esempio per la mancanza di accesso al supporto tecnico
* Usare una soglia **alta** durante il rollout iniziale dei criteri o se è necessario ridurre al minimo gli avvisi visualizzati dagli utenti finali.
* Usare una soglia **bassa** se l'organizzazione richiede una maggiore sicurezza. La scelta di una soglia **bassa** introduce richieste di accesso aggiuntive per l'utente, ma garantisce una maggiore sicurezza.

L'impostazione predefinita consigliata per la maggior parte delle organizzazioni è la configurazione di una regola per una soglia **media** , che permette di bilanciare usabilità e sicurezza.

Per una panoramica dell'esperienza utente correlata, vedere:

* [Flusso di ripristino di account compromessi](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Flusso di account compromessi bloccati](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**Per aprire la relativa finestra di dialogo di configurazione**:

- Nel pannello **Azure AD Identity Protection** fare clic su **Criteri di rischio utente** nella sezione **Configura**.

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1009.png "Criteri di rischio utente")

### <a name="mitigating-user-risk-events"></a>Mitigazione di eventi di rischio utente
Gli amministratori possono impostare criteri di sicurezza per il rischio utente per bloccare gli utenti al momento dell'accesso in base al livello di rischio.

Il blocco dell'accesso:

* Impedisce la generazione di nuovi eventi di rischio utente per l'utente interessato
* Consente agli amministratori di correggere manualmente gli eventi di rischio che interessano l'identità dell'utente e di ripristinarne lo stato protetto



## <a name="multi-factor-authentication-registration-policy"></a>Criteri di registrazione per l'autenticazione a più fattori
Azure Multi-Factor Authentication è un metodo di verifica dell'identità dell'utente che richiede l'uso di più fattori, oltre a un nome utente e una password. Fornisce un secondo livello di sicurezza agli accessi e alle transazioni degli utenti.  
È consigliabile richiedere l'autenticazione a più fattori per l'accesso degli utenti perché:

* Offre un'autenticazione avanzata con una gamma di opzioni di verifica semplici
* Svolge un ruolo chiave nella preparazione dell'organizzazione per le operazioni di protezione e ripristino in caso di compromissione degli account

![Criteri di rischio utente](./media/active-directory-identityprotection/1019.png "Criteri di rischio utente")

Per altre informazioni, vedere la pagina relativa ad [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection permette di gestire il rollout della registrazione per l'autenticazione a più fattori con la configurazione di criteri che consentono di:

* Impostare gli utenti e i gruppi a cui vengono applicati i criteri:

    ![Criteri MFA](./media/active-directory-identityprotection/1020.png "Criteri MFA")
* Impostare i controlli da applicare quando viene attivato il criterio:  

    ![Criteri MFA](./media/active-directory-identityprotection/1021.png "Criteri MFA")
* Cambiare lo stato dei criteri:

    ![Criteri MFA](./media/active-directory-identityprotection/403.png "Criteri MFA")
* Visualizzare lo stato di registrazione corrente:

    ![Criteri MFA](./media/active-directory-identityprotection/1022.png "Criteri MFA")

Per una panoramica dell'esperienza utente correlata, vedere:

* [Flusso di registrazione per l'autenticazione a più fattori](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Esperienze di accesso con Azure AD Identity Protection](active-directory-identityprotection-flows.md).  

**Per aprire la relativa finestra di dialogo di configurazione**:

- Nel pannello **Azure AD Identity Protection** fare clic su **Criteri di registrazione per l'autenticazione a più fattori** nella sezione **Configura**.

    ![Criteri MFA](./media/active-directory-identityprotection/1019.png "Criteri MFA")

## <a name="next-steps"></a>Passaggi successivi
* [Channel 9: Azure AD and Identity Show: Identity Protection Preview](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Abilitazione di Azure Active Directory Identity Protection](active-directory-identityprotection-enable.md)

* [Vulnerabilità rilevate da Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md)

* [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md)

* [Notifiche di Azure Active Directory Identity Protection](active-directory-identityprotection-notifications.md)

* [Studio di Azure Active Directory Identity Protection](active-directory-identityprotection-playbook.md)

* [Glossario di Azure Active Directory Identity Protection](active-directory-identityprotection-glossary.md)

* [Esperienze di accesso con Azure AD Identity Protection](active-directory-identityprotection-flows.md)

* [Azure Active Directory Identity Protection: come sbloccare gli utenti](active-directory-identityprotection-unblock-howto.md)

* [Introduzione ad Azure Active Directory Identity Protection e a Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
