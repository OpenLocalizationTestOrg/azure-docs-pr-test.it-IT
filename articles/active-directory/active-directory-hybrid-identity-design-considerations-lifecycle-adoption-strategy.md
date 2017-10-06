---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare strategia di adozione del ciclo di vita di identità ibrida | Documenti Microsoft"
description: "Consente di definire le attività di gestione delle identità di hello ibrida toohello opzioni disponibili per ogni fase del ciclo di vita di base."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Determinare la strategia di adozione del ciclo di vita della soluzione ibrida di gestione delle identità
In questa attività verranno definite strategia di gestione di identità hello ai ibrida identità soluzione toomeet hello requisiti aziendali definiti in [determinare l'attività di gestione identità ibride](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

toodefine hello ibrida identità attività di gestione in base toohello ciclo di vita delle identità end-to-end riportata in precedenza in questo passaggio, sarà necessario tooconsider hello le opzioni disponibili per ogni fase del ciclo di vita.

## <a name="access-management-and-provisioning"></a>Gestione e provisioning degli accessi
Una soluzione di gestione di accesso account valido, l'organizzazione possibile tenere traccia con precisione che dispone di informazioni di accesso toowhat organizzazione hello.

Il controllo di accesso è una funzione critica di un sistema di provisioning centralizzato. Oltre a proteggere le informazioni sensibili, il controllo di accesso espone gli account esistenti con autorizzazioni non approvate o non più necessari. account obsoleta toocontrol, hello provisioning system collegamenti contemporaneamente informazioni dell'account con le informazioni autorevoli utenti hello proprietari di account hello. Informazioni sull'identità attendibile viene mantenute in genere nei database di hello e le directory delle risorse umane.

Gli account di aziende del settore IT complesse includono centinaia di parametri che definiscono l'autorità di hello e queste informazioni possono essere controllate dal sistema di provisioning. Nuovi utenti possono essere identificati con dati hello forniti dall'origine autorevole hello. funzionalità di approvazione richiesta di accesso Hello avvia i processi di hello che approvano il provisioning per le risorse (o rifiutano).

| Fase di gestione del ciclo di vita | Locale | Cloud | Ibrido |
| --- | --- | --- | --- |
| Gestione e provisioning degli account |Con ruolo hello del server Servizi di dominio Active Directory® (AD DS), è possibile creare un'infrastruttura scalabile, sicura e gestibile per utente e la gestione delle risorse e forniscono il supporto per applicazioni quali Microsoft® Exchange Server. <br><br> [È possibile eseguire il provisioning dei gruppi in Servizi di dominio Active Directory tramite un Identity manager](https://technet.microsoft.com/library/ff686261.aspx) <br>[ È possibile eseguire il provisioning degli utenti in Servizi di dominio Active Directory](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Gli amministratori possono utilizzare le risorse tooshared di accesso utente di accesso controllo toomanage per motivi di sicurezza. In Active Directory, il controllo di accesso viene amministrato a livello di oggetto hello dall'impostazione di diversi livelli di accesso o le autorizzazioni, tooobjects, ad esempio controllo completo, scrittura, lettura o non consente l'accesso. Il controllo di accesso in Active Directory definisce il modo in cui gli utenti possono usare gli oggetti di Active Directory. Per impostazione predefinita, le autorizzazioni per oggetti in Active Directory sono toohello un'impostazione più sicura. |Toocreate avere un account per tutti gli utenti che avranno accesso a un servizio cloud Microsoft. È anche possibile modificare gli account utente oppure eliminarli quando non sono più necessari. Per impostazione predefinita, gli utenti non hanno autorizzazioni di amministratore, ma è possibile scegliere facoltativamente di assegnarle. Per altre informazioni, vedere [Gestione degli utenti in Azure AD](active-directory-create-users.md). <br><br> All'interno di Azure Active Directory, una delle funzionalità principali di hello è hello possibilità toomanage accesso tooresources. Queste risorse possono far parte della directory di hello, come nel caso di hello oggetti toomanage autorizzazioni tramite ruoli nella directory hello o risorse che sono directory toohello esterno, ad esempio applicazioni SaaS, servizi di Azure e siti di SharePoint o in locale risorse. <br><br> In hello soluzione di gestione accesso center di Azure Active Directory è il gruppo di sicurezza di hello. proprietario della risorsa Hello (o messaggio per l'amministratore della directory hello) possibile assegnare tooprovide un gruppo una determinate risorse di destra toohello accesso che sono proprietari. i membri del gruppo di hello Hello verranno forniti accesso hello e proprietario della risorsa hello possibile delegare l'elenco dei membri hello toomanage destra hello di un gruppo di toosomeone altri, ad esempio un responsabile del reparto o un amministratore di help desk<br> <br> gruppi di gestione di Hello in Azure AD argomento vengono fornite ulteriori informazioni sulla gestione di accesso tramite i gruppi. |Estendere le identità di Active Directory nel cloud hello tramite la sincronizzazione e la federazione |

## <a name="role-based-access-control"></a>Controllo degli accessi in base al ruolo
Controllo di accesso basato sui ruoli (RBAC) vengono utilizzati i ruoli e provisioning tooevaluate criteri, test e applicare i processi di business e le regole per la concessione dell'accesso toousers. Gli amministratori chiavi creare criteri di provisioning e assegnare gli utenti tooroles e che definiscono i set di diritti tooresources per questi ruoli. RBAC estende hello identità soluzione toouse basata su software processi di gestione e ridurre l'intervento manuale nel processo di provisioning hello.
Azure AD RBAC consente hello società toorestrict hello massima per le operazioni che un singolo può eseguire una volta che ha accesso tooAzure portale di gestione. Utilizzando portale toohello di RBAC toocontrol accesso, gli amministratori IT ca l'accesso delegato tramite hello seguendo la gestione degli accessi approcci:

* **Assegnazione di ruolo in base al gruppo**: È possibile assegnare l'accesso tooAzure AD gruppi che possono essere sincronizzati da Active Directory locale. In questo modo tooleverage hello investimenti effettuati in strumenti e processi per la gestione dei gruppi dell'organizzazione. È inoltre possibile utilizzare funzionalità di gestione gruppi delegata hello di Azure AD Premium.
* **Usare compilate con i ruoli in Azure**: È possibile utilizzare tre ruoli: tooensure proprietario, collaboratore e lettore, che gli utenti e gruppi dispongono di autorizzazioni toodo attività hello solo devono toodo i processi.
* **Accesso granulare tooresources**: È possibile assegnare ruoli toousers e gruppi per una determinata sottoscrizione, gruppo di risorse o una singola risorsa di Azure, ad esempio un sito Web o di un database. In questo modo, è possibile garantire che gli utenti accedere alle risorse di hello tooall che devono e non tooresources di accesso che non richiedono toomanage.

## <a name="provisioning-and-other-customization-options"></a>Provisioning e altre opzioni di personalizzazione
Il team può usare toodecide piani e i requisiti di business quanto soluzione di identità toocustomize hello. Ad esempio, per i flussi di lavoro e gli adattatori personalizzati una grande impresa può richiedere un piano di implementazione a fasi basato su una sequenza temporale per eseguire il provisioning delle applicazioni usate più di frequente per varie aree geografiche in modo incrementale. Per due o più toobe applicazioni il provisioning nell'intera organizzazione, dopo aver completato il test, potrebbe fornire un altro piano di personalizzazione. È possibile personalizzare l'interazione dell'utente dell'applicazione e procedure per il provisioning di risorse potrebbero essere modificate tooaccommodate automatizzata provisioning.

È possibile eseguire il deprovisioning tooremove un servizio o componente. Deprovisioning di un account, ad esempio, significa che l'account hello viene eliminato da una risorsa.

modello ibrido Hello del provisioning delle risorse combina richiesta e gli approcci basata su ruoli, che sono supportati da Azure AD. Per un sottoinsieme di dipendenti o i sistemi gestiti, un'azienda potrebbe essere necessario tooautomate accesso con l'assegnazione basata su ruoli. oppure di gestire tutte le altre eccezioni o richieste di accesso tramite un modello basato sulla richiesta. Altre aziende possono invece iniziare con l'assegnazione manuale per poi evolvere verso un modello ibrido, con l'intenzione di effettuare una distribuzione completamente basata sul ruolo in futuro.

Altre società potrebbe risultare poco pratico per business motivi tooachieve basata su ruoli provisioning completo e un approccio ibrido di destinazione come obiettivo desiderato. Ancora altre società potrebbe essere soddisfatto con provisioning basato solo su richiesta e non desidera tooinvest sforzo aggiuntivo toodefine e gestire i criteri di provisioning automatici, in base al ruolo.

## <a name="license-management"></a>Gestione licenze
Gestione delle licenze in base al gruppo in Azure AD consente agli amministratori di assegnare il gruppo di sicurezza tooa utenti e AD Azure assegna automaticamente le licenze appartenenti a hello tooall hello gruppo. Se un utente viene successivamente aggiunti o rimossi dal gruppo di hello, una licenza verrà automaticamente assegnata o rimosso come appropriata.

È possibile usare i gruppi sincronizzati da Active Directory locale o gestiti in Azure AD e Associazione di questo con Azure AD premium, gestione dei gruppi Self-Service è possibile delegare licenza assegnazione toohello responsabili appropriati. È garantito che problemi quali conflitti di licenze e dati mancanti per la località vengono risolti automaticamente.

## <a name="self-regulating-user-administration"></a>Regolazione automatica dell'amministrazione degli utenti
Quando l'organizzazione inizia tooprovision risorse in tutte le organizzazioni interne, è implementare funzionalità di amministrazione utente regola automaticamente hello. Limiti dell'organizzazione, è possibile ottenere vantaggi hello e i vantaggi di provisioning utenti. In questo ambiente, una modifica dello stato di un utente si riflette automaticamente nei diritti di accesso in tutta l'organizzazione e in tutte le aree geografiche. È possibile ridurre i costi di provisioning e semplificare i processi di accesso e l'approvazione di hello. implementazione di Hello che realizza una potenzialità hello di implementazione del controllo di accesso basato sui ruoli per la gestione accessi end-to-end all'interno dell'organizzazione. Favorisce la riduzione dei costi amministrativi tramite procedure automatizzate che regolamentano il provisioning degli utenti. Migliora la sicurezza grazie all'automazione dell'imposizione dei criteri di sicurezza, alla semplificazione e alla centralizzazione del ciclo di vita degli utenti e al provisioning delle risorse per grandi quantità di utenti.

> [!NOTE]
> Per altre informazioni, vedere Configurazione di Azure AD per la gestione self-service dell'accesso alle applicazioni
> 
> 

I servizi di Azure AD basati su licenza o diritti funzionano attivando una sottoscrizione nel tenant di directory/servizio di Azure AD. Una volta hello sottoscrizione è attiva funzionalità del servizio di hello può essere gestito dagli amministratori o servizi di directory e utilizzati dagli utenti con licenza. Per altre informazioni, vedere la sezione Come funzionano le licenze di Azure AD?
Integrazione con altri provider di terze parti

Azure Active Directory fornisce single sign-in e migliorato toothousands di sicurezza di accesso dell'applicazione di applicazioni SaaS e applicazioni web locali. Per un elenco dettagliato di una raccolta di applicazioni Azure Active Directory per applicazioni SaaS supportate, vedere l'elenco di compatibilità di Azure Active Directory federation: provider di identità di terze parti che possono essere utilizzati tooimplement accesso single sign-on

## <a name="define-synchronization-management"></a>Definire la soluzione di gestione della sincronizzazione
L'integrazione delle directory locali con Azure AD rende gli utenti più produttivi in quanto fornisce un'identità comune per accedere alle risorse cloud e locali. Con questa integrazione utenti e organizzazioni possono sfruttare seguente hello:

* Le organizzazioni possono consentire agli utenti con un'identità ibrida comune in locale o servizi basati su cloud utilizzando Windows Server Active Directory e quindi connettersi tooAzure Active Directory.
* Gli amministratori possono fornire l'accesso condizionale in base alla risorsa dell'applicazione, al dispositivo e all'identità utente, al percorso di rete e all'autenticazione a più fattori.
* Gli utenti possono utilizzare la propria identità comune tramite gli account di Azure AD tooOffice 365, Intune, le app SaaS e applicazioni di terze parti.
* Gli sviluppatori possono compilare applicazioni che sfruttano modello di identità comune hello, integrazione di applicazioni in Active Directory locale o in Azure per le applicazioni basate su cloud

Hello nella figura seguente è un esempio di una vista di alto livello del processo di sincronizzazione delle identità.

![](./media/hybrid-id-design-considerations/identitysync.png)

Processo di sincronizzazione delle identità

Esaminare hello tabella toocompare hello sincronizzazione le opzioni seguenti:

| Opzione di gestione della sincronizzazione | Vantaggi | Svantaggi: |
| --- | --- | --- |
| Basata sulla sincronizzazione (tramite DirSync o AAD Connect) |Utenti e gruppi sincronizzati in locale e su cloud <br>  **Controllo dei criteri**: è possibile impostare i criteri di Account tramite Active Directory, che fornisce i criteri di password toomanage hello amministratore hello possibilità, workstation, restrizioni, i controlli di blocco e altri, senza la necessità di tooperform aggiuntive attività cloud hello.  <br>  **Controllo di accesso**: possibile limitare l'accesso toohello cloud servizio in modo che i servizi di hello è possibile accedere tramite l'ambiente aziendale hello, tramite server online o entrambi. <br>  Riduzione delle chiamate al supporto tecnico: se gli utenti dispongono di meno tooremember le password, sono tooforget meno probabile che li. <br>  Sicurezza: Informazioni di identità e degli utenti vengono protette perché tutti i server di hello e servizi utilizzati in single sign-on, vengono gestiti e controllati in locale. <br>  Supporto per l'autenticazione avanzata: È possibile utilizzare l'autenticazione avanzata (detto anche autenticazione a due fattori) con il servizio cloud hello. In tal caso, però, sarà necessario usare l'accesso Single Sign-On. | |
| Basata su federazione (tramite AD FS) |Abilitata tramite il servizio token di sicurezza. Quando si configura un servizio token di sicurezza tooprovide accesso single sign-on con un servizio cloud Microsoft, verrà creata una relazione di trust federativa tra il servizio token di sicurezza locale e il dominio federato di hello specificato nel tenant di Azure AD. <br> Consente agli utenti finali hello toouse stesso insieme di credenziali tooobtain accedere toomultiple alle risorse <br>gli utenti finali non è necessario toomaintain più set di credenziali. Ancora, gli utenti di hello hanno tooprovide tooeach loro credenziali uno di hello partecipanti risorse., B2B e B2C scenari supportati. |Richiede personale specializzato per la distribuzione e la manutenzione di server AD FS locali dedicati. Se si prevede di toouse ADFS per il servizio token di sicurezza, esistono restrizioni sull'utilizzo di hello dell'autenticazione avanzata. Per altre informazioni, vedere [Configurazione delle opzioni avanzate per AD FS 2.0](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Per altre informazioni, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

