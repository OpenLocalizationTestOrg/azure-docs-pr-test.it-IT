---
title: Criteri - Reimpostazione password self-service di Azure AD | Microsoft Docs
description: Opzioni dei criteri di reimpostazione password self-service di Azure AD
services: active-directory
keywords: gestione delle password in Active Directory, gestione delle password, reimpostazione password self-service di Azure AD
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
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Restrizioni e criteri password in Azure Active Directory

Questo articolo descrive i criteri password hello e i requisiti di complessità associati agli account utente archiviati nel tenant di Azure AD.

## <a name="administrator-password-policy-differences"></a>Differenze tra i criteri password degli amministratori

Microsoft consente di applicare criteri avanzati di reimpostazione della password con **doppio controllo** predefiniti per tutti i ruoli di amministratore di Azure, ad esempio amministratore globale, amministratore del supporto tecnico, amministratore password e così via.

Questo disabilita gli amministratori di usare le domande di sicurezza e applica la seguente hello.

Due controllare criteri, che richiedono due tipi di dati di autenticazione (indirizzo di posta elettronica **e** il numero di telefono), si applica in hello seguenti circostanze

* Tutti i ruoli di amministratore di Azure
  * Amministratore del supporto tecnico
  * Amministratore del supporto servizio
  * Amministratore fatturazione
  * Supporto partner - Livello 1
  * Supporto partner - Livello 2
  * Amministratore del servizio Exchange
  * Amministratore del servizio Lync
  * Amministratore account utente
  * Writer di directory
  * Amministratore globale/amministratore aziendale
  * Amministratore del servizio SharePoint
  * Amministratore di conformità
  * Amministratore di applicazioni
  * Amministratore della sicurezza
  * Amministratore dei ruoli con privilegi
  * Amministratore del servizio Intune
  * Amministratore del servizio proxy di applicazione
  * Amministratore del servizio CRM
  * Amministratore del servizio Power BI
  
* 30 giorni trascorsi per una versione di valutazione **OPPURE**
* Presenza di un dominio personalizzato (contoso.com) **OPPURE**
* Identità sincronizzate da Azure AD Connect nella directory locale

### <a name="exceptions"></a>Eccezioni
I criteri a un controllo, che richiedono una parte di dati di autenticazione (indirizzo di posta elettronica **o** il numero di telefono), si applica in hello seguenti circostanze

* Primi 30 giorni di una versione di valutazione **OPPURE**
* Dominio personalizzato non presente (*.onmicrosoft.com) **E** identità non sincronizzate da Azure AD


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>Criteri UserPrincipalName che si applicano gli account utente tooall

Ogni account utente che deve toosign in tooAzure Active Directory deve avere un valore di attributo nome principale (UPN) univoco utente associato all'account. tabella Hello seguente contorni hello criteri che si applicano tooboth locale gli account utente di Active Directory sincronizzati toohello cloud e account utente solo toocloud.

| Proprietà | Requisiti di UserPrincipalName |
| --- | --- |
| Caratteri consentiti |<ul> <li>A-Z</li> <li>a - z</li><li>0 – 9</li> <li> . - \_ ! \# ^ \~</li></ul> |
| Caratteri non consentiti |<ul> <li>Qualsiasi ' @' carattere che non è separando il nome utente hello dal dominio hello.</li> <li>Non può contenere un carattere punto '.' immediatamente precedente hello ' @' simbolo</li></ul> |
| Vincoli di lunghezza |<ul> <li>La lunghezza totale non deve superare i 113 caratteri</li><li>64 caratteri prima hello ' @' simbolo</li><li>48 caratteri dopo hello ' @' simbolo</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Criteri password che si applicano solo gli account utente di toocloud

Hello nella tabella seguente descrive le impostazioni di criteri password disponibili hello che possono essere applicati toouser che vengono create e gestite in Azure AD.

| Proprietà | Requisiti |
| --- | --- |
| Caratteri consentiti |<ul><li>A-Z</li><li>a - z</li><li>0 – 9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| Caratteri non consentiti |<ul><li>Caratteri Unicode</li><li>Spazi</li><li> **Le password complesse**: non può contenere un carattere punto '.' immediatamente precedente hello ' @' simbolo</li></ul> |
| Restrizioni per le password |<ul><li>minimo 8 caratteri e massimo 16 caratteri</li><li>**Le password complesse**: richiede 3 su 4 seguenti hello:<ul><li>Caratteri minuscoli</li><li>Caratteri maiuscoli</li><li>Numeri (0-9)</li><li>Simboli (vedere le restrizioni per le password sopra citate)</li></ul></li></ul> |
| Durata di validità della password |<ul><li>Valore predefinito: **90** giorni </li><li>Valore è configurabile tramite il cmdlet Set-MsolPasswordPolicy hello da hello modulo di Azure Active Directory per Windows PowerShell.</li></ul> |
| Notifica della scadenza della password |<ul><li>Valore predefinito: **14** giorni (prima della scadenza della password)</li><li>Valore è configurabile tramite il cmdlet Set-MsolPasswordPolicy hello.</li></ul> |
| Scadenza della password |<ul><li>Valore predefinito: **false** giorni (indica che la scadenza password è abilitata) </li><li>Valore può essere configurato per singoli account utente utilizzando i cmdlet Set-MsolUser hello. </li></ul> |
| Cronologia di **modifica** della password |L'ultima password **non può** essere riusata alla **modifica** della password. |
| Cronologia di **reimpostazione** della password | L'ultima password **può** essere riusata alla **reimpostazione** della password dimenticata. |
| Blocco account |Dopo 10 Accedi tentativi (password errata), utente hello verrà bloccato per un minuto. Ulteriormente corretto tentativi di accesso utente hello blocco per aumentare la durata. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Impostare i criteri di scadenza della password in Azure Active Directory

Un amministratore globale per un servizio cloud Microsoft può utilizzare hello modulo dei Microsoft Azure Active Directory per Windows PowerShell tooset backup delle password utente non tooexpire. È anche possibile utilizzare i cmdlet tooremove hello-non scade mai configurazione o toosee tooexpire non vengono impostate le password utente di Windows PowerShell. Questa guida si applica tooother provider, ad esempio Microsoft Intune e Office 365, che si basano su Microsoft Azure Active Directory anche per i servizi di identità e directory.

> [!NOTE]
> Le password sole per gli account utente che non sono sincronizzati tramite sincronizzazione della directory possono essere configurati toonot scadenza. Per altre informazioni sulla sincronizzazione delle directory, vedere [Integrare le directory locali con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>Impostare o verificare i criteri password tramite PowerShell

tooget avviato, è necessario troppo[scaricare e installare il modulo di Azure AD PowerShell hello](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0). Dopo aver installato, è possibile eseguire operazioni di hello seguenti tooconfigure ogni campo.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>Come criteri di scadenza toocheck una password
1. Connettersi tooWindows PowerShell utilizzando le credenziali di amministratore della società.
2. Eseguire uno dei seguenti comandi hello:

   * toosee se la password di un utente è impostata toonever scadenza, eseguire hello seguente cmdlet utilizzando hello nome principale utente (UPN) (ad esempio, aprilr@contoso.onmicrosoft.com) o hello ID utente dell'utente hello desiderato toocheck:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee hello impostazione "Nessuna scadenza Password" per tutti gli utenti, eseguire hello seguente cmdlet:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>Impostare una password tooexpire

1. Connettersi tooWindows PowerShell utilizzando le credenziali di amministratore della società.
2. Eseguire uno dei seguenti comandi hello:

   * password hello tooset di un utente in modo che hello scadenza della password, eseguire hello seguente cmdlet utilizzando hello nome principale utente (UPN) o hello l'ID dell'utente hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * le password hello tooset di tutti gli utenti dell'organizzazione hello in modo che scadono, utilizzano hello seguente cmdlet:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>Scadenza set toonever una password

1. Connettersi tooWindows PowerShell utilizzando le credenziali di amministratore della società.
2. Eseguire uno dei seguenti comandi hello:

   * password hello tooset di un utente toonever scadenza, eseguire hello seguente cmdlet utilizzando hello nome principale utente (UPN) o l'ID dell'utente hello hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * le password hello tooset di tutti gli utenti di hello in un'organizzazione di toonever scadenza, eseguire hello seguente cmdlet:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR
