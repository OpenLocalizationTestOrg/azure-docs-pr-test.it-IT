---
title: Esempi e definizioni di API per la creazione di report sull'uso in Azure Active Directory B2C | Microsoft Docs
description: "Guida ed esempi su come ottenere i report su utenti, autenticazioni e autenticazioni a più fattori del tenant di Azure AD B2C"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Accesso ai report di utilizzo in Azure Active Directory B2C tramite API di segnalazione hello

Azure Active Directory B2C (Azure AD B2C) fornisce l'autenticazione basata sull'accesso utente e sull'autenticazione a più fattori di Azure. L'autenticazione è disponibile per gli utenti finali della famiglia di applicazioni tra i provider di identità. Quando si conosce il numero di hello di utenti registrati nel tenant di hello provider hello e utilizzate tooregister e numero di autenticazioni di hello dal tipo, è possibile rispondere a domande come:
* Il numero di utenti da ogni tipo di provider di identità (ad esempio, un account Microsoft o LinkedIn) è registrate in hello ultimi 10 giorni?
* Quanti autenticazioni tramite multi-Factor Authentication sono state completate in hello ultimo mese?
* Numero di autenticazioni basate su accesso eseguite correttamente nel mese corrente, per ogni giorno e per ogni applicazione.
* Come è possibile stimare hello è previsto un costo mensile di attività tenant Azure Active Directory B2C?

Questo articolo è incentrato sull'attività di toobilling report correlato, che si basa sul numero di hello di utenti, le autenticazioni di accesso in base fatturabili e autenticazioni di multi-factor Authentication.


## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, è necessario passaggi hello toocomplete [tooaccess prerequisiti hello Azure AD reporting API](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Creare un'applicazione, per ottenere una chiave privata e accedere concedere i diritti di report del tenant di Azure Active Directory B2C tooyour. Di seguito vengono riportati anche esempi di *script Bash* e *script Python*. 

## <a name="powershell-script"></a>Script di PowerShell
Questo script illustra la creazione di hello di quattro report di utilizzo tramite hello `TimeStamp` parametro e hello `ApplicationId` filtro.

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a>Definizioni dei report sull'uso
* **tenantUserCount**: hello numero di utenti nel tenant di hello dal tipo di provider di identità, al giorno in hello ultimi 30 giorni. (Facoltativamente, un `TimeStamp` filtro fornisce al conteggio degli utenti da toohello una data specificata data corrente). Hello report disponibili.
  * **TotalUserCount**: hello numero di tutti gli oggetti utente.
  * **OtherUserCount**: hello numero di utenti di Azure Active Directory (non gli utenti di Azure Active Directory B2C).
  * **LocalUserCount**: hello numero di account utente di Azure Active Directory B2C creato con tenant Azure Active Directory B2C di toohello locale le credenziali.

* **AlternateIdUserCount**: numero hello di utenti di Azure Active Directory B2C registrato con provider di identità esterno (ad esempio, Facebook, un account Microsoft o un altro tenant di Azure Active Directory, denominato anche tooas un `OrgId`).

* **b2cAuthenticationCountSummary**: riepilogo numero giornaliero di hello di autenticazioni fatturabili su hello ultimi 30 giorni dal giorno e il tipo di flusso di autenticazione.

* **b2cAuthenticationCount**: hello numero di autenticazioni entro un periodo di tempo. valore predefinito di Hello è hello ultimi 30 giorni.  (Facoltativo: hello all'inizio e fine `TimeStamp` parametri definiscono un periodo di tempo specifico.) sono inclusi l'output di hello `StartTimeStamp` (prima data dell'attività per questo tenant) e `EndTimeStamp` (ultimo aggiornamento).

* **b2cMfaRequestCountSummary**: riepilogo del numero giornaliero di hello di autenticazioni di multi-factor, dal giorno e il tipo (SMS o vocale).


## <a name="limitations"></a>Limitazioni
Dati di conteggio dell'utente viene aggiornati ogni 24 ore too48. Le autenticazioni vengono aggiornate diverse volte al giorno. Quando si utilizza hello `ApplicationId` filtro, una risposta di un report vuoto può essere dovuta tooone delle condizioni seguenti:
  * ID dell'applicazione Hello non esiste nel tenant di hello. Verificare che sia corretto.
  * ID dell'applicazione Hello esiste, ma nessun dato è stato trovato nel periodo di reporting hello. Controllare i valori dei parametri Data/Ora.


## <a name="next-steps"></a>Passaggi successivi
### <a name="monthly-bill-estimates-for-azure-ad"></a>Stime della fattura mensile per Azure AD
In combinazione con [hello aggiornate Azure Active Directory B2C disponibili prezzi](https://azure.microsoft.com/pricing/details/active-directory-b2c/), è possibile stimare giornaliera, settimana e mensile consumo di Azure.  Questa stima è particolarmente utile quando si pianificano modifiche nel comportamento del tenant che potrebbero influire sul costo complessivo. È possibile rivedere i costi attuali nella [sottoscrizione Azure collegata](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Opzioni per altri formati di output
Hello codice riportato di seguito vengono illustrati esempi di invio tooJSON output, un elenco di valori di nome e XML:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
