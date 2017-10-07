---
title: linee guida per le applicazioni aaaBranding | Documenti Microsoft
description: Una serie completa Guida orientata ai servizi toodeveloper risorse di Azure Active Directory
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>Linee guida sulla personalizzazione per le applicazioni
Questo argomento illustra hello personalizzazione linee guida, che è consigliabile utilizzare durante lo sviluppo di applicazioni con Azure Active Directory (Azure AD). Queste linee guida consente di indirizzare i clienti quando desiderano toouse il proprio lavoro o l'account dell'istituto di istruzione, gestito in Azure AD o proprio account personale per l'applicazione di iscrizione e accesso tooyour.

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>Confronto tra account Microsoft personali e aziendali o dell'istituto di istruzione
Microsoft gestisce due tipi di account utente:

* **Account personali** (noti in precedenza come Windows Live ID). Questi account rappresentano la relazione hello tra *singoli* utenti Microsoft e vengono utilizzati tooaccess dispositivi e servizi Microsoft. Questi account sono concepiti per un uso personale.
* **Account aziendali o dell'istituto di istruzione.** Questi account sono gestiti da Microsoft per conto delle organizzazioni che usano Azure Active Directory. Questi account sono utilizzati toosign tooOffice 365 e altri servizi aziendali Microsoft.

Microsoft account aziendali o dell'istituto di istruzione sono in genere assegnate agli utenti di tooend (dipendenti, studenti, impiegati) dalle organizzazioni (azienda, istituto di istruzione, agenzia governativa). Questi account sono che uno gestiti direttamente nel cloud. hello in piattaforma hello Azure AD o sincronizzato tooAzure AD da una directory locale, ad esempio Windows Server Active Directory. Microsoft è hello *responsabile* di lavoro hello o scuola, ma hello account sono controllati e di proprietà da organizzazione hello.

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>Riferimento tooAzure AD account nell'applicazione
Microsoft non espone gli utenti finali toohello Azure o i marchi di hello Active Directory e non è necessario.

* Una volta che gli utenti connessi, è necessario utilizzare nome e il più possibile il logo dell'organizzazione hello. Questa soluzione è preferibile rispetto all'uso di termini generici come "organizzazione".
* Quando gli utenti non connessi, è consigliabile consultare tootheir account come "lavoro o scuola account" e utilizzare hello Microsoft logo tooconvey che questi account sono gestiti da Microsoft. Non usare termini quali "account dell'azienda", "account dell'impresa" o "account della società", perché potrebbero creare confusione nell'utente.

## <a name="user-account-pictogram"></a>Pittogramma dell'account utente
In una versione precedente di queste linee guida si è consigliato di usare un pittogramma di "badge blu". In base ai commenti e suggerimenti utenti e agli sviluppatori, ora invece è consigliabile utilizzare hello del logo Microsoft hello. Ciò consentirà agli utenti comprendere che possono riutilizzare hello l'account utilizzato con Office 365 o altri toosign di servizi aziendali Microsoft nell'app tooyour.

## <a name="signing-up-and-signing-in-with-azure-ad"></a>Iscrizione e accesso con Azure AD
App possono presentare percorsi separati per l'iscrizione e Accedi e hello le sezioni seguenti fornisce indicazioni visive per entrambi gli scenari.

**Se l'app supporta l'utente finale di iscrizione (ad esempio disponibile tootrial o freemium modello)**: È possibile visualizzare un **Accedi** pulsante che consente agli utenti tooaccess all'app con l'account aziendale o il proprio account personale. Azure AD visualizzerà un hello dei messaggi di richiesta di consenso prima volta che accedono alle app.

**Se l'app richiede autorizzazioni che solo gli amministratori possono concedere oppure se l'app richiede una licenza dell'organizzazione**: è consigliabile separare l'acquisizione amministrativa dall'accesso utente. Hello **"ottenere questa app" pulsante** verrà reindirizzare toosign admins in quindi chiedere toogrant consenso per conto degli utenti dell'organizzazione. Questo è hello ulteriore vantaggio di eliminare gli utenti finali consenso richieste tooyour app.

## <a name="visual-guidance-for-app-acquisition"></a>Indicazioni visive per l'acquisizione di app
Il collegamento "ottenere app hello" è necessario reindirizzare hello utente Azure AD toohello concedere l'accesso (autorizzazione) pagina, tooallow tooauthorize amministratore dell'organizzazione toohave l'app accedere ai dati dell'organizzazione tootheir ospitato da Microsoft. Informazioni dettagliate su come accesso toorequest vengono discussi in hello [integrazione di applicazioni con Azure Active Directory](active-directory-integrating-applications.md) articolo.

Dopo che gli amministratori di consenso app tooyour, possono scegliere tooadd è tootheir di Office 365 app dell'utilità di avvio da parte degli utenti (accessibile dal waffle hello e dal [https://portal.office.com/myapps](https://portal.office.com/myapps)). Se si desidera tooadvertise questa funzionalità, è possibile utilizzare termini quali "Aggiungi questa organizzazione tooyour app" e Mostra un pulsante simile al seguente:

![Scenari e tipi di applicazione](./media/active-directory-branding-guidelines/add-to-my-org.png)

È tuttavia consigliabile scrivere un testo descrittivo, invece di fare affidamento sui pulsanti. ad esempio:

> *Se si usa già Office 365 o altri servizi aziendali Microsoft, è possibile concedere semplicemente i dati dell'organizzazione di < your_app_name > accesso tooyour. In questo modo il tooaccess utenti < your_app_name > con l'account aziendale esistente.*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>Indicazioni visive per l'accesso
L'app deve essere visualizzato un segno nel pulsante che consente di reindirizzare gli utenti toohello Accedi endpoint corrispondente protocollo toohello utilizzare toointegrate con Azure AD. Hello seguente sezione vengono fornite informazioni dettagliate su quale pulsante deve essere simile.

### <a name="pictogram-and-sign-in-with-microsoft"></a>Pittogramma e "Accedi con Microsoft"
'S associazione hello logo Microsoft hello e termini di "Sign in con Microsoft" hello che rappresenta in modo univoco Azure AD dagli altri provider di identità supportati dall'app. Se non si dispone di spazio sufficiente per "Sign in con Microsoft", è ok tooshorten troppo "Accedi".

![Scenari e tipi di applicazione](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![Scenari e tipi di applicazione](./media/active-directory-branding-guidelines/sign-in-light.png)

È anche possibile utilizzare una combinazione di colori scuro per i pulsanti hello.

![Scenari e tipi di applicazione](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![Scenari e tipi di applicazione](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>Azioni consentite e non consentite per la personalizzazione
**ESEGUIRE** "account aziendale o dell'istituto di istruzione" in combinazione con hello "Sign in con Microsoft" pulsante tooprovide spiegazione aggiuntiva toohelp gli utenti finali di utilizzare riconoscere se è possibile utilizzarlo. **NON** usare termini quali "account dell'azienda", "account dell'impresa" o "account della società".

**NON USARE** "ID di Office 365" o "ID di Azure". Office 365 è anche il nome di hello di un consumer offerta da Microsoft che non usano Azure AD per l'autenticazione.

**Non** alter logo Microsoft hello.

**Non** esporre marchi di Active Directory o Azure toohello gli utenti finali. È tuttavia toouse questi termini con gli sviluppatori, i professionisti IT e gli amministratori.

## <a name="navigation-dos-and-donts"></a>Azioni consentite e non consentite per la navigazione
**ESEGUIRE** forniscono un modo per gli utenti toosign out e cambiare l'account utente tooanother. Quasi tutte le persone hanno in genere un singolo account per Microsoft, Facebook, Google e Twitter, ma sono spesso associate a più organizzazioni. Il supporto per l'accesso di più utenti sarà presto disponibile.

