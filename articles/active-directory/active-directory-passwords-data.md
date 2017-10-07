---
title: Requisiti dei dati di Azure AD SSPR | Documentazione Microsoft
description: Reimpostare i requisiti di dati per la password self-service di Azure AD e come toosatisfy li
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
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Distribuire la reimpostazione della password senza richiedere la registrazione dell'utente finale

La distribuzione di reimpostazione di Password Self-Service (SSPR) richiede l'autenticazione dati toobe presente. Alcune organizzazioni hanno agli utenti di immettere i dati di autenticazione se stessi, ma molte organizzazioni preferiscono toosynchronize con i dati esistenti in Active Directory. Se i dati siano formattati correttamente nella directory locale e configurare [Azure AD Connect impostazioni rapide](./connect/active-directory-aadconnect-get-started-express.md), che i dati vengono resi disponibili tooAzure AD e SSPR, senza l'intervento dell'utente necessari.

Tutti i numeri di telefono devono essere in formato hello + esempio di PhoneNumber CountryCode: + 1 4255551234 toowork correttamente.

> [!NOTE]
> La reimpostazione della password non supporta le estensioni del telefono. Anche in formato 12345 4255551234 + 1 X di hello, le estensioni vengono rimossi prima viene effettuata la chiamata di hello.

## <a name="fields-populated"></a>Campi popolati

Se si utilizzano le impostazioni predefinite di hello in Azure AD Connect hello seguenti vengono eseguiti mapping.

| Active Directory locale | Azure AD | Informazioni di contatto per l'autenticazione di Azure AD |
| --- | --- | --- |
| telephoneNumber | Telefono ufficio | Telefono alternativo |
| mobile | Cellulare | Telefono |


## <a name="security-questions-and-answers"></a>Domande di sicurezza e risposte

Domande di sicurezza e le risposte vengono archiviate in modo sicuro nel tenant di Azure AD e sono solo accessibili toousers tramite hello [portale di registrazione SSPR](https://aka.ms/ssprsetup). Gli amministratori possono visualizzare o modificare contenuto hello di un altro utenti domande frequenti.

### <a name="what-happens-when-a-user-registers"></a>Cosa accade quando un utente si registra

Quando un utente registra, pagina di registrazione hello imposta hello seguenti campi:

* Telefono per l'autenticazione
* Indirizzo di posta elettronica per l'autenticazione
* Domande di sicurezza e risposte

Se è stato specificato un valore per **cellulare** o **posta elettronica alternativo**, gli utenti possono utilizzare immediatamente tooreset tali valori le password, anche se non sono stati registrati per il servizio di hello. Inoltre, gli utenti visualizzati tali valori durante la registrazione per hello prima volta e modificarle se necessario. Dopo la registrazione sono correttamente, tali valori verranno mantenuti nel hello **telefono per l'autenticazione** e **posta elettronica di autenticazione** campi, rispettivamente.

## <a name="set-and-read-authentication-data-using-powershell"></a>Impostare e leggere i dati di autenticazione tramite PowerShell

Hello seguente i campi può essere impostata mediante PowerShell

* Indirizzo di posta elettronica alternativo
* Cellulare
* Telefono ufficio - può essere impostato solo se non in sincronizzazione con una directory locale

### <a name="using-powershell-v1"></a>Tramite PowerShell V1

tooget avviato, è necessario troppo[scaricare e installare il modulo di Azure AD PowerShell hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Dopo aver installato, è possibile seguire i passaggi di hello che seguono tooconfigure ogni campo.

#### <a name="set-authentication-data-with-powershell-v1"></a>Impostare i Dati di autenticazione con PowerShell V1

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>Leggere i Dati di autenticazione con PowerShell V1

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>Telefono per l'autenticazione e la posta elettronica di autenticazione possono solo essere letti utilizzando Powershell V1 hello utilizzando i comandi che seguono

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>Tramite PowerShell V2

tooget avviato, è necessario troppo[scaricare e installare il modulo di PowerShell hello Azure Active Directory V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Dopo aver installato, è possibile seguire i passaggi di hello che seguono tooconfigure ogni campo.

tooinstall rapidamente da versioni recenti di PowerShell che supportano Install-Module, eseguire questi comandi (prima riga hello controlla semplicemente toosee se è già installato):

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>Impostare i Dati di autenticazione con PowerShell V2

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>Leggere i Dati di autenticazione con PowerShell V2

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR
