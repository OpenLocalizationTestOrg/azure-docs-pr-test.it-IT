---
title: 'Personalizzazione: reimpostazione password self-service di Azure AD | Microsoft Docs'
description: Opzioni di personalizzazione per la reimpostazione della password self-service di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Personalizzare la funzionalità di Azure AD per la Reimpostazione self-service delle password

I professionisti IT ricerca toodeploy la reimpostazione della password self-service è possono personalizzare il hello esperienza toomatch agli utenti.

## <a name="customize-hello-contact-your-administrator-link"></a>Personalizzare il collegamento di amministratore di contatto hello

Anche se SSPR non gli utenti abilitati ancora un collegamento "contattare l'amministratore" password hello portale di reimpostazione.  Facendo clic su questo collegamento tramite posta elettronica agli amministratori che richiede l'assistenza di modifica della password dell'utente hello. Questo messaggio viene inviato toohello destinatari hello seguendo l'ordine seguente:

1. Se hello **amministratore Password** ruolo viene assegnato, vengono visualizzata una notifica agli amministratori di questo ruolo
2. Se nessuna Password amministratore vengono assegnati, quindi gli amministratori con hello **Amministratore utenti** viene inviata una notifica di ruolo
3. Se nessuno dei ruoli di hello precedenti sono stati assegnati, quindi **gli amministratori globali** viene inviata una notifica

In tutti i casi, viene inviata una notifica a un massimo di 100 destinatari totali.

toofind ulteriori informazioni su hello diversi ruoli di amministratore e come essi vedere tooassign hello documento [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Disabilitare i messaggi di posta elettronica Contattare l'amministratore

Se l'organizzazione non desidera che gli amministratori informati password le richieste di reset, hello configurazione seguente può essere abilitata

* Abilitare la reimpostazione self-service delle password per tutti gli utenti finali. Questa opzione è in **Reimpostazione password > Proprietà**.
    * Se non si desidera che gli utenti tooreset le proprie password, è possibile definire l'ambito di gruppo vuoto di accesso tooan **questa opzione si consiglia di non**.
* Personalizzare hello helpdesk collegamento tooprovide un URL web o mailto: indirizzo che gli utenti possono usare tooget assistenza. Questa opzione si trova in **Reimpostazione password > Personalizzazione > Indirizzo di posta elettronica o URL del supporto tecnico**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>Personalizzazione di ADFS nella pagina di accesso per SSPR

Gli amministratori di ADFS è possibile aggiungere una collegamento tootheir pagina di accesso usando il materiale sussidiario hello nell'articolo hello [descrizione nella pagina di accesso Add](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

Comando hello che segue nel server ADFS consente di aggiungere una pagina di accesso ADFS toohello di collegamento che consente di flusso di lavoro la reimpostazione della password self-service di utenti tooenter hello direttamente.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>Personalizzare hello Accedi e accesso pannello aspetto

Quando gli utenti accedono a pagina di accesso hello, è possibile personalizzare il logo hello che viene visualizzata con hello nella pagina di accesso immagine toofit azienda personalizzazione.

Questi elementi grafici vengono visualizzati in hello seguenti circostanze:

* Dopo che l'utente digita il proprio nome utente
* L'utente accede a un url personalizzato
    * Da hello passando come "https://login.microsoftonline.com/?whr=contoso.com" pagina di reimpostazione password toohello di parametro "whr"
    * Per il passaggio di hello "username" parametro toohello reimpostazione della password pagina, ad esempio "https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>Dettagli di grafica

consentono di determinare le caratteristiche visive toochange hello della pagina di accesso hello Hello impostazioni seguenti ed è reperibile nella **Azure Active Directory**, **personalizzazione specifica della società**, **modifica aziendale personalizzazione**

* L'immagine della pagina di accesso deve essere un file con estensione PNG o JPG da 1420 x 1200 pixel e non superiore a 500 KB. È consigliabile toobe circa 200 KB per ottenere risultati ottimali.
* Colore di sfondo nella pagina di accesso viene utilizzato quando si trovano le connessioni con latenza elevata e deve essere in formato esadecimale RGB di hello.
* L'immagine del banner deve essere un file con estensione PNG o JPG da 60 x 280 pixel e non superiore a 10 KB.
* Logo quadrato (tema normale e scuro) PNG o JPG 240 x 240 (ridimensionabile) non superiore a 10 KB.

### <a name="sign-in-text-options"></a>Opzioni del testo di accesso

Hello le impostazioni seguenti consentono di organizzazione tooyour pertinenti di tooadd testo toohello nella pagina di accesso. Queste impostazioni sono disponibili nella sezione **Azure Active Directory**, **Informazioni personalizzate distintive dell'azienda**, **Modifica informazioni personalizzate distintive dell'azienda**

* **Hint di nome utente** sostituisce hello testo di esempio di someone@example.com con un nome più appropriato per gli utenti, consigliabile toobe sinistro predefinito per supportare gli utenti interni ed esterni
* **Testo della pagina di accesso** contiene un massimo di 256 caratteri. Questo testo e verrà visualizzato in qualsiasi punto l'account di accesso di utenti online, hello esperienza di aggiunta ad Azure AD in Windows 10. Usare questo testo per le condizioni di utilizzo, le istruzioni e i suggerimenti per gli utenti. **Chiunque può visualizzare la pagina di accesso pertanto si consiglia di non fornire informazioni riservate qui.**

### <a name="keep-me-signed-in-disabled"></a>Mantieni l'accesso disabilitata

opzione Hello "Mantieni l'accesso disabilitato" consente agli utenti tooremain connesso quando viene chiuso e riaperto la finestra del browser. e non influisce sulla durata della sessione. Queste impostazioni sono disponibili nella sezione **Azure Active Directory > Informazioni personalizzate distintive dell'azienda > Modifica informazioni personalizzate distintive dell'azienda**.

Alcune funzionalità di SharePoint Online e Office 2010 dipendono gli utenti in grado di toocheck questa casella. Se si nasconde questa opzione, gli utenti possono ottenere prompt di accesso aggiuntivi e imprevisti.

### <a name="directory-name"></a>Nome della directory

È possibile modificare l'attributo nome hello **Azure Active Directory > proprietà** tooshow un nome descrittivo dell'organizzazione visualizzato nel portale di hello e automatizzata delle comunicazioni. Questa opzione è più visibile nel modulo hello dei messaggi di posta elettronica automatizzati in form di hello che seguono

* Nome descrittivo nel messaggio di posta elettronica "Microsoft per conto della demo CONTOSO"
* Riga dell'oggetto nel messaggio di posta elettronica "Codice di verifica della e-mail dell'account di demo CONTOSO"

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD
* [**Writeback delle password**](active-directory-passwords-writeback.md): funzionamento del writeback delle password con la directory locale
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR

