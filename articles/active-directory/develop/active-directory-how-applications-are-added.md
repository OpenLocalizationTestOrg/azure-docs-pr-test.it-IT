---
title: vengono aggiunte le applicazioni di aaaHow tooAzure Active Directory.
description: In questo articolo viene descritto come le applicazioni vengono aggiunti tooan istanza di Azure Active Directory.
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>Come e perché le applicazioni vengono aggiunte AD tooAzure
Uno dei hello inizialmente perplessità operazioni quando si visualizza un elenco di applicazioni nella propria istanza di Azure Active Directory è comprendere la provenienza applicazioni hello e perché sono.  In questo articolo verrà fornita una panoramica di alto livello di come le applicazioni sono rappresentate nella directory hello e forniscono contesto utili per comprendere come un'applicazione fornito toobe nella directory.

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>I servizi di Azure AD fornisce tooapplications?
Le applicazioni vengono aggiunte tooleverage tooAzure AD uno o più servizi hello forniti.  I servizi comprendono:

* Autenticazione e autorizzazione delle app
* Autenticazione e autorizzazione degli utenti
* Accesso Single Sign-On tramite federazione o password
* Provisioning e sincronizzazione degli utenti
* Controllo di accesso basato sui ruoli. Utilizzare hello directory toodefine applicazione tooperform ruoli basato su controlli di autorizzazione in un'applicazione.
* servizi di autorizzazione oAuth (usati da Office 365 e altre App tooauthorize accesso tooAPIs/risorse Microsoft).
* Pubblicazione dell'applicazione e proxy. Pubblicare un'app da una rete privata di toohello internet

## <a name="how-are-applications-represented-in-hello-directory"></a>Come le applicazioni sono rappresentate nella directory hello?
Le applicazioni sono rappresentate in Azure AD usando la 2 oggetti hello: un oggetto applicazione e un oggetto entità servizio.  C'è un oggetto di applicazione, registrato in un "home" / "proprietario" o "pubblicazione" directory e uno o più oggetti entità che rappresenta un'applicazione hello in ogni directory in cui serve del servizio.  

Descrive hello app tooAzure AD (servizio multi-tenant hello) Hello oggetto applicazione e può includere uno dei seguenti hello: (*nota*: non si tratta di un elenco esaustivo.)

* Nome, logo e autore
* Segreti (le chiavi simmetriche e/o asimmetriche utilizzato tooauthenticate hello app)
* Dipendenze API (oAuth)
* API/risorse/ambiti pubblicati (oAuth)
* Ruoli app (Controllo degli accessi in base al ruolo)
* Metadati e configurazione Single Sign-On (SSO)
* Metadati e configurazione del provisioning utenti
* Metadati e configurazione proxy

entità servizio Hello è un record di un'applicazione hello in ogni directory, in cui un'applicazione hello agisce inclusi relativa home directory.  entità servizio: Hello

* Fa riferimento l'oggetto applicazione tooan tramite proprietà id di app hello
* Registra le assegnazioni del ruolo app al gruppo e all'utente locale
* Record utente e amministratore le autorizzazioni concesse toohello app locale
  * Ad esempio: l'autorizzazione per hello app tooaccess un messaggio di posta elettronica di utenti specifici
* Registra i criteri locali, inclusi i criteri di accesso condizionale
* Registra le impostazioni locali alternative per un'app
  * Regole di trasformazione delle attestazioni
  * Mapping degli attributi (provisioning utenti)
  * I ruoli app specifico del tenant (se app hello supporta i ruoli personalizzati)
  * Nome/Logo

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>Diagramma degli oggetti applicazione e delle entità servizio tra le directory
![Diagramma che illustra gli oggetti applicazione e le entità servizio presenti all'interno delle istanze di Azure AD.][apps_service_principals_directory]

Come si può notare dal diagramma hello precedente.  Microsoft gestisce due directory internamente (sul lato sinistro di hello) Usa toopublish applicazioni.

* Una per le app Microsoft (directory di servizi Microsoft)
* Una per le app di terze parti preintegrate (directory Raccolta app)

I server di pubblicazione o fornitori di applicazioni che si integrano con Azure AD sono necessari toohave una directory di pubblicazione.  (ad alcuni una directory SaaS).

Applicazioni aggiunte dall'utente:

* App sviluppate dall'utente (integrate con AAD)
* App connesse per l'accesso Single Sign-On
* Le applicazioni pubblicate mediante hello proxy dell'applicazione Azure AD.

### <a name="a-couple-of-notes-and-exceptions"></a>Note ed eccezioni
* Non tutte le entità servizio punto di oggetti tooapplication indietro.  Questo perché Quando è stato compilato in Azure AD servizi hello fornito tooapplications sono molto più limitato e l'entità servizio hello è sufficiente per stabilire un'identità di applicazione.  entità di servizio originale Hello è stato più vicino nella forma toohello account del servizio di Windows Server Active Directory.  Per questo motivo, che è comunque possibile toocreate entità servizio utilizzando hello Azure AD PowerShell senza prima creare un oggetto applicazione.  Hello API Graph richiede un oggetto applicazione prima di creare un servizio principale.
* Non tutte le informazioni di hello descritte in precedenza è attualmente esposte a livello di codice.  esempio Hello è disponibili solo in hello dell'interfaccia utente:
  * Regole di trasformazione delle attestazioni
  * Mapping degli attributi (provisioning utenti)
* Per ulteriori informazioni dettagliate sulle entità servizio hello e gli oggetti dell'applicazione, vedere la documentazione di riferimento toohello API REST di Azure AD Graph.  *Hint*: hello documentazione dell'API Graph di Azure AD è riferimento allo schema tooa hello più vicino cosa per Azure AD che è attualmente disponibile.  
  * [Applicazione](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [Entità servizio](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>Come le app vengono aggiunti i toomy istanza di Azure AD?
Esistono molti modi che un'app può essere aggiunto AD tooAzure:

* Aggiungere un'app da hello [raccolta di App di Azure Active Directory](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* Iscriversi o accedere a un'app di terze parti integrata in Azure Active Directory, ad esempio [Smartsheet](https://app.smartsheet.com/b/home) o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx)
  * Durante l'iscrizione alto o in utenti sono frequenti toogive autorizzazione toohello app tooaccess proprio profilo e le altre autorizzazioni.  Hello prima persona toogive acconsente cause di un'entità servizio che rappresenta hello app toobe aggiunto toohello directory.
* Iscriversi o accedere ai Microsoft Online Services, ad esempio [Office 365](http://products.office.com/)
  * Quando si effettua la sottoscrizione tooOffice 365 iniziarne una versione di valutazione o altre entità di servizio vengono create nella directory hello che rappresenta hello vari servizi che vengono utilizzati toodeliver tutte funzionalità hello associate a Office 365.
  * Alcuni servizi di Office 365 come SharePoint creare entità servizio in una lezione tooallow comunicazione tra i componenti inclusi flussi di lavoro.
* Aggiungere un'app che stai sviluppando nel portale di gestione di Azure vedere hello: https://msdn.microsoft.com/library/azure/dn132599.aspx
* Aggiungere un'app in fase di sviluppo tramite Visual Studio. Vedere:
  * [Metodi di autenticazione ASP.NET](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [Servizi connessi](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* Aggiungere un hello di app toouse toouse [Proxy dell'applicazione Azure AD](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* Connettere un'app per l'accesso Single Sign-On tramite SAML o SSO basato su password
* Sono disponibili altri modi, incluse varie esperienze utente in Azure ed esperienze di esplorazione delle API nei centri per sviluppatori

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>Chi è l'istanza di Azure AD toomy applicazioni tooadd autorizzazione?
Solo gli amministratori globali possono:

* Aggiungere App dalla raccolta di app hello Azure AD (3rd Party le app preintegrate)
* Pubblicare un'app usando hello Proxy dell'applicazione Azure AD

Tutti gli utenti nella directory di disporre di applicazioni tooadd diritti che stanno sviluppando e su quali applicazioni sono condivisione/consentono di accedere ai dati aziendali di tootheir discrezione.  *Ricordare di accesso utente remoto/tooan app e concedono autorizzazioni possono comportare un servizio principale viene creato.*

Questo potrebbe inizialmente audio relative, ma hello keep seguente presente:

* Le app sono state tooleverage in grado di Windows Server Active Directory per l'autenticazione utente per molti anni senza toobe applicazione hello registrato e registrate nella directory hello.  Ora verrà visibilità tooexactly hanno migliorato le organizzazione hello quanti App utilizzano directory hello e for possibili.
* Non serve un processo di registrazione/pubblicazione delle app basato su amministratore.  Con Active Directory Federation Services è probabile che un amministratore ha tooadd un'app come relying party per conto di sviluppatori.  Ora gli sviluppatori possono eseguire queste operazioni in modo indipendente.
* Gli utenti in/backup tooapps utilizzando l'account dell'organizzazione per gli scopi aziendali di firma sono positiva.  Se gli utenti lasciano successivamente organizzazione hello perdono account di accesso tootheir in un'applicazione hello che erano in uso.
* È positivo anche il fatto di poter tenere sotto controllo quali dati sono stati condivisi e con quali applicazioni.  I dati sono più trasportabili che mai ed è quindi utile sapere chi ha condiviso determinati dati e con quali applicazioni.
* Le app che usano Azure AD per oAuth decidere esattamente le autorizzazioni che gli utenti sono in grado di toogrant tooapplications e le autorizzazioni che richiedono un tooagree di amministrazione di.  Dovrebbe essere che informa che solo gli amministratori possono fornire il consenso toolarger ambiti e le autorizzazioni più significative.
* Gli utenti aggiunta e consentendo tooaccess App che sono i propri dati gli eventi controllati in modo da visualizzare i report di controllo hello all'interno di toodetermine del portale di gestione di Azure hello come un'app è stato aggiunto toohello directory.

**Nota:** *Microsoft stesso è stato utilizzato con configurazione predefinita di hello per numero di mesi ora.*

Con tutto ciò ha che tooprevent possibili gli utenti nella directory da aggiungere applicazioni e da esercitare discrezione su quali informazioni condividono con le applicazioni mediante la modifica di configurazione di Directory nel portale di gestione di Azure hello.  Hello configurazione seguenti sono accessibili nel portale di gestione di Azure hello nella scheda "Configurazione" della Directory.

![Una schermata di hello dell'interfaccia utente per la configurazione delle impostazioni dell'app integrata][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su tooadd tooAzure applicazioni Active Directory come tooconfigure servizi e per le app.

* Gli sviluppatori: [informazioni come toointegrate un'applicazione con AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* Sviluppatori: [Esaminare il codice di esempio per le app integrate con Azure Active Directory in GitHub](https://github.com/AzureADSamples)
* Gli sviluppatori e professionisti IT: [hello API REST per vedere documentazione di hello API di Graph di Azure Active Directory](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* I professionisti IT: [informazioni su Azure Active Directory toouse pre-l'integrazione di applicazioni dalla raccolta di App hello](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* Professionisti IT: [Esercitazioni per la configurazione di app preintegrate specifiche](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* I professionisti IT: [informazioni su come un'app usando toopublish hello Proxy dell'applicazione Azure Active Directory](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>Vedere anche
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
