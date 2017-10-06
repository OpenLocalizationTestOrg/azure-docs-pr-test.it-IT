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
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Riferimento API del report sull'attività di accesso di Azure Active Directory
Questo argomento fa parte di una raccolta di argomenti sull'hello Azure Active Directory reporting API.  
Report di Azure AD fornisce un'API che consente di dati del report attività di accesso tooaccess tramite codice o gli strumenti correlati.
Hello l'ambito di questo argomento è tooprovide con informazioni di riferimento su hello **Accedi attività report API**.

Vedere:

* [Attività di accesso](active-directory-reporting-azure-portal.md#activity-reports) .
* [Introduzione a hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) per ulteriori informazioni sulle API di segnalazione hello.


## <a name="who-can-access-hello-api-data"></a>Chi può accedere a dati API hello?
* Utenti ed entità servizio ruolo di amministratore responsabile della sicurezza o sicurezza lettore hello
* Gli amministratori globali
* Qualsiasi applicazione che dispone di autorizzazione tooaccess hello API (autorizzazione app può essere il programma di installazione solo in base alle autorizzazioni dell'amministratore globale)

accesso tooconfigure per un'applicazione tooaccess sicurezza API, ad esempio gli eventi di accesso, utilizzare hello seguenti applicazioni di hello tooadd PowerShell dell'entità servizio nel ruolo di sicurezza Reader hello

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Prerequisiti
Questo report tramite tooaccess hello API di creazione di report, è necessario disporre di:

* Disporre di [Azure Active Directory Premium, edizione P1 o P2](active-directory-editions.md)
* Hello completato [prerequisiti tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>L'accesso API hello
È possibile accedere a questa API tramite hello [Esplora grafico](https://graphexplorer2.cloudapp.net) o a livello di codice, ad esempio tramite PowerShell. Per PowerShell toocorrectly interpretare sintassi del filtro OData hello usata nelle chiamate REST Graph di Azure ad, è necessario utilizzare apice inverso hello (noto anche come: accento grave) carattere troppo "carattere di escape" hello $. funge da carattere apice inverso Hello [carattere di escape di PowerShell](https://technet.microsoft.com/library/hh847755.aspx), consentendo alle toodo PowerShell un'interpretazione di valore letterale di carattere $ hello ed evitare di confondere, come un nome di variabile di PowerShell (ad esempio: $filter).

hello Esplora grafico è attivo Hello di questo argomento. Per un esempio di PowerShell, vedere questo [script di PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>Endpoint API
È possibile accedere a questa API utilizzando hello seguente URI di base:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



A causa di toohello volume di dati, questa API è un limite di un milione di record restituiti. 

Questa chiamata non restituisce dati hello in batch. Ogni batch contiene un massimo di 1000 record.  
tooget hello successivo gruppo di record, utilizzare hello del collegamento successivo. Ottenere hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informazioni hello primo gruppo di record restituiti. token skip Hello sarà alla fine di hello hello di set di risultati.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Filtri supportati
È possibile limitare il numero di hello di record restituiti da un'API chiamata sotto forma di un filtro.  
Per l'API di accesso sono supportati i dati correlati, hello seguenti filtri:

* **$top =\<restituito un numero di record toobe\>**  -numero di hello toolimit di record restituiti. Si tratta di un'operazione impegnativa. Utilizzare questo filtro non se si desidera tooreturn migliaia di oggetti.  
* **$filter =\<l'istruzione di filtro\>**  -toospecify, su base hello di campi di filtro supportato, il tipo di hello di record è rilevante

## <a name="supported-filter-fields-and-operators"></a>Operatori e campi dei filtri supportati
tipo di hello toospecify di record che è rilevante, è possibile compilare un'istruzione di filtro che può contenere uno o una combinazione di hello campi filtro seguente:

* [signinDateTime](#signindatetime) : definisce una data o un intervallo di date
* [userId](#userid) -definisce l'ID. dell'utente un utente specifico in base hello
* [userPrincipalName](#userprincipalname) -definisce un utente specifico in base hello dell'utente nome entità utente (UPN)
* [appId](#appid) -definisce un'app specifica in base hello dell'ID app
* [appDisplayName](#appdisplayname) -nome visualizzato dell'applicazione hello di app specifici in base
* [loginStatus](#loginStatus) -definisce lo stato di hello degli account di accesso hello (esito positivo o negativo)

> [!NOTE]
> Quando si utilizza Esplora grafico, hello è necessario toouse hello corretto case per ogni lettera è i campi filtro.
> 
> 

toonarrow all'ambito hello di hello ha restituito dati, è possibile compilare combinazioni di filtri hello supportato e i campi di filtro. Ad esempio, hello istruzione seguente restituisce hello top 10 record tra 2016 1 ° luglio e luglio 2016 6:

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

parametro datetime Hello deve essere in formato UTC hello 

- - -
### <a name="userid"></a>userId
**Operatori supportati**: eq

**Esempio**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Note**:

il valore di Hello UserID è un valore stringa

- - -
### <a name="userprincipalname"></a>userPrincipalName
**Operatori supportati**: eq

**Esempio**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Note**:

il valore userPrincipalName Hello è un valore stringa

- - -
### <a name="appid"></a>appId
**Operatori supportati**: eq

**Esempio**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Note**:

il valore appId Hello è un valore stringa

- - -
### <a name="appdisplayname"></a>appDisplayName
**Operatori supportati**: eq

**Esempio**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Note**:

valore Hello appDisplayName è un valore stringa

- - -
### <a name="loginstatus"></a>loginStatus
**Operatori supportati**: eq

**Esempio**:

    $filter=loginStatus+eq+'1'  


**Note**:

Sono disponibili due opzioni per hello loginStatus: 0 - esito positivo, 1 - errore

- - -
## <a name="next-steps"></a>Passaggi successivi
* Si desidera toosee esempi per attività filtrate Accedi? Estrarre hello [gli esempi di API report attività di accesso di Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).
* Si desidera tooknow ulteriori informazioni sull'API di creazione di report hello Azure AD? Vedere [introduzione hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).

