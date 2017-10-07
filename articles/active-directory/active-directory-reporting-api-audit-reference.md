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
# <a name="azure-active-directory-audit-api-reference"></a>Informazioni di riferimento sull'API di controllo di Azure Active Directory
Questo argomento fa parte di una raccolta di argomenti sull'hello Azure Active Directory reporting API.  
Azure Active Directory reporting fornisce un'API che consente di dati di controllo tooaccess tramite codice o gli strumenti correlati.
Hello l'ambito di questo argomento è tooprovide con informazioni di riferimento su hello **audit API**.

Vedere:

* [Log di controllo](active-directory-reporting-azure-portal.md#activity-reports) per informazioni più concettuali

* [Introduzione a hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) per ulteriori informazioni sulle API di segnalazione hello.


Per:

- Domande frequenti, leggere le [Domande Frequenti](active-directory-reporting-faq.md) 

- Problemi, [inviare un ticket di supporto](active-directory-troubleshooting-support-howto.md) 


## <a name="who-can-access-hello-data"></a>Chi può accedere a dati hello?
* Utenti nel ruolo di amministratore responsabile della sicurezza o di sicurezza Reader hello
* Gli amministratori globali
* Qualsiasi applicazione che dispone di autorizzazione tooaccess hello API (autorizzazione app può essere il programma di installazione solo in base alle autorizzazioni dell'amministratore globale)

## <a name="prerequisites"></a>Prerequisiti
In questo report tramite tooaccess di ordine hello API di Reporting, è necessario disporre di:

* Un' [edizione gratuita di Azure Active Directory o superiore](active-directory-editions.md)
* Hello completato [prerequisiti tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>L'accesso API hello
È possibile accedere a questa API tramite hello [Esplora grafico](https://graphexplorer2.cloudapp.net) o a livello di codice, ad esempio tramite PowerShell. Per PowerShell toocorrectly interpretare sintassi del filtro OData hello usata nelle chiamate REST Graph di Azure ad, è necessario utilizzare apice inverso hello (noto anche come: accento grave) carattere troppo "carattere di escape" hello $. funge da carattere apice inverso Hello [carattere di escape di PowerShell](https://technet.microsoft.com/library/hh847755.aspx), consentendo alle toodo PowerShell un'interpretazione di valore letterale di carattere $ hello ed evitare di confondere, come un nome di variabile di PowerShell (ad esempio: $filter).

hello Esplora grafico è attivo Hello di questo argomento. Per un esempio di PowerShell, vedere questo [script di PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>Endpoint API
È possibile accedere a questa API utilizzando hello seguente URI:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Non è previsto alcun limite per il numero di hello di record restituito dall'API di controllo hello Azure AD (mediante la paginazione OData).
Per i limiti di conservazione sui dati dei report, consultare [Criteri di conservazione dei report](active-directory-reporting-retention.md).

Questa chiamata non restituisce dati hello in batch. Ogni batch contiene un massimo di 1000 record.  
tooget hello successivo gruppo di record, utilizzare hello del collegamento successivo. Ottenere informazioni skiptoken hello dal primo set di hello di record restituiti. token skip Hello sarà alla fine di hello hello di set di risultati.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Filtri supportati
È possibile limitare il numero di hello di record restituiti da un'API chiamata sotto forma di un filtro.  
Per l'API di accesso sono supportati i dati correlati, hello seguenti filtri:

* **$top =\<restituito un numero di record toobe\>**  -numero di hello toolimit di record restituiti. Si tratta di un'operazione impegnativa. Utilizzare questo filtro non se si desidera tooreturn migliaia di oggetti.     
* **$filter =\<l'istruzione di filtro\>**  -toospecify, su base hello di campi di filtro supportato, il tipo di hello di record è rilevante

## <a name="supported-filter-fields-and-operators"></a>Operatori e campi dei filtri supportati
tipo di hello toospecify di record che è rilevante, è possibile compilare un'istruzione di filtro che può contenere uno o una combinazione di hello campi filtro seguente:

* [activityDate](#activitydate): definisce una data o un intervallo di date
* [categoria](#category) -definisce la categoria di hello desiderato toofilter.
* [activityStatus](#activitystatus) -definisce hello stato di un'attività
* [la proprietà activityType](#activitytype) -definisce il tipo di hello di un'attività
* [attività](#activity) -definisce attività hello come stringa  
* [Nome/attore](#actorname) -definisce attore hello in forma di nome hello actor
* [attore/objectid](#actorobjectid) -definisce attore hello in forma di ID dell'attore hello   
* [attore/upn](#actorupn) -definisce attore hello in forma di nome dell'entità utente (UPN) dell'attore hello 
* [nome didestinazione/](#targetname) -definisce la destinazione hello sotto forma di nome hello actor
* [destinazione/objectid](#targetobjectid) -definisce la destinazione hello sotto forma di ID del database di destinazione di hello  
* [destinazione/upn](#targetupn) -definisce attore hello in forma di nome dell'entità utente (UPN) dell'attore hello   

- - -
### <a name="activitydate"></a>activityDate
**Operatori supportati**: eq, ge, le, gt, lt

**Esempio**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Note**:

datetime deve essere in formato UTC

- - -
### <a name="category"></a>category

**Valori supportati**:

| Categoria                         | Valore     |
| :--                              | ---       |
| Directory principale                   | Directory |
| Gestione delle password self-service | SSPR      |
| Gestione gruppi self-service    | SSGM      |
| Provisioning degli account             | Sincronizzazione      |
| Automated Password Rollover (Rollover automatizzato delle password)      | Automated Password Rollover (Rollover automatizzato delle password) |
| Identity Protection              | IdentityProtection |
| Utenti invitati                    | Utenti invitati |
| Servizio MIM                      | Servizio MIM |



**Operatori supportati**: eq

**Esempio**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>activityStatus

**Valori supportati**:

| Stato attività | Valore |
| :--             | ---   |
| Success         | 0     |
| Esito negativo         | - 1   |

**Operatori supportati**: eq

**Esempio**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**Operatori supportati**: eq

**Esempio**:

    $filter=activityType eq 'User'    

**Note**:

fa distinzione tra maiuscole e minuscole

- - -
### <a name="activity"></a>activity
**Operatori supportati**: eq, contains, startsWith

**Esempio**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Note**:

fa distinzione tra maiuscole e minuscole

- - -
### <a name="actorname"></a>actor/name
**Operatori supportati**: eq, contains, startsWith

**Esempio**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Note**:

non fa distinzione tra maiuscole e minuscole

- - -
### <a name="actorobjectid"></a>actor/objectid
**Operatori supportati**: eq

**Esempio**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>target/name
**Operatori supportati**: eq, contains, startsWith

**Esempio**:

    $filter=targets/any(t: t/name eq 'some name')    

**Note**:

non fa distinzione tra maiuscole e minuscole

- - -
### <a name="targetupn"></a>target/upn
**Operatori supportati**: eq, startsWith

**Esempio**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Note**:

* non fa distinzione tra maiuscole e minuscole
* È necessario hello tooadd completo dello spazio dei nomi quando si eseguono query Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity

- - -
### <a name="targetobjectid"></a>target/name
**Operatori supportati**: eq

**Esempio**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>actor/upn
**Operatori supportati**: eq, startsWith

**Esempio**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Note**:

* non fa distinzione tra maiuscole e minuscole 
* È necessario hello tooadd completo dello spazio dei nomi quando si eseguono query Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity

- - -
## <a name="next-steps"></a>Passaggi successivi
* Specificare se toosee esempi per attività di sistema filtrato. Estrarre hello [esempi di API di controllo di Azure Active Directory](active-directory-reporting-api-audit-samples.md).
* Si desidera tooknow ulteriori informazioni sull'API di creazione di report hello Azure AD? Vedere [introduzione hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).

