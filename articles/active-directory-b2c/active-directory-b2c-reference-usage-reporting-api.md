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
ms.openlocfilehash: 52180b760046d273c5a75720df0a73532d0343ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="b2fb1-103">Accesso ai report sull'uso in Azure AD B2C tramite l'API per la creazione di report</span><span class="sxs-lookup"><span data-stu-id="b2fb1-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="b2fb1-104">Azure Active Directory B2C (Azure AD B2C) fornisce l'autenticazione basata sull'accesso utente e sull'autenticazione a più fattori di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="b2fb1-105">L'autenticazione è disponibile per gli utenti finali della famiglia di applicazioni tra i provider di identità.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="b2fb1-106">Quando si conosce il numero di utenti registrati nel tenant, i provider usati per la registrazione e il numero di autenticazioni per tipo è possibile ottenere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2fb1-106">When you know the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="b2fb1-107">Numero di utenti per ogni tipo di provider di identità (ad esempio, account Microsoft o LinkedIn) registrati negli ultimi 10 giorni.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in the last 10 days?</span></span>
* <span data-ttu-id="b2fb1-108">Numero di autenticazioni che usano l'autenticazione a più fattori eseguite correttamente nell'ultimo mese.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-108">How many authentications using Multi-Factor Authentication have completed successfully in the last month?</span></span>
* <span data-ttu-id="b2fb1-109">Numero di autenticazioni basate su accesso eseguite correttamente nel mese corrente,</span><span class="sxs-lookup"><span data-stu-id="b2fb1-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="b2fb1-110">per ogni giorno</span><span class="sxs-lookup"><span data-stu-id="b2fb1-110">Per day?</span></span> <span data-ttu-id="b2fb1-111">e per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-111">Per application?</span></span>
* <span data-ttu-id="b2fb1-112">Previsione del costo mensile dell'attività del proprio tenant Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-112">How can I estimate the expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="b2fb1-113">Questo articolo si concentra sui report collegati all'attività di fatturazione, che si basa sul numero di utenti, di autenticazioni fatturabili basate su accesso e di autenticazioni a più fattori.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-113">This article focuses on reports tied to billing activity, which is based on the number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b2fb1-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b2fb1-114">Prerequisites</span></span>
<span data-ttu-id="b2fb1-115">Prima di iniziare è necessario completare i passaggi nei [prerequisiti per l'accesso alle API per la creazione di report di Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="b2fb1-115">Before you get started, you need to complete the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="b2fb1-116">Creare un'applicazione, ottenere il relativo segreto e concedere i diritti di accesso ai report del tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-116">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="b2fb1-117">Di seguito vengono riportati anche esempi di *script Bash* e *script Python*.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="b2fb1-118">Script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2fb1-118">PowerShell script</span></span>
<span data-ttu-id="b2fb1-119">Questo script illustra la creazione di quattro report sull'uso impiegando il parametro `TimeStamp` e il filtro `ApplicationId`.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-119">This script demonstrates the creation of four usage reports by using the `TimeStamp` parameter and the `ApplicationId` filter.</span></span>

```powershell
# This script will require the Web Application and permissions setup in Azure Active Directory

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

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="b2fb1-120">Definizioni dei report sull'uso</span><span class="sxs-lookup"><span data-stu-id="b2fb1-120">Usage report definitions</span></span>
* <span data-ttu-id="b2fb1-121">**tenantUserCount**: il numero di utenti del tenant al giorno per tipo di provider di identità negli ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-121">**tenantUserCount**: The number of users in the tenant by type of identity provider, per day in the last 30 days.</span></span> <span data-ttu-id="b2fb1-122">(Facoltativo: un filtro `TimeStamp` specifica il numero di utenti da una data specificata alla data attuale).</span><span class="sxs-lookup"><span data-stu-id="b2fb1-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date to the current date).</span></span> <span data-ttu-id="b2fb1-123">Questo report offre le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2fb1-123">The report provides:</span></span>
  * <span data-ttu-id="b2fb1-124">**TotalUserCount**: il numero totale degli oggetti utente.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-124">**TotalUserCount**: The number of all user objects.</span></span>
  * <span data-ttu-id="b2fb1-125">**OtherUserCount**: il numero di utenti di Azure Active Directory (non gli utenti di Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="b2fb1-125">**OtherUserCount**: The number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="b2fb1-126">**LocalUserCount**: il numero di account utente Azure AD B2C creati con le credenziali locali di accesso al tenant Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-126">**LocalUserCount**: The number of Azure AD B2C user accounts created with credentials local to the Azure AD B2C tenant.</span></span>

* <span data-ttu-id="b2fb1-127">**AlternateIdUserCount**: il numero di utenti di Azure AD B2C registrati con provider di identità esterno (ad esempio, Facebook, un account Microsoft o un altro tenant di Azure Active Directory, detto anche `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="b2fb1-127">**AlternateIdUserCount**: The number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred to as an `OrgId`).</span></span>

* <span data-ttu-id="b2fb1-128">**b2cAuthenticationCountSummary**: il riepilogo del numero giornaliero di autenticazioni fatturabili eseguite negli ultimi 30 giorni, per data e per tipo di flusso di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-128">**b2cAuthenticationCountSummary**: Summary of the daily number of billable authentications over the last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="b2fb1-129">**b2cAuthenticationCount**: il numero di autenticazioni eseguite entro un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-129">**b2cAuthenticationCount**: The number of authentications within a time period.</span></span> <span data-ttu-id="b2fb1-130">Il valore predefinito corrisponde agli ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-130">The default is the last 30 days.</span></span>  <span data-ttu-id="b2fb1-131">(Facoltativo: i parametri `TimeStamp` di inizio e fine definiscono un periodo di tempo specifico). L'output include `StartTimeStamp` (prima data dell'attività per questo tenant) e `EndTimeStamp` (ultimo aggiornamento).</span><span class="sxs-lookup"><span data-stu-id="b2fb1-131">(Optional: The beginning and ending `TimeStamp` parameters define a specific time period.) The output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="b2fb1-132">**b2cMfaRequestCountSummary**: il riepilogo del numero giornaliero di autenticazioni a più fattori (voce o SMS), per data e per tipo.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-132">**b2cMfaRequestCountSummary**: Summary of the daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="b2fb1-133">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="b2fb1-133">Limitations</span></span>
<span data-ttu-id="b2fb1-134">I dati relativi al numero di utenti vengono aggiornati con una frequenza compresa tra 24 e 48 ore.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-134">User count data is refreshed every 24 to 48 hours.</span></span> <span data-ttu-id="b2fb1-135">Le autenticazioni vengono aggiornate diverse volte al giorno.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="b2fb1-136">Quando si usa il filtro `ApplicationId`, se si ottiene un report vuoto la causa può essere una delle seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2fb1-136">When using the `ApplicationId` filter, an empty report response can be due to one of following conditions:</span></span>
  * <span data-ttu-id="b2fb1-137">L'ID dell'applicazione non esiste nel tenant.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-137">The application ID does not exist in the tenant.</span></span> <span data-ttu-id="b2fb1-138">Verificare che sia corretto.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="b2fb1-139">L'ID dell'applicazione esiste, ma non sono stati trovati dati nel periodo di reporting selezionato.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-139">The application ID exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="b2fb1-140">Controllare i valori dei parametri Data/Ora.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b2fb1-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2fb1-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="b2fb1-142">Stime della fattura mensile per Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2fb1-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="b2fb1-143">È possibile fare riferimento ai [prezzi più aggiornati di Azure AD B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/) per stimare il proprio consumo di Azure giornaliero, settimanale e mensile.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-143">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="b2fb1-144">Questa stima è particolarmente utile quando si pianificano modifiche nel comportamento del tenant che potrebbero influire sul costo complessivo.</span><span class="sxs-lookup"><span data-stu-id="b2fb1-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="b2fb1-145">È possibile rivedere i costi attuali nella [sottoscrizione Azure collegata](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="b2fb1-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="b2fb1-146">Opzioni per altri formati di output</span><span class="sxs-lookup"><span data-stu-id="b2fb1-146">Options for other output formats</span></span>
<span data-ttu-id="b2fb1-147">Il codice seguente illustra esempi di invio di output a JSON, un elenco di valori nome, e XML:</span><span class="sxs-lookup"><span data-stu-id="b2fb1-147">The following code shows examples of sending output to JSON, a name value list, and XML:</span></span>
```powershell
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
