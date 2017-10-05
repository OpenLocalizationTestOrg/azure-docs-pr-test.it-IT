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
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Riferimento API del report sull'attività di accesso di Azure Active Directory
Questo argomento fa parte di una raccolta di argomenti sull'API di creazione report di Azure Active Directory.  
La creazione di report di Azure Active Directory fornisce un'API che consente di accedere ai dati del report sull'attività di accesso tramite codice o strumenti correlati.
L'obiettivo di questo argomento è fornire informazioni di riferimento sull' **API del report sull'attività di accesso**.

Vedere:

* [Attività di accesso](active-directory-reporting-azure-portal.md#activity-reports) .
* [Introduzione all'API di creazione report di Azure Active Directory](active-directory-reporting-api-getting-started.md) .


## <a name="who-can-access-the-api-data"></a>Chi può accedere ai dati dell'API?
* Utenti ed entità servizio nel ruolo di amministratore della sicurezza o con autorizzazioni di lettura per la sicurezza
* Gli amministratori globali
* Qualsiasi applicazione che dispone di autorizzazione per accedere all'API. L'autorizzazione dell'app può essere configurata solo in base alle autorizzazioni dell'amministratore globale.

Per configurare l'accesso per un'applicazione che usa API di sicurezza, ad esempio eventi di accesso, usare questo comando PowerShell per aggiungere le entità servizio delle applicazioni al ruolo con autorizzazioni di lettura per la sicurezza

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Prerequisiti
Per accedere a questo report tramite l'API di creazione report, è necessario:

* Disporre di [Azure Active Directory Premium, edizione P1 o P2](active-directory-editions.md)
* Aver completato i [prerequisiti di accesso all'API di creazione report di Azure AD](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-the-api"></a>Accesso all'API
È possibile accedere a questa API tramite [Graph Explorer](https://graphexplorer2.cloudapp.net) o a livello di codice, ad esempio usando PowerShell. Al fine di consentire a Per PowerShell di interpretare correttamente la sintassi del filtro OData usata nelle chiamate REST di Graph di AAD, è necessario fare uso dell'apice inverso, ovvero l'accento grave, per eseguire l'"escape" del carattere $. L'apice inverso viene usato come [carattere di escape di PowerShell](https://technet.microsoft.com/library/hh847755.aspx)e consente a PowerShell di eseguire un'interpretazione letterale del carattere $, che evita la confusione con il nome di una variabile di PowerShell (ad esempio: $filter).

Questo argomento si concentra su Graph Explorer. Per un esempio di PowerShell, vedere questo [script di PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>Endpoint API
È possibile accedere a questa API tramite l'URI di base seguente:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



A causa del volume di dati, questa API presenta un limite di un milione di record restituiti. 

Questa chiamata restituisce i dati in batch. Ogni batch contiene un massimo di 1000 record.  
Per ottenere il batch successivo di record, usare il link Avanti. Ottenere le informazioni sullo [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) dal primo set di record restituiti. Il token skip si trova alla fine del set di risultati.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Filtri supportati
È possibile restringere il numero di record restituiti da una chiamata API usando un filtro.  
Per i dati relativi all'API di accesso sono supportati i filtri seguenti:

* **$top=\<numero di record da restituire\>**: per limitare il numero di record restituiti. Si tratta di un'operazione impegnativa. Non è consigliabile usare questo filtro se si desidera restituire migliaia di oggetti.  
* **$filter=\<istruzione per il filtro\>**: per specificare il tipo di record da restituire, sulla base dei campi filtro supportati

## <a name="supported-filter-fields-and-operators"></a>Operatori e campi dei filtri supportati
Per specificare il tipo di record da restituire, è possibile compilare un'istruzione per il filtro che può contenere uno o una combinazione dei campi filtro seguenti:

* [signinDateTime](#signindatetime) : definisce una data o un intervallo di date
* [userId](#userid) : definisce uno specifico utente in base all'ID dell'utente
* [userPrincipalName](#userprincipalname) : definisce uno specifico utente in base al nome dell'entità utente (UPN)
* [appId](#appid) : definisce una specifica applicazione in base all'ID dell'app
* [appDisplayName](#appdisplayname) : definisce una specifica app in base al nome visualizzato dell'app
* [loginStatus](#loginStatus) : definisce lo stato dell'accesso (esito positivo/esito negativo)

> [!NOTE]
> Quando si usa Graph Explorer, è necessario distinguere tra lettere maiuscole e minuscole per ogni lettera nei campi del filtro.
> 
> 

Per restringere l'ambito dei dati restituiti, è possibile creare combinazioni dei filtri supportati e dei campi dei filtri. Ad esempio, l'istruzione seguente restituisce i primi 10 record tra il 1° luglio 2016 e il 6 luglio 2016:

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**Operatori supportati**: eq, ge, le, gt, lt

**Esempio**:

Uso di una data specifica

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



Uso di un intervallo di date    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**Note**:

Il parametro datetime deve presentarsi nel formato UTC 

- - -
### <a name="userid"></a>userId
**Operatori supportati**: eq

**Esempio**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Note**:

Il valore di userId è un valore stringa

- - -
### <a name="userprincipalname"></a>userPrincipalName
**Operatori supportati**: eq

**Esempio**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Note**:

Il valore di userPrincipalName è un valore stringa

- - -
### <a name="appid"></a>appId
**Operatori supportati**: eq

**Esempio**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Note**:

Il valore di appId è un valore stringa

- - -
### <a name="appdisplayname"></a>appDisplayName
**Operatori supportati**: eq

**Esempio**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Note**:

Il valore di appDisplayName è un valore stringa

- - -
### <a name="loginstatus"></a>loginStatus
**Operatori supportati**: eq

**Esempio**:

    $filter=loginStatus+eq+'1'  


**Note**:

Sono disponibili due opzioni per loginStatus: 0 - esito positivo, 1 - esito negativo

- - -
## <a name="next-steps"></a>Passaggi successivi
* Si desidera vedere esempi sulle attività di accesso filtrate? Consultare la pagina [Esempi dell'API del report sull'attività di accesso di Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).
* Si desiderano altre informazioni sull'API di creazione report di Azure AD? Vedere [Introduzione all'API di creazione report di Azure Active Directory](active-directory-reporting-api-getting-started.md).

