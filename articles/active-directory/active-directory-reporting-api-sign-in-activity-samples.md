---
title: "esempi di report API attività aaaAzure sign-in Active Directory | Documenti Microsoft"
description: "La modalità di avvio tooget con hello API Azure Active Directory Reporting"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Esempi dell'API del report sull'attività di accesso di Azure Active Directory
Questo argomento fa parte di una raccolta di argomenti sull'hello Azure Active Directory reporting API.  
Azure Active Directory reporting fornisce un'API che consente di dati di attività di accesso tooaccess tramite codice o gli strumenti correlati.  
ambito di questo argomento Hello è tooprovide all'esempio di codice per hello **Accedi attività API**.

Vedere:

* [Log di controllo](active-directory-reporting-azure-portal.md#activity-reports) per informazioni più concettuali
* [Introduzione a hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) per ulteriori informazioni sulle API di segnalazione hello.


## <a name="prerequisites"></a>Prerequisiti
Prima di poter utilizzare gli esempi di hello in questo argomento, è necessario hello toocomplete [prerequisiti tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).  

## <a name="powershell-script"></a>Script di PowerShell
    # This script will require hello Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a>L'esecuzione dello script hello
Una volta terminare la modifica di script hello, eseguirlo e verificare che hello previsto vengono restituiti i dati da hello report di log di controllo.

script Hello restituisce l'output di hello Accedi report in formato JSON. Crea inoltre un `SigninActivities.json` file con hello stesso output. È possibile provare la modifica dei dati di tooreturn hello script da altri report e i formati di output di hello non è necessario impostare come commento.

## <a name="next-steps"></a>Passaggi successivi
* Si desidera che gli esempi di hello toocustomize in questo argomento. Estrarre hello [Azure Active Directory attività di accesso di riferimento all'API](active-directory-reporting-api-sign-in-activity-reference.md). 
* Se si desidera una panoramica completa dell'uso toosee hello reporting API Azure Active Directory, vedere [introduzione hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).
* Se si desidera toofind ulteriori informazioni sui report di Azure Active Directory, vedere hello [Azure Active Directory Reporting Guida](active-directory-reporting-guide.md).  

