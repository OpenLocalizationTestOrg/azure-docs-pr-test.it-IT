---
title: "report attività aaaAzure sign-in Active Directory riferimenti alle API | Documenti Microsoft"
description: "Riferimento per il report attività hello sign-in Azure Active Directory API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="a5260-103">Riferimento API del report sull'attività di accesso di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5260-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="a5260-104">Questo argomento fa parte di una raccolta di argomenti sull'hello Azure Active Directory reporting API.</span><span class="sxs-lookup"><span data-stu-id="a5260-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="a5260-105">Report di Azure AD fornisce un'API che consente di dati del report attività di accesso tooaccess tramite codice o gli strumenti correlati.</span><span class="sxs-lookup"><span data-stu-id="a5260-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="a5260-106">Hello l'ambito di questo argomento è tooprovide con informazioni di riferimento su hello **Accedi attività report API**.</span><span class="sxs-lookup"><span data-stu-id="a5260-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="a5260-107">Vedere:</span><span class="sxs-lookup"><span data-stu-id="a5260-107">See:</span></span>

* <span data-ttu-id="a5260-108">[Attività di accesso](active-directory-reporting-azure-portal.md#activity-reports) .</span><span class="sxs-lookup"><span data-stu-id="a5260-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="a5260-109">[Introduzione a hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) per ulteriori informazioni sulle API di segnalazione hello.</span><span class="sxs-lookup"><span data-stu-id="a5260-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="a5260-110">Chi può accedere a dati API hello?</span><span class="sxs-lookup"><span data-stu-id="a5260-110">Who can access hello API data?</span></span>
* <span data-ttu-id="a5260-111">Utenti ed entità servizio ruolo di amministratore responsabile della sicurezza o sicurezza lettore hello</span><span class="sxs-lookup"><span data-stu-id="a5260-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="a5260-112">Gli amministratori globali</span><span class="sxs-lookup"><span data-stu-id="a5260-112">Global Admins</span></span>
* <span data-ttu-id="a5260-113">Qualsiasi applicazione che dispone di autorizzazione tooaccess hello API (autorizzazione app può essere il programma di installazione solo in base alle autorizzazioni dell'amministratore globale)</span><span class="sxs-lookup"><span data-stu-id="a5260-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="a5260-114">accesso tooconfigure per un'applicazione tooaccess sicurezza API, ad esempio gli eventi di accesso, utilizzare hello seguenti applicazioni di hello tooadd PowerShell dell'entità servizio nel ruolo di sicurezza Reader hello</span><span class="sxs-lookup"><span data-stu-id="a5260-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="a5260-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5260-115">Prerequisites</span></span>
<span data-ttu-id="a5260-116">Questo report tramite tooaccess hello API di creazione di report, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="a5260-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="a5260-117">Disporre di [Azure Active Directory Premium, edizione P1 o P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="a5260-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="a5260-118">Hello completato [prerequisiti tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="a5260-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="a5260-119">L'accesso API hello</span><span class="sxs-lookup"><span data-stu-id="a5260-119">Accessing hello API</span></span>
<span data-ttu-id="a5260-120">È possibile accedere a questa API tramite hello [Esplora grafico](https://graphexplorer2.cloudapp.net) o a livello di codice, ad esempio tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5260-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="a5260-121">Per PowerShell toocorrectly interpretare sintassi del filtro OData hello usata nelle chiamate REST Graph di Azure ad, è necessario utilizzare apice inverso hello (noto anche come: accento grave) carattere troppo "carattere di escape" hello $.</span><span class="sxs-lookup"><span data-stu-id="a5260-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="a5260-122">funge da carattere apice inverso Hello [carattere di escape di PowerShell](https://technet.microsoft.com/library/hh847755.aspx), consentendo alle toodo PowerShell un'interpretazione di valore letterale di carattere $ hello ed evitare di confondere, come un nome di variabile di PowerShell (ad esempio: $filter).</span><span class="sxs-lookup"><span data-stu-id="a5260-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="a5260-123">hello Esplora grafico è attivo Hello di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="a5260-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="a5260-124">Per un esempio di PowerShell, vedere questo [script di PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="a5260-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="a5260-125">Endpoint API</span><span class="sxs-lookup"><span data-stu-id="a5260-125">API Endpoint</span></span>
<span data-ttu-id="a5260-126">È possibile accedere a questa API utilizzando hello seguente URI di base:</span><span class="sxs-lookup"><span data-stu-id="a5260-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="a5260-127">A causa di toohello volume di dati, questa API è un limite di un milione di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="a5260-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="a5260-128">Questa chiamata non restituisce dati hello in batch.</span><span class="sxs-lookup"><span data-stu-id="a5260-128">This call returns hello data in batches.</span></span> <span data-ttu-id="a5260-129">Ogni batch contiene un massimo di 1000 record.</span><span class="sxs-lookup"><span data-stu-id="a5260-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="a5260-130">tooget hello successivo gruppo di record, utilizzare hello del collegamento successivo.</span><span class="sxs-lookup"><span data-stu-id="a5260-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="a5260-131">Ottenere hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informazioni hello primo gruppo di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="a5260-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="a5260-132">token skip Hello sarà alla fine di hello hello di set di risultati.</span><span class="sxs-lookup"><span data-stu-id="a5260-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="a5260-133">Filtri supportati</span><span class="sxs-lookup"><span data-stu-id="a5260-133">Supported filters</span></span>
<span data-ttu-id="a5260-134">È possibile limitare il numero di hello di record restituiti da un'API chiamata sotto forma di un filtro.</span><span class="sxs-lookup"><span data-stu-id="a5260-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="a5260-135">Per l'API di accesso sono supportati i dati correlati, hello seguenti filtri:</span><span class="sxs-lookup"><span data-stu-id="a5260-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="a5260-136">**$top =\<restituito un numero di record toobe\>**  -numero di hello toolimit di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="a5260-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="a5260-137">Si tratta di un'operazione impegnativa.</span><span class="sxs-lookup"><span data-stu-id="a5260-137">This is an expensive operation.</span></span> <span data-ttu-id="a5260-138">Utilizzare questo filtro non se si desidera tooreturn migliaia di oggetti.</span><span class="sxs-lookup"><span data-stu-id="a5260-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="a5260-139">**$filter =\<l'istruzione di filtro\>**  -toospecify, su base hello di campi di filtro supportato, il tipo di hello di record è rilevante</span><span class="sxs-lookup"><span data-stu-id="a5260-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="a5260-140">Operatori e campi dei filtri supportati</span><span class="sxs-lookup"><span data-stu-id="a5260-140">Supported filter fields and operators</span></span>
<span data-ttu-id="a5260-141">tipo di hello toospecify di record che è rilevante, è possibile compilare un'istruzione di filtro che può contenere uno o una combinazione di hello campi filtro seguente:</span><span class="sxs-lookup"><span data-stu-id="a5260-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="a5260-142">[signinDateTime](#signindatetime) : definisce una data o un intervallo di date</span><span class="sxs-lookup"><span data-stu-id="a5260-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="a5260-143">[userId](#userid) -definisce l'ID. dell'utente un utente specifico in base hello</span><span class="sxs-lookup"><span data-stu-id="a5260-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="a5260-144">[userPrincipalName](#userprincipalname) -definisce un utente specifico in base hello dell'utente nome entità utente (UPN)</span><span class="sxs-lookup"><span data-stu-id="a5260-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="a5260-145">[appId](#appid) -definisce un'app specifica in base hello dell'ID app</span><span class="sxs-lookup"><span data-stu-id="a5260-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="a5260-146">[appDisplayName](#appdisplayname) -nome visualizzato dell'applicazione hello di app specifici in base</span><span class="sxs-lookup"><span data-stu-id="a5260-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="a5260-147">[loginStatus](#loginStatus) -definisce lo stato di hello degli account di accesso hello (esito positivo o negativo)</span><span class="sxs-lookup"><span data-stu-id="a5260-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="a5260-148">Quando si utilizza Esplora grafico, hello è necessario toouse hello corretto case per ogni lettera è i campi filtro.</span><span class="sxs-lookup"><span data-stu-id="a5260-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="a5260-149">toonarrow all'ambito hello di hello ha restituito dati, è possibile compilare combinazioni di filtri hello supportato e i campi di filtro.</span><span class="sxs-lookup"><span data-stu-id="a5260-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="a5260-150">Ad esempio, hello istruzione seguente restituisce hello top 10 record tra 2016 1 ° luglio e luglio 2016 6:</span><span class="sxs-lookup"><span data-stu-id="a5260-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="a5260-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="a5260-151">signinDateTime</span></span>
<span data-ttu-id="a5260-152">**Operatori supportati**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="a5260-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="a5260-153">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="a5260-153">**Example**:</span></span>

<span data-ttu-id="a5260-154">Uso di una data specifica</span><span class="sxs-lookup"><span data-stu-id="a5260-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="a5260-155">Uso di un intervallo di date</span><span class="sxs-lookup"><span data-stu-id="a5260-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="a5260-156">**Note**:</span><span class="sxs-lookup"><span data-stu-id="a5260-156">**Notes**:</span></span>

<span data-ttu-id="a5260-157">parametro datetime Hello deve essere in formato UTC hello</span><span class="sxs-lookup"><span data-stu-id="a5260-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="a5260-158">userId</span><span class="sxs-lookup"><span data-stu-id="a5260-158">userId</span></span>
<span data-ttu-id="a5260-159">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="a5260-159">**Supported operators**: eq</span></span>

<span data-ttu-id="a5260-160">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="a5260-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="a5260-161">**Note**:</span><span class="sxs-lookup"><span data-stu-id="a5260-161">**Notes**:</span></span>

<span data-ttu-id="a5260-162">il valore di Hello UserID è un valore stringa</span><span class="sxs-lookup"><span data-stu-id="a5260-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="a5260-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="a5260-163">userPrincipalName</span></span>
<span data-ttu-id="a5260-164">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="a5260-164">**Supported operators**: eq</span></span>

<span data-ttu-id="a5260-165">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="a5260-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="a5260-166">**Note**:</span><span class="sxs-lookup"><span data-stu-id="a5260-166">**Notes**:</span></span>

<span data-ttu-id="a5260-167">il valore userPrincipalName Hello è un valore stringa</span><span class="sxs-lookup"><span data-stu-id="a5260-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="a5260-168">appId</span><span class="sxs-lookup"><span data-stu-id="a5260-168">appId</span></span>
<span data-ttu-id="a5260-169">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="a5260-169">**Supported operators**: eq</span></span>

<span data-ttu-id="a5260-170">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="a5260-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="a5260-171">**Note**:</span><span class="sxs-lookup"><span data-stu-id="a5260-171">**Notes**:</span></span>

<span data-ttu-id="a5260-172">il valore appId Hello è un valore stringa</span><span class="sxs-lookup"><span data-stu-id="a5260-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="a5260-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="a5260-173">appDisplayName</span></span>
<span data-ttu-id="a5260-174">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="a5260-174">**Supported operators**: eq</span></span>

<span data-ttu-id="a5260-175">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="a5260-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="a5260-176">**Note**:</span><span class="sxs-lookup"><span data-stu-id="a5260-176">**Notes**:</span></span>

<span data-ttu-id="a5260-177">valore Hello appDisplayName è un valore stringa</span><span class="sxs-lookup"><span data-stu-id="a5260-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="a5260-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="a5260-178">loginStatus</span></span>
<span data-ttu-id="a5260-179">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="a5260-179">**Supported operators**: eq</span></span>

<span data-ttu-id="a5260-180">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="a5260-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="a5260-181">**Note**:</span><span class="sxs-lookup"><span data-stu-id="a5260-181">**Notes**:</span></span>

<span data-ttu-id="a5260-182">Sono disponibili due opzioni per hello loginStatus: 0 - esito positivo, 1 - errore</span><span class="sxs-lookup"><span data-stu-id="a5260-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="a5260-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5260-183">Next steps</span></span>
* <span data-ttu-id="a5260-184">Si desidera toosee esempi per attività filtrate Accedi?</span><span class="sxs-lookup"><span data-stu-id="a5260-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="a5260-185">Estrarre hello [gli esempi di API report attività di accesso di Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a5260-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="a5260-186">Si desidera tooknow ulteriori informazioni sull'API di creazione di report hello Azure AD?</span><span class="sxs-lookup"><span data-stu-id="a5260-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="a5260-187">Vedere [introduzione hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a5260-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

