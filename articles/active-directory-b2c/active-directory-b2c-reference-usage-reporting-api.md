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
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="12e8e-103">Accesso ai report di utilizzo in Azure Active Directory B2C tramite API di segnalazione hello</span><span class="sxs-lookup"><span data-stu-id="12e8e-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="12e8e-104">Azure Active Directory B2C (Azure AD B2C) fornisce l'autenticazione basata sull'accesso utente e sull'autenticazione a più fattori di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e8e-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="12e8e-105">L'autenticazione è disponibile per gli utenti finali della famiglia di applicazioni tra i provider di identità.</span><span class="sxs-lookup"><span data-stu-id="12e8e-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="12e8e-106">Quando si conosce il numero di hello di utenti registrati nel tenant di hello provider hello e utilizzate tooregister e numero di autenticazioni di hello dal tipo, è possibile rispondere a domande come:</span><span class="sxs-lookup"><span data-stu-id="12e8e-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="12e8e-107">Il numero di utenti da ogni tipo di provider di identità (ad esempio, un account Microsoft o LinkedIn) è registrate in hello ultimi 10 giorni?</span><span class="sxs-lookup"><span data-stu-id="12e8e-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="12e8e-108">Quanti autenticazioni tramite multi-Factor Authentication sono state completate in hello ultimo mese?</span><span class="sxs-lookup"><span data-stu-id="12e8e-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="12e8e-109">Numero di autenticazioni basate su accesso eseguite correttamente nel mese corrente,</span><span class="sxs-lookup"><span data-stu-id="12e8e-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="12e8e-110">per ogni giorno</span><span class="sxs-lookup"><span data-stu-id="12e8e-110">Per day?</span></span> <span data-ttu-id="12e8e-111">e per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="12e8e-111">Per application?</span></span>
* <span data-ttu-id="12e8e-112">Come è possibile stimare hello è previsto un costo mensile di attività tenant Azure Active Directory B2C?</span><span class="sxs-lookup"><span data-stu-id="12e8e-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="12e8e-113">Questo articolo è incentrato sull'attività di toobilling report correlato, che si basa sul numero di hello di utenti, le autenticazioni di accesso in base fatturabili e autenticazioni di multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="12e8e-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="12e8e-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="12e8e-114">Prerequisites</span></span>
<span data-ttu-id="12e8e-115">Prima di iniziare, è necessario passaggi hello toocomplete [tooaccess prerequisiti hello Azure AD reporting API](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="12e8e-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="12e8e-116">Creare un'applicazione, per ottenere una chiave privata e accedere concedere i diritti di report del tenant di Azure Active Directory B2C tooyour.</span><span class="sxs-lookup"><span data-stu-id="12e8e-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="12e8e-117">Di seguito vengono riportati anche esempi di *script Bash* e *script Python*.</span><span class="sxs-lookup"><span data-stu-id="12e8e-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="12e8e-118">Script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="12e8e-118">PowerShell script</span></span>
<span data-ttu-id="12e8e-119">Questo script illustra la creazione di hello di quattro report di utilizzo tramite hello `TimeStamp` parametro e hello `ApplicationId` filtro.</span><span class="sxs-lookup"><span data-stu-id="12e8e-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

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


## <a name="usage-report-definitions"></a><span data-ttu-id="12e8e-120">Definizioni dei report sull'uso</span><span class="sxs-lookup"><span data-stu-id="12e8e-120">Usage report definitions</span></span>
* <span data-ttu-id="12e8e-121">**tenantUserCount**: hello numero di utenti nel tenant di hello dal tipo di provider di identità, al giorno in hello ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="12e8e-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="12e8e-122">(Facoltativamente, un `TimeStamp` filtro fornisce al conteggio degli utenti da toohello una data specificata data corrente).</span><span class="sxs-lookup"><span data-stu-id="12e8e-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="12e8e-123">Hello report disponibili.</span><span class="sxs-lookup"><span data-stu-id="12e8e-123">hello report provides:</span></span>
  * <span data-ttu-id="12e8e-124">**TotalUserCount**: hello numero di tutti gli oggetti utente.</span><span class="sxs-lookup"><span data-stu-id="12e8e-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="12e8e-125">**OtherUserCount**: hello numero di utenti di Azure Active Directory (non gli utenti di Azure Active Directory B2C).</span><span class="sxs-lookup"><span data-stu-id="12e8e-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="12e8e-126">**LocalUserCount**: hello numero di account utente di Azure Active Directory B2C creato con tenant Azure Active Directory B2C di toohello locale le credenziali.</span><span class="sxs-lookup"><span data-stu-id="12e8e-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="12e8e-127">**AlternateIdUserCount**: numero hello di utenti di Azure Active Directory B2C registrato con provider di identità esterno (ad esempio, Facebook, un account Microsoft o un altro tenant di Azure Active Directory, denominato anche tooas un `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="12e8e-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="12e8e-128">**b2cAuthenticationCountSummary**: riepilogo numero giornaliero di hello di autenticazioni fatturabili su hello ultimi 30 giorni dal giorno e il tipo di flusso di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="12e8e-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="12e8e-129">**b2cAuthenticationCount**: hello numero di autenticazioni entro un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="12e8e-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="12e8e-130">valore predefinito di Hello è hello ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="12e8e-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="12e8e-131">(Facoltativo: hello all'inizio e fine `TimeStamp` parametri definiscono un periodo di tempo specifico.) sono inclusi l'output di hello `StartTimeStamp` (prima data dell'attività per questo tenant) e `EndTimeStamp` (ultimo aggiornamento).</span><span class="sxs-lookup"><span data-stu-id="12e8e-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="12e8e-132">**b2cMfaRequestCountSummary**: riepilogo del numero giornaliero di hello di autenticazioni di multi-factor, dal giorno e il tipo (SMS o vocale).</span><span class="sxs-lookup"><span data-stu-id="12e8e-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="12e8e-133">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="12e8e-133">Limitations</span></span>
<span data-ttu-id="12e8e-134">Dati di conteggio dell'utente viene aggiornati ogni 24 ore too48.</span><span class="sxs-lookup"><span data-stu-id="12e8e-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="12e8e-135">Le autenticazioni vengono aggiornate diverse volte al giorno.</span><span class="sxs-lookup"><span data-stu-id="12e8e-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="12e8e-136">Quando si utilizza hello `ApplicationId` filtro, una risposta di un report vuoto può essere dovuta tooone delle condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="12e8e-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="12e8e-137">ID dell'applicazione Hello non esiste nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="12e8e-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="12e8e-138">Verificare che sia corretto.</span><span class="sxs-lookup"><span data-stu-id="12e8e-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="12e8e-139">ID dell'applicazione Hello esiste, ma nessun dato è stato trovato nel periodo di reporting hello.</span><span class="sxs-lookup"><span data-stu-id="12e8e-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="12e8e-140">Controllare i valori dei parametri Data/Ora.</span><span class="sxs-lookup"><span data-stu-id="12e8e-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="12e8e-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12e8e-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="12e8e-142">Stime della fattura mensile per Azure AD</span><span class="sxs-lookup"><span data-stu-id="12e8e-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="12e8e-143">In combinazione con [hello aggiornate Azure Active Directory B2C disponibili prezzi](https://azure.microsoft.com/pricing/details/active-directory-b2c/), è possibile stimare giornaliera, settimana e mensile consumo di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e8e-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="12e8e-144">Questa stima è particolarmente utile quando si pianificano modifiche nel comportamento del tenant che potrebbero influire sul costo complessivo.</span><span class="sxs-lookup"><span data-stu-id="12e8e-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="12e8e-145">È possibile rivedere i costi attuali nella [sottoscrizione Azure collegata](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="12e8e-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="12e8e-146">Opzioni per altri formati di output</span><span class="sxs-lookup"><span data-stu-id="12e8e-146">Options for other output formats</span></span>
<span data-ttu-id="12e8e-147">Hello codice riportato di seguito vengono illustrati esempi di invio tooJSON output, un elenco di valori di nome e XML:</span><span class="sxs-lookup"><span data-stu-id="12e8e-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
