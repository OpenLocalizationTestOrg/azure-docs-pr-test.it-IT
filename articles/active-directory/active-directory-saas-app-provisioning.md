---
title: aaaAutomated SaaS app provisioning degli utenti in Azure AD | Documenti Microsoft
description: "Toohow un'introduzione è possibile usare il provisioning di tooautomatically di Azure AD, deprovisioning e aggiornare continuamente gli account utente in più applicazioni SaaS di terze parti."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>Automatizzare il provisioning e deprovisioning tooSaaS applicazioni con Azure Active Directory
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>Informazioni sul provisioning utenti automatizzato per app SaaS
Azure Active Directory (Azure AD) consente la creazione di hello tooautomate, la manutenzione e la rimozione delle identità utente nel cloud ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) le applicazioni, ad esempio Dropbox, Salesforce, ServiceNow e altro ancora.

**Di seguito sono riportati alcuni esempi di ciò che questa funzionalità permette toodo:**

* Crea automaticamente nuovi account in hello App SaaS corrette per i nuovi utenti quando accedono al team.
* Quando gli utenti lasciano inevitabilmente team di hello verrà disattivato automaticamente gli account da app SaaS.
* Verificare che le identità hello nelle App SaaS siano mantenute backup toodate in base alle modifiche nella directory hello.
* Eseguire il provisioning di oggetti non utente, ad esempio gruppi, le app tooSaaS che li supportano.

**Il provisioning utenti automatizzato include anche hello seguenti funzionalità:**

* Hello le identità esistenti possibilità toomatch tra Azure AD e le app SaaS.
* Opzioni di personalizzazione toohelp AD Azure adatta configurazioni correnti di hello di App SaaS hello che l'organizzazione è attualmente in uso.
* Avvisi di posta elettronica facoltativi per errori di provisioning.
* Creazione di report e attività toohelp registri con monitoraggio e risoluzione dei problemi.

## <a name="why-use-automated-provisioning"></a>Perché usare il provisioning automatico?
Di seguito sono riportate alcune motivazioni comuni per l'uso di questa funzionalità:

* i costi di hello tooavoid inefficienze ed errori umani associato ai processi di provisioning manuale.
* l'organizzazione rimuovendo immediatamente le identità degli utenti da toosecure chiave App SaaS quando escono dalla organizzazione hello.
* tooeasily importare un numero di massa di utenti in una particolare applicazione SaaS.
* praticità hello tooenjoy che la soluzione di provisioning eseguito da hello stessi criteri di accesso app definite per Azure AD Single Sign-On.

## <a name="frequently-asked-questions"></a>Domande frequenti
**Frequenza con cui Azure AD scrivere app SaaS toohello modifiche di directory?**

Azure AD Verifica presenza di modifiche ogni cinque minuti tooten. Se l'applicazione SaaS hello restituisce diversi errori (ad esempio in caso di hello di credenziali di amministratore non valida), gradualmente Azure AD rallenterà relativo tooonce tooup frequenza per ogni giorno fino a quando non saranno corretti hello.

**Quanto tempo sarà necessario tooprovision gli utenti?**

Le modifiche incrementali verificarsi quasi istantaneamente ma se si tenta di tooprovision la maggior parte delle directory, quindi dipende dal numero di hello di utenti e gruppi di cui si dispone. Per le directory di piccole dimensioni sono necessari solo pochi minuti, per le directory di medie dimensioni alcuni minuti e per le directory di grandi dimensioni potrebbero essere necessarie diverse ore.

**Come posso tenere traccia corso hello del processo di provisioning corrente hello?**

È possibile esaminare hello Report Provisioning degli Account nella sezione report hello della directory. Un'altra opzione è toovisit hello applicazione SaaS che si esegue il provisioning della scheda Dashboard hello e guarda sotto la sezione "Integrazione con stato" nella parte inferiore di hello della pagina hello hello.

**Come è possibile determinare se gli utenti non tooget il provisioning in modo corretto?**

Alla fine hello hello provisioning guidato di configurazione vi è una notifica di tooemail toosubscribe opzione per il provisioning di errori. È inoltre possibile controllare gli utenti che non è stato possibile toobe il provisioning di hello Report degli errori di Provisioning toosee e sul motivo.

**Azure AD scrivere le modifiche dalla directory di backup toohello app SaaS hello?**

Per la maggior parte delle applicazioni SaaS, il provisioning è solo in uscita, il che significa che gli utenti vengono scritte da un'applicazione hello directory toohello e le modifiche apportate da un'applicazione hello non possono essere scritta toohello directory. Per [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), tuttavia, il provisioning è solo in ingresso, il che significa che gli utenti siano importati nella directory hello da Workday e allo stesso modo, le modifiche nella directory di hello non ottenere scritta in Workday.

**Come è possibile inviare i team di progettazione toohello di commenti e suggerimenti?**

Contattare Microsoft tramite hello [forum sul feedback su Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>Come funziona il provisioning automatizzato?
Azure AD esegue il provisioning utenti tooSaaS App connettendo endpoint tooprovisioning fornite da ogni fornitore dell'applicazione. Questi endpoint consentono di Azure AD tooprogrammatically creare, aggiornare e rimuovere utenti. Di seguito è fornita una breve panoramica di hello diversi passaggi che Azure AD accetta tooautomate provisioning.

1. Quando si abilita il provisioning di un'applicazione hello per la prima volta, viene eseguita hello seguenti azioni:
   * Azure Active Directory tenterà toomatch agli utenti esistenti con le identità corrispondenti nella directory hello app SaaS hello. Quando c’è una corrispondenza per un utente è una corrispondenza, *non* è automaticamente abilitato per il servizio di single sign-on. Affinché un'applicazione di toohello utente toohave accesso, si deve essere assegnati esplicitamente toohello app in Azure AD, direttamente o tramite l'appartenenza al gruppo.
   * Se sono già stati specificati gli utenti che devono essere assegnati toohello applicazione e Azure AD ha esito negativo toofind account esistenti per gli utenti, Azure AD verrà effettuare il provisioning di nuovi account per tali in un'applicazione hello.
2. Dopo aver completata la sincronizzazione iniziale di hello come descritto in precedenza, Azure AD verificherà ogni 10 minuti per hello seguenti modifiche:
   * Se i nuovi utenti sono stati assegnati applicazione toohello (direttamente o tramite l'appartenenza al gruppo), quindi sarà eseguito il provisioning di un nuovo account di app SaaS hello.
   * Se l'accesso dell'utente è stato rimosso, il relativo account in app SaaS hello verrà contrassegnato come disabilitato (gli utenti sono mai completamente rimossi, che impedisce la perdita di dati nell'evento hello di un errore di configurazione).
   * Se si dispone già di un account di hello applicazione SaaS che l'account verrà contrassegnato come abilitato e alcune proprietà utente possono essere aggiornate se sono scadute toohello confrontati directory applicazione toohello recentemente è stato assegnato un utente.
   * Se le informazioni dell'utente (ad esempio il numero di telefono ufficio, e così via) sono state modificate nella directory di hello, tali informazioni anche essere aggiornate in hello applicazione SaaS.

Per ulteriori informazioni sulla modalità di mapping tra Azure AD attributi e app SaaS, vedere l'articolo hello in [personalizzazione dei mapping di attributi](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Elenco di applicazioni che supportano il provisioning utenti automatizzato
Tutte le app "In primo piano" hello nella raccolta di applicazioni Azure AD hello supporta il provisioning utenti automatizzato. [elenco di Hello di App in primo piano può essere visualizzato qui.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

Affinché un'applicazione toosupport automatizzati di provisioning dell'utente, innanzitutto necessario fornire hello gli endpoint necessari per la creazione di programmi esterni tooautomate hello, manutenzione e la rimozione degli utenti. Pertanto, non tutte le app SaaS sono compatibili con questa funzionalità. Per le applicazioni che supportano questa operazione, team di progettazione di hello Azure AD verrà quindi essere in grado di toobuild un provisioning toothose connettore App e il lavoro è ordinati in base alle esigenze di hello e potenziali clienti.

ingegneria hello Azure AD toocontact team toorequest provisioning il supporto per applicazioni aggiuntive, inviare un messaggio tramite hello [forum sul feedback su Azure Active Directory](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Personalizzazione dei mapping degli attributi per il Provisioning dell’utente](active-directory-saas-customizing-attribute-mappings.md)
* [Scrittura di espressioni per i mapping degli attributi](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Ambito dei filtri per il Provisioning utente](active-directory-saas-scoping-filters.md)
* [Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notifiche relative al provisioning dell'account](active-directory-saas-account-provisioning-notifications.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS](active-directory-saas-tutorial-list.md)

