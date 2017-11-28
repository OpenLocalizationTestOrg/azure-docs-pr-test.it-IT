---
title: controllo di Active Directory aaaAzure riferimento API | Documenti Microsoft
description: "La modalità di avvio tooget con hello API di controllo di Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="c560c-103">Informazioni di riferimento sull'API di controllo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c560c-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="c560c-104">Questo argomento fa parte di una raccolta di argomenti sull'hello Azure Active Directory reporting API.</span><span class="sxs-lookup"><span data-stu-id="c560c-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="c560c-105">Azure Active Directory reporting fornisce un'API che consente di dati di controllo tooaccess tramite codice o gli strumenti correlati.</span><span class="sxs-lookup"><span data-stu-id="c560c-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="c560c-106">Hello l'ambito di questo argomento è tooprovide con informazioni di riferimento su hello **audit API**.</span><span class="sxs-lookup"><span data-stu-id="c560c-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="c560c-107">Vedere:</span><span class="sxs-lookup"><span data-stu-id="c560c-107">See:</span></span>

* <span data-ttu-id="c560c-108">[Log di controllo](active-directory-reporting-azure-portal.md#activity-reports) per informazioni più concettuali</span><span class="sxs-lookup"><span data-stu-id="c560c-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="c560c-109">[Introduzione a hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) per ulteriori informazioni sulle API di segnalazione hello.</span><span class="sxs-lookup"><span data-stu-id="c560c-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="c560c-110">Per:</span><span class="sxs-lookup"><span data-stu-id="c560c-110">For:</span></span>

- <span data-ttu-id="c560c-111">Domande frequenti, leggere le [Domande Frequenti](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c560c-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="c560c-112">Problemi, [inviare un ticket di supporto](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="c560c-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="c560c-113">Chi può accedere a dati hello?</span><span class="sxs-lookup"><span data-stu-id="c560c-113">Who can access hello data?</span></span>
* <span data-ttu-id="c560c-114">Utenti nel ruolo di amministratore responsabile della sicurezza o di sicurezza Reader hello</span><span class="sxs-lookup"><span data-stu-id="c560c-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="c560c-115">Gli amministratori globali</span><span class="sxs-lookup"><span data-stu-id="c560c-115">Global Admins</span></span>
* <span data-ttu-id="c560c-116">Qualsiasi applicazione che dispone di autorizzazione tooaccess hello API (autorizzazione app può essere il programma di installazione solo in base alle autorizzazioni dell'amministratore globale)</span><span class="sxs-lookup"><span data-stu-id="c560c-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c560c-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c560c-117">Prerequisites</span></span>
<span data-ttu-id="c560c-118">In questo report tramite tooaccess di ordine hello API di Reporting, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="c560c-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="c560c-119">Un' [edizione gratuita di Azure Active Directory o superiore](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="c560c-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="c560c-120">Hello completato [prerequisiti tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="c560c-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="c560c-121">L'accesso API hello</span><span class="sxs-lookup"><span data-stu-id="c560c-121">Accessing hello API</span></span>
<span data-ttu-id="c560c-122">È possibile accedere a questa API tramite hello [Esplora grafico](https://graphexplorer2.cloudapp.net) o a livello di codice, ad esempio tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c560c-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="c560c-123">Per PowerShell toocorrectly interpretare sintassi del filtro OData hello usata nelle chiamate REST Graph di Azure ad, è necessario utilizzare apice inverso hello (noto anche come: accento grave) carattere troppo "carattere di escape" hello $.</span><span class="sxs-lookup"><span data-stu-id="c560c-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="c560c-124">funge da carattere apice inverso Hello [carattere di escape di PowerShell](https://technet.microsoft.com/library/hh847755.aspx), consentendo alle toodo PowerShell un'interpretazione di valore letterale di carattere $ hello ed evitare di confondere, come un nome di variabile di PowerShell (ad esempio: $filter).</span><span class="sxs-lookup"><span data-stu-id="c560c-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="c560c-125">hello Esplora grafico è attivo Hello di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="c560c-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="c560c-126">Per un esempio di PowerShell, vedere questo [script di PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="c560c-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="c560c-127">Endpoint API</span><span class="sxs-lookup"><span data-stu-id="c560c-127">API Endpoint</span></span>
<span data-ttu-id="c560c-128">È possibile accedere a questa API utilizzando hello seguente URI:</span><span class="sxs-lookup"><span data-stu-id="c560c-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="c560c-129">Non è previsto alcun limite per il numero di hello di record restituito dall'API di controllo hello Azure AD (mediante la paginazione OData).</span><span class="sxs-lookup"><span data-stu-id="c560c-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="c560c-130">Per i limiti di conservazione sui dati dei report, consultare [Criteri di conservazione dei report](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="c560c-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="c560c-131">Questa chiamata non restituisce dati hello in batch.</span><span class="sxs-lookup"><span data-stu-id="c560c-131">This call returns hello data in batches.</span></span> <span data-ttu-id="c560c-132">Ogni batch contiene un massimo di 1000 record.</span><span class="sxs-lookup"><span data-stu-id="c560c-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="c560c-133">tooget hello successivo gruppo di record, utilizzare hello del collegamento successivo.</span><span class="sxs-lookup"><span data-stu-id="c560c-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="c560c-134">Ottenere informazioni skiptoken hello dal primo set di hello di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="c560c-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="c560c-135">token skip Hello sarà alla fine di hello hello di set di risultati.</span><span class="sxs-lookup"><span data-stu-id="c560c-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="c560c-136">Filtri supportati</span><span class="sxs-lookup"><span data-stu-id="c560c-136">Supported filters</span></span>
<span data-ttu-id="c560c-137">È possibile limitare il numero di hello di record restituiti da un'API chiamata sotto forma di un filtro.</span><span class="sxs-lookup"><span data-stu-id="c560c-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="c560c-138">Per l'API di accesso sono supportati i dati correlati, hello seguenti filtri:</span><span class="sxs-lookup"><span data-stu-id="c560c-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="c560c-139">**$top =\<restituito un numero di record toobe\>**  -numero di hello toolimit di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="c560c-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="c560c-140">Si tratta di un'operazione impegnativa.</span><span class="sxs-lookup"><span data-stu-id="c560c-140">This is an expensive operation.</span></span> <span data-ttu-id="c560c-141">Utilizzare questo filtro non se si desidera tooreturn migliaia di oggetti.</span><span class="sxs-lookup"><span data-stu-id="c560c-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="c560c-142">**$filter =\<l'istruzione di filtro\>**  -toospecify, su base hello di campi di filtro supportato, il tipo di hello di record è rilevante</span><span class="sxs-lookup"><span data-stu-id="c560c-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="c560c-143">Operatori e campi dei filtri supportati</span><span class="sxs-lookup"><span data-stu-id="c560c-143">Supported filter fields and operators</span></span>
<span data-ttu-id="c560c-144">tipo di hello toospecify di record che è rilevante, è possibile compilare un'istruzione di filtro che può contenere uno o una combinazione di hello campi filtro seguente:</span><span class="sxs-lookup"><span data-stu-id="c560c-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="c560c-145">[activityDate](#activitydate): definisce una data o un intervallo di date</span><span class="sxs-lookup"><span data-stu-id="c560c-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="c560c-146">[categoria](#category) -definisce la categoria di hello desiderato toofilter.</span><span class="sxs-lookup"><span data-stu-id="c560c-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="c560c-147">[activityStatus](#activitystatus) -definisce hello stato di un'attività</span><span class="sxs-lookup"><span data-stu-id="c560c-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="c560c-148">[la proprietà activityType](#activitytype) -definisce il tipo di hello di un'attività</span><span class="sxs-lookup"><span data-stu-id="c560c-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="c560c-149">[attività](#activity) -definisce attività hello come stringa</span><span class="sxs-lookup"><span data-stu-id="c560c-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="c560c-150">[Nome/attore](#actorname) -definisce attore hello in forma di nome hello actor</span><span class="sxs-lookup"><span data-stu-id="c560c-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="c560c-151">[attore/objectid](#actorobjectid) -definisce attore hello in forma di ID dell'attore hello</span><span class="sxs-lookup"><span data-stu-id="c560c-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="c560c-152">[attore/upn](#actorupn) -definisce attore hello in forma di nome dell'entità utente (UPN) dell'attore hello</span><span class="sxs-lookup"><span data-stu-id="c560c-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="c560c-153">[nome didestinazione/](#targetname) -definisce la destinazione hello sotto forma di nome hello actor</span><span class="sxs-lookup"><span data-stu-id="c560c-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="c560c-154">[destinazione/objectid](#targetobjectid) -definisce la destinazione hello sotto forma di ID del database di destinazione di hello</span><span class="sxs-lookup"><span data-stu-id="c560c-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="c560c-155">[destinazione/upn](#targetupn) -definisce attore hello in forma di nome dell'entità utente (UPN) dell'attore hello</span><span class="sxs-lookup"><span data-stu-id="c560c-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="c560c-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="c560c-156">activityDate</span></span>
<span data-ttu-id="c560c-157">**Operatori supportati**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="c560c-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="c560c-158">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="c560c-159">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c560c-159">**Notes**:</span></span>

<span data-ttu-id="c560c-160">datetime deve essere in formato UTC</span><span class="sxs-lookup"><span data-stu-id="c560c-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="c560c-161">category</span><span class="sxs-lookup"><span data-stu-id="c560c-161">category</span></span>

<span data-ttu-id="c560c-162">**Valori supportati**:</span><span class="sxs-lookup"><span data-stu-id="c560c-162">**Supported values**:</span></span>

| <span data-ttu-id="c560c-163">Categoria</span><span class="sxs-lookup"><span data-stu-id="c560c-163">Category</span></span>                         | <span data-ttu-id="c560c-164">Valore</span><span class="sxs-lookup"><span data-stu-id="c560c-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="c560c-165">Directory principale</span><span class="sxs-lookup"><span data-stu-id="c560c-165">Core Directory</span></span>                   | <span data-ttu-id="c560c-166">Directory</span><span class="sxs-lookup"><span data-stu-id="c560c-166">Directory</span></span> |
| <span data-ttu-id="c560c-167">Gestione delle password self-service</span><span class="sxs-lookup"><span data-stu-id="c560c-167">Self-service Password Management</span></span> | <span data-ttu-id="c560c-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="c560c-168">SSPR</span></span>      |
| <span data-ttu-id="c560c-169">Gestione gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="c560c-169">Self-service Group Management</span></span>    | <span data-ttu-id="c560c-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="c560c-170">SSGM</span></span>      |
| <span data-ttu-id="c560c-171">Provisioning degli account</span><span class="sxs-lookup"><span data-stu-id="c560c-171">Account Provisioning</span></span>             | <span data-ttu-id="c560c-172">Sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="c560c-172">Sync</span></span>      |
| <span data-ttu-id="c560c-173">Automated Password Rollover (Rollover automatizzato delle password)</span><span class="sxs-lookup"><span data-stu-id="c560c-173">Automated Password Rollover</span></span>      | <span data-ttu-id="c560c-174">Automated Password Rollover (Rollover automatizzato delle password)</span><span class="sxs-lookup"><span data-stu-id="c560c-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="c560c-175">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="c560c-175">Identity Protection</span></span>              | <span data-ttu-id="c560c-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="c560c-176">IdentityProtection</span></span> |
| <span data-ttu-id="c560c-177">Utenti invitati</span><span class="sxs-lookup"><span data-stu-id="c560c-177">Invited Users</span></span>                    | <span data-ttu-id="c560c-178">Utenti invitati</span><span class="sxs-lookup"><span data-stu-id="c560c-178">Invited Users</span></span> |
| <span data-ttu-id="c560c-179">Servizio MIM</span><span class="sxs-lookup"><span data-stu-id="c560c-179">MIM Service</span></span>                      | <span data-ttu-id="c560c-180">Servizio MIM</span><span class="sxs-lookup"><span data-stu-id="c560c-180">MIM Service</span></span> |



<span data-ttu-id="c560c-181">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c560c-181">**Supported operators**: eq</span></span>

<span data-ttu-id="c560c-182">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="c560c-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="c560c-183">activityStatus</span></span>

<span data-ttu-id="c560c-184">**Valori supportati**:</span><span class="sxs-lookup"><span data-stu-id="c560c-184">**Supported values**:</span></span>

| <span data-ttu-id="c560c-185">Stato attività</span><span class="sxs-lookup"><span data-stu-id="c560c-185">Activity Status</span></span> | <span data-ttu-id="c560c-186">Valore</span><span class="sxs-lookup"><span data-stu-id="c560c-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="c560c-187">Success</span><span class="sxs-lookup"><span data-stu-id="c560c-187">Success</span></span>         | <span data-ttu-id="c560c-188">0</span><span class="sxs-lookup"><span data-stu-id="c560c-188">0</span></span>     |
| <span data-ttu-id="c560c-189">Esito negativo</span><span class="sxs-lookup"><span data-stu-id="c560c-189">Failure</span></span>         | <span data-ttu-id="c560c-190">- 1</span><span class="sxs-lookup"><span data-stu-id="c560c-190">- 1</span></span>   |

<span data-ttu-id="c560c-191">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c560c-191">**Supported operators**: eq</span></span>

<span data-ttu-id="c560c-192">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="c560c-193">activityType</span><span class="sxs-lookup"><span data-stu-id="c560c-193">activityType</span></span>
<span data-ttu-id="c560c-194">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c560c-194">**Supported operators**: eq</span></span>

<span data-ttu-id="c560c-195">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="c560c-196">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c560c-196">**Notes**:</span></span>

<span data-ttu-id="c560c-197">fa distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="c560c-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="c560c-198">activity</span><span class="sxs-lookup"><span data-stu-id="c560c-198">activity</span></span>
<span data-ttu-id="c560c-199">**Operatori supportati**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="c560c-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="c560c-200">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="c560c-201">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c560c-201">**Notes**:</span></span>

<span data-ttu-id="c560c-202">fa distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="c560c-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="c560c-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="c560c-203">actor/name</span></span>
<span data-ttu-id="c560c-204">**Operatori supportati**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="c560c-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="c560c-205">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="c560c-206">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c560c-206">**Notes**:</span></span>

<span data-ttu-id="c560c-207">non fa distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="c560c-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="c560c-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="c560c-208">actor/objectId</span></span>
<span data-ttu-id="c560c-209">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c560c-209">**Supported operators**: eq</span></span>

<span data-ttu-id="c560c-210">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="c560c-211">target/name</span><span class="sxs-lookup"><span data-stu-id="c560c-211">target/name</span></span>
<span data-ttu-id="c560c-212">**Operatori supportati**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="c560c-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="c560c-213">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="c560c-214">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c560c-214">**Notes**:</span></span>

<span data-ttu-id="c560c-215">non fa distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="c560c-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="c560c-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="c560c-216">target/upn</span></span>
<span data-ttu-id="c560c-217">**Operatori supportati**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="c560c-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="c560c-218">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="c560c-219">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c560c-219">**Notes**:</span></span>

* <span data-ttu-id="c560c-220">non fa distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="c560c-220">Case-insensitive</span></span>
* <span data-ttu-id="c560c-221">È necessario hello tooadd completo dello spazio dei nomi quando si eseguono query Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="c560c-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="c560c-222">target/name</span><span class="sxs-lookup"><span data-stu-id="c560c-222">target/objectId</span></span>
<span data-ttu-id="c560c-223">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c560c-223">**Supported operators**: eq</span></span>

<span data-ttu-id="c560c-224">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="c560c-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="c560c-225">actor/upn</span></span>
<span data-ttu-id="c560c-226">**Operatori supportati**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="c560c-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="c560c-227">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c560c-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="c560c-228">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c560c-228">**Notes**:</span></span>

* <span data-ttu-id="c560c-229">non fa distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="c560c-229">Case-insensitive</span></span> 
* <span data-ttu-id="c560c-230">È necessario hello tooadd completo dello spazio dei nomi quando si eseguono query Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="c560c-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="c560c-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c560c-231">Next Steps</span></span>
* <span data-ttu-id="c560c-232">Specificare se toosee esempi per attività di sistema filtrato.</span><span class="sxs-lookup"><span data-stu-id="c560c-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="c560c-233">Estrarre hello [esempi di API di controllo di Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c560c-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="c560c-234">Si desidera tooknow ulteriori informazioni sull'API di creazione di report hello Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c560c-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="c560c-235">Vedere [introduzione hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c560c-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

