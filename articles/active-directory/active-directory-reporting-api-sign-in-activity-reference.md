---
title: "Riferimento API del report sull'attività di accesso di Azure Active Directory | Microsoft Docs"
description: "Riferimento API del report sull'attività di accesso di Azure Active Directory"
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
ms.openlocfilehash: d83f1a899ba38dab2c1c1661adede87db6f88c20
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="c1be2-103">Riferimento API del report sull'attività di accesso di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1be2-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="c1be2-104">Questo argomento fa parte di una raccolta di argomenti sull'API di creazione report di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1be2-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="c1be2-105">La creazione di report di Azure Active Directory fornisce un'API che consente di accedere ai dati del report sull'attività di accesso tramite codice o strumenti correlati.</span><span class="sxs-lookup"><span data-stu-id="c1be2-105">Azure AD reporting provides you with an API that enables you to access sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="c1be2-106">L'obiettivo di questo argomento è fornire informazioni di riferimento sull' **API del report sull'attività di accesso**.</span><span class="sxs-lookup"><span data-stu-id="c1be2-106">The scope of this topic is to provide you with reference information about the **sign-in activity report API**.</span></span>

<span data-ttu-id="c1be2-107">Vedere:</span><span class="sxs-lookup"><span data-stu-id="c1be2-107">See:</span></span>

* <span data-ttu-id="c1be2-108">[Attività di accesso](active-directory-reporting-azure-portal.md#activity-reports) .</span><span class="sxs-lookup"><span data-stu-id="c1be2-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="c1be2-109">[Introduzione all'API di creazione report di Azure Active Directory](active-directory-reporting-api-getting-started.md) .</span><span class="sxs-lookup"><span data-stu-id="c1be2-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="who-can-access-the-api-data"></a><span data-ttu-id="c1be2-110">Chi può accedere ai dati dell'API?</span><span class="sxs-lookup"><span data-stu-id="c1be2-110">Who can access the API data?</span></span>
* <span data-ttu-id="c1be2-111">Utenti ed entità servizio nel ruolo di amministratore della sicurezza o con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="c1be2-111">Users and Service Principals in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="c1be2-112">Gli amministratori globali</span><span class="sxs-lookup"><span data-stu-id="c1be2-112">Global Admins</span></span>
* <span data-ttu-id="c1be2-113">Qualsiasi applicazione che dispone di autorizzazione per accedere all'API. L'autorizzazione dell'app può essere configurata solo in base alle autorizzazioni dell'amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="c1be2-113">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="c1be2-114">Per configurare l'accesso per un'applicazione che usa API di sicurezza, ad esempio eventi di accesso, usare questo comando PowerShell per aggiungere le entità servizio delle applicazioni al ruolo con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="c1be2-114">To configure access for an application to access security APIs such as signin events, use the following PowerShell to add the applications Service Principal into the Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="c1be2-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c1be2-115">Prerequisites</span></span>
<span data-ttu-id="c1be2-116">Per accedere a questo report tramite l'API di creazione report, è necessario:</span><span class="sxs-lookup"><span data-stu-id="c1be2-116">To access this report through the reporting API, you must have:</span></span>

* <span data-ttu-id="c1be2-117">Disporre di [Azure Active Directory Premium, edizione P1 o P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="c1be2-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="c1be2-118">Aver completato i [prerequisiti di accesso all'API di creazione report di Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="c1be2-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="c1be2-119">Accesso all'API</span><span class="sxs-lookup"><span data-stu-id="c1be2-119">Accessing the API</span></span>
<span data-ttu-id="c1be2-120">È possibile accedere a questa API tramite [Graph Explorer](https://graphexplorer2.cloudapp.net) o a livello di codice, ad esempio usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1be2-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="c1be2-121">Al fine di consentire a Per PowerShell di interpretare correttamente la sintassi del filtro OData usata nelle chiamate REST di Graph di AAD, è necessario fare uso dell'apice inverso, ovvero l'accento grave, per eseguire l'"escape" del carattere $.</span><span class="sxs-lookup"><span data-stu-id="c1be2-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="c1be2-122">L'apice inverso viene usato come [carattere di escape di PowerShell](https://technet.microsoft.com/library/hh847755.aspx)e consente a PowerShell di eseguire un'interpretazione letterale del carattere $, che evita la confusione con il nome di una variabile di PowerShell (ad esempio: $filter).</span><span class="sxs-lookup"><span data-stu-id="c1be2-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="c1be2-123">Questo argomento si concentra su Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="c1be2-123">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="c1be2-124">Per un esempio di PowerShell, vedere questo [script di PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="c1be2-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="c1be2-125">Endpoint API</span><span class="sxs-lookup"><span data-stu-id="c1be2-125">API Endpoint</span></span>
<span data-ttu-id="c1be2-126">È possibile accedere a questa API tramite l'URI di base seguente:</span><span class="sxs-lookup"><span data-stu-id="c1be2-126">You can access this API using the following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="c1be2-127">A causa del volume di dati, questa API presenta un limite di un milione di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="c1be2-127">Due to the volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="c1be2-128">Questa chiamata restituisce i dati in batch.</span><span class="sxs-lookup"><span data-stu-id="c1be2-128">This call returns the data in batches.</span></span> <span data-ttu-id="c1be2-129">Ogni batch contiene un massimo di 1000 record.</span><span class="sxs-lookup"><span data-stu-id="c1be2-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="c1be2-130">Per ottenere il batch successivo di record, usare il link Avanti.</span><span class="sxs-lookup"><span data-stu-id="c1be2-130">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="c1be2-131">Ottenere le informazioni sullo [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) dal primo set di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="c1be2-131">Get the [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from the first set of returned records.</span></span> <span data-ttu-id="c1be2-132">Il token skip si trova alla fine del set di risultati.</span><span class="sxs-lookup"><span data-stu-id="c1be2-132">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="c1be2-133">Filtri supportati</span><span class="sxs-lookup"><span data-stu-id="c1be2-133">Supported filters</span></span>
<span data-ttu-id="c1be2-134">È possibile restringere il numero di record restituiti da una chiamata API usando un filtro.</span><span class="sxs-lookup"><span data-stu-id="c1be2-134">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="c1be2-135">Per i dati relativi all'API di accesso sono supportati i filtri seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1be2-135">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="c1be2-136">**$top=\<numero di record da restituire\>**: per limitare il numero di record restituiti.</span><span class="sxs-lookup"><span data-stu-id="c1be2-136">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="c1be2-137">Si tratta di un'operazione impegnativa.</span><span class="sxs-lookup"><span data-stu-id="c1be2-137">This is an expensive operation.</span></span> <span data-ttu-id="c1be2-138">Non è consigliabile usare questo filtro se si desidera restituire migliaia di oggetti.</span><span class="sxs-lookup"><span data-stu-id="c1be2-138">You should not use this filter if you want to return thousands of objects.</span></span>  
* <span data-ttu-id="c1be2-139">**$filter=\<istruzione per il filtro\>**: per specificare il tipo di record da restituire, sulla base dei campi filtro supportati</span><span class="sxs-lookup"><span data-stu-id="c1be2-139">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="c1be2-140">Operatori e campi dei filtri supportati</span><span class="sxs-lookup"><span data-stu-id="c1be2-140">Supported filter fields and operators</span></span>
<span data-ttu-id="c1be2-141">Per specificare il tipo di record da restituire, è possibile compilare un'istruzione per il filtro che può contenere uno o una combinazione dei campi filtro seguenti:</span><span class="sxs-lookup"><span data-stu-id="c1be2-141">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="c1be2-142">[signinDateTime](#signindatetime) : definisce una data o un intervallo di date</span><span class="sxs-lookup"><span data-stu-id="c1be2-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="c1be2-143">[userId](#userid) : definisce uno specifico utente in base all'ID dell'utente</span><span class="sxs-lookup"><span data-stu-id="c1be2-143">[userId](#userid) - defines a specific user based the user's ID.</span></span>
* <span data-ttu-id="c1be2-144">[userPrincipalName](#userprincipalname) : definisce uno specifico utente in base al nome dell'entità utente (UPN)</span><span class="sxs-lookup"><span data-stu-id="c1be2-144">[userPrincipalName](#userprincipalname) - defines a specific user based the user's user principal name (UPN)</span></span>
* <span data-ttu-id="c1be2-145">[appId](#appid) : definisce una specifica applicazione in base all'ID dell'app</span><span class="sxs-lookup"><span data-stu-id="c1be2-145">[appId](#appid) - defines a specific app based the app's ID</span></span>
* <span data-ttu-id="c1be2-146">[appDisplayName](#appdisplayname) : definisce una specifica app in base al nome visualizzato dell'app</span><span class="sxs-lookup"><span data-stu-id="c1be2-146">[appDisplayName](#appdisplayname) - defines a specific app based the app's display name</span></span>
* <span data-ttu-id="c1be2-147">[loginStatus](#loginStatus) : definisce lo stato dell'accesso (esito positivo/esito negativo)</span><span class="sxs-lookup"><span data-stu-id="c1be2-147">[loginStatus](#loginStatus) - defines the status of the logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="c1be2-148">Quando si usa Graph Explorer, è necessario distinguere tra lettere maiuscole e minuscole per ogni lettera nei campi del filtro.</span><span class="sxs-lookup"><span data-stu-id="c1be2-148">When using Graph Explorer, you the need to use the correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="c1be2-149">Per restringere l'ambito dei dati restituiti, è possibile creare combinazioni dei filtri supportati e dei campi dei filtri.</span><span class="sxs-lookup"><span data-stu-id="c1be2-149">To narrow down the scope of the returned data, you can build combinations of the supported filters and filter fields.</span></span> <span data-ttu-id="c1be2-150">Ad esempio, l'istruzione seguente restituisce i primi 10 record tra il 1° luglio 2016 e il 6 luglio 2016:</span><span class="sxs-lookup"><span data-stu-id="c1be2-150">For example, the following statement returns the top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="c1be2-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="c1be2-151">signinDateTime</span></span>
<span data-ttu-id="c1be2-152">**Operatori supportati**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="c1be2-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="c1be2-153">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-153">**Example**:</span></span>

<span data-ttu-id="c1be2-154">Uso di una data specifica</span><span class="sxs-lookup"><span data-stu-id="c1be2-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="c1be2-155">Uso di un intervallo di date</span><span class="sxs-lookup"><span data-stu-id="c1be2-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="c1be2-156">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-156">**Notes**:</span></span>

<span data-ttu-id="c1be2-157">Il parametro datetime deve presentarsi nel formato UTC</span><span class="sxs-lookup"><span data-stu-id="c1be2-157">The datetime parameter should be in the UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="c1be2-158">userId</span><span class="sxs-lookup"><span data-stu-id="c1be2-158">userId</span></span>
<span data-ttu-id="c1be2-159">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c1be2-159">**Supported operators**: eq</span></span>

<span data-ttu-id="c1be2-160">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="c1be2-161">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-161">**Notes**:</span></span>

<span data-ttu-id="c1be2-162">Il valore di userId è un valore stringa</span><span class="sxs-lookup"><span data-stu-id="c1be2-162">The value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="c1be2-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="c1be2-163">userPrincipalName</span></span>
<span data-ttu-id="c1be2-164">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c1be2-164">**Supported operators**: eq</span></span>

<span data-ttu-id="c1be2-165">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="c1be2-166">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-166">**Notes**:</span></span>

<span data-ttu-id="c1be2-167">Il valore di userPrincipalName è un valore stringa</span><span class="sxs-lookup"><span data-stu-id="c1be2-167">The value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="c1be2-168">appId</span><span class="sxs-lookup"><span data-stu-id="c1be2-168">appId</span></span>
<span data-ttu-id="c1be2-169">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c1be2-169">**Supported operators**: eq</span></span>

<span data-ttu-id="c1be2-170">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="c1be2-171">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-171">**Notes**:</span></span>

<span data-ttu-id="c1be2-172">Il valore di appId è un valore stringa</span><span class="sxs-lookup"><span data-stu-id="c1be2-172">The value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="c1be2-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="c1be2-173">appDisplayName</span></span>
<span data-ttu-id="c1be2-174">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c1be2-174">**Supported operators**: eq</span></span>

<span data-ttu-id="c1be2-175">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="c1be2-176">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-176">**Notes**:</span></span>

<span data-ttu-id="c1be2-177">Il valore di appDisplayName è un valore stringa</span><span class="sxs-lookup"><span data-stu-id="c1be2-177">The value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="c1be2-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="c1be2-178">loginStatus</span></span>
<span data-ttu-id="c1be2-179">**Operatori supportati**: eq</span><span class="sxs-lookup"><span data-stu-id="c1be2-179">**Supported operators**: eq</span></span>

<span data-ttu-id="c1be2-180">**Esempio**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="c1be2-181">**Note**:</span><span class="sxs-lookup"><span data-stu-id="c1be2-181">**Notes**:</span></span>

<span data-ttu-id="c1be2-182">Sono disponibili due opzioni per loginStatus: 0 - esito positivo, 1 - esito negativo</span><span class="sxs-lookup"><span data-stu-id="c1be2-182">There are two options for the loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="c1be2-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c1be2-183">Next steps</span></span>
* <span data-ttu-id="c1be2-184">Si desidera vedere esempi sulle attività di accesso filtrate?</span><span class="sxs-lookup"><span data-stu-id="c1be2-184">Do you want to see examples for filtered sign-in activities?</span></span> <span data-ttu-id="c1be2-185">Consultare la pagina [Esempi dell'API del report sull'attività di accesso di Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c1be2-185">Check out the [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="c1be2-186">Si desiderano altre informazioni sull'API di creazione report di Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c1be2-186">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="c1be2-187">Vedere [Introduzione all'API di creazione report di Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c1be2-187">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

