---
title: basato su aaaAttribute appartenenza dinamica ai gruppi in Azure Active Directory | Documenti Microsoft
description: Toocreate avanzate come le regole di appartenenza dinamica ai gruppi inclusi i parametri e operatori di regole di espressione supportati.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fb434cc2-9a91-4ebf-9753-dd81e289787e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cd06ed70433eff65401c67d7351d5dcc12a9dd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a>Creare regole basate su attributi per l'appartenenza dinamica ai gruppi in Azure Active Directory
In Azure Active Directory (Azure AD), è possibile creare regole avanzate tooenable complesso basato su attributi appartenenza dinamica ai gruppi. In questo articolo illustra in dettaglio gli attributi di hello e regole di appartenenza dinamica toocreate sintassi per gli utenti o dispositivi.

Quando gli attributi di una modifica utente o dispositivo, sistema hello valuta tutte le regole gruppo dinamico in una directory di toosee se Attiva modifica hello qualsiasi gruppo aggiunge o rimuove. Se un utente o un dispositivo soddisfa una regola in un gruppo, viene aggiunto come membro a tale gruppo. Se non soddisfano la regola hello, questi vengono rimossi.

> [!NOTE]
> - È possibile configurare una regola per l'appartenenza dinamica nei gruppi di sicurezza o nei gruppi di Office 365.
>
> - Questa funzionalità richiede una licenza Azure AD Premium P1 per ogni gruppo di utenti membro tooat aggiunto almeno una dinamica.
>
> - Sebbene sia possibile creare un gruppo dinamico per i dispositivi o gli utenti, non è possibile creare una regola che contenga sia oggetti utente che dispositivo.

> - Al momento di hello non è possibile toocreate un gruppo di dispositivi in base agli attributi dell'utente proprietario. Le regole di appartenenza dispositivo possono solo immediato attributi di riferimento degli oggetti dispositivo hello directory.

## <a name="toocreate-an-advanced-rule"></a>toocreate una regola avanzata
1. Accedi toohello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) con un account che sia un amministratore globale o un amministratore dell'account utente.
2. Selezionare **Utenti e gruppi**.
3. Selezionare **Tutti i gruppi**.

   ![Pannello gruppi hello di apertura](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. In **Tutti i gruppi**, selezionare **Nuovo gruppo**.

   ![Aggiungere un nuovo gruppo](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. In hello **gruppo** pannello, immettere un nome e una descrizione per il nuovo gruppo di hello. Selezionare un **tipo di appartenenza** tra **dinamica dell'utente** o **dispositivi dinamici**, a seconda se si desidera toocreate una regola per gli utenti o dispositivi e quindi selezionare **Aggiungi dinamica delle query**. Per gli attributi di hello usati per le regole di dispositivo, vedere [utilizzando le regole toocreate di attributi per gli oggetti dispositivo](#using-attributes-to-create-rules-for-device-objects).

   ![Aggiungere una regola di appartenenza dinamica](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. In hello **le regole di appartenenza dinamica** pannello, immettere la regola in hello **dell'appartenenza dinamica Aggiungi regola avanzata** , premere INVIO e quindi selezionare **crea** in fondo hello Pannello Hello.
7. Selezionare **crea** su hello **gruppo** gruppo hello toocreate di blade.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Corpo hello costruzione di una regola avanzata
Hello la regola avanzata che è possibile creare per hello appartenenza dinamica ai gruppi è essenzialmente un'espressione binaria costituita da tre parti e dai risultati in un risultato true o false. Hello tre parti sono:

* Parametro sinistro
* Operatore binario
* Costante destra

Una regola avanzata completa sarà simile toothis: (leftParameter binaryOperator "RightConstant"), dove hello di apertura e chiusura parentesi è facoltativa per l'intera espressione binaria di hello, le virgolette doppie sono facoltative, nonché richiesto solo per hello destra costante in questo caso, stringa e la sintassi di hello per il parametro di sinistra hello è User. Può essere costituiti da una regola avanzata di più espressioni binarie separate dagli hello- e- o e - operatori logici non.

Hello di seguito è riportati esempi di una regola avanzata creata correttamente:
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
Per l'elenco completo di hello dei parametri supportati e operatori di regole di espressione, vedere le sezioni seguenti. Per gli attributi di hello usati per le regole di dispositivo, vedere [utilizzando le regole toocreate di attributi per gli oggetti dispositivo](#using-attributes-to-create-rules-for-device-objects).

lunghezza totale di Hello del corpo hello della regola avanzata non può superare i 2048 caratteri.

> [!NOTE]
> Le operazioni di stringa ed espressione regolare non fanno distinzione tra maiuscole e minuscole. È inoltre possibile eseguire controlli Null usando $null come costante, ad esempio user.department -eq $null.
> Le stringhe contenenti virgolette (") devono essere precedute dal carattere di escape ', ad esempio user.department -eq \`"Sales".

## <a name="supported-expression-rule-operators"></a>Operatori delle regole di espressione supportati
Hello nella tabella seguente sono elencati tutti gli operatori di regole di espressione hello è supportato e toobe loro sintassi utilizzato nel corpo di hello di hello regola avanzata:

| operatore | Sintassi |
| --- | --- |
| Non uguale a |-ne |
| Uguale a |-eq |
| Non inizia con |-notStartsWith |
| Inizia con |-startsWith |
| Non contiene |-notContains |
| Contiene |-contains |
| Non corrispondente |-notMatch |
| Corrispondente |-match |
| In | -in |
| Non incluso | -notIn |

## <a name="operator-precedence"></a>Precedenza degli operatori

Tutti gli operatori sono elencati di seguito per la priorità da toohigher inferiore. Gli operatori nella stessa riga hanno uguale precedenza:
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
Tutti gli operatori possono essere utilizzati con o senza prefisso trattino hello. Le parentesi sono necessarie solo quando la priorità non soddisfa i requisiti.
ad esempio:
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
Equivale a:
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-hello--in-and--notin-operators"></a>Utilizzando hello - In e gli operatori - notIn

Se si desidera toocompare hello valore di un attributo utente con un numero di valori diversi è possibile utilizzare hello - In o - notIn operatori. Di seguito è riportato un esempio utilizzando hello - nell'operatore:
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
Si noti utilizzo hello di hello "[" e "]" all'inizio di hello e alla fine dell'elenco di hello di valori. Questa condizione viene valutata tooTrue del valore di hello di Department è uguale a uno dei valori hello hello elenco.


## <a name="query-error-remediation"></a>Correzione degli errori di query
Hello nella tabella seguente sono elencati gli errori potenziali e come toocorrect, se si verificano

| Errore di analisi della query | Uso errato | Uso corretto |
| --- | --- | --- |
| Errore: l'attributo non è supportato |(user.invalidProperty -eq "Valore") |(user.department -eq "valore")<br/>Proprietà deve corrispondere a una delle hello [supportata l'elenco delle proprietà](#supported-properties). |
| Errore: l'operatore non è supportato sull'attributo. |(user.accountEnabled -contains true) |(user.accountEnabled -eq true)<br/>La proprietà è di tipo booleano. Utilizzare gli operatori supportato hello (-eq o - ne) di tipo booleano hello sopra l'elenco. |
| Errore: si è verificato un errore di compilazione della query. |(user.department -eq "Vendite") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext" |(user.department -eq "Sales") -and (user.department -eq "Marketing")<br/>Operatore logico deve corrispondere a una delle proprietà hello è supportato nell'elenco precedente. (User-corrispondenza ". *@domain.ext") o (User-corrispondono "@domain.ext$") errore nell'espressione regolare. |
| Errore: l'espressione binaria non ha il formato corretto |(user.department –eq "Vendite") (user.department -eq "Vendite")(user.department-eq"Vendite") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>La query include più errori. La parentesi non si trova nella posizione corretta. |
| Errore: si è verificato un errore sconosciuto durante la configurazione delle appartenenze dinamiche. |(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain" |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>La query include più errori. La parentesi non si trova nella posizione corretta. |

## <a name="supported-properties"></a>Proprietà supportate
di seguito Hello sono tutte le proprietà utente hello che è possibile utilizzare la regola avanzata:

### <a name="properties-of-type-boolean"></a>Proprietà di tipo boolean
Operatori consentiti

* -eq
* -ne

| Proprietà | Valori consentiti | Utilizzo |
| --- | --- | --- |
| accountEnabled |true false |user.accountEnabled -eq true |
| dirSyncEnabled |true false |user.dirSyncEnabled -eq true |

### <a name="properties-of-type-string"></a>Proprietà di tipo stringa
Operatori consentiti

* -eq
* -ne
* -notStartsWith
* -startsWith
* -contains
* -notContains
* -match
* -notMatch
* -in
* -notIn

| Proprietà | Valori consentiti | Utilizzo |
| --- | --- | --- |
| city |Qualsiasi valore stringa o $null |(user.city -eq "valore") |
| country |Qualsiasi valore stringa o $null |(user.country -eq "valore") |
| companyName | Qualsiasi valore stringa o $null | (user.companyName -eq "value") |
| department |Qualsiasi valore stringa o $null |(user.department -eq "valore") |
| displayName |Qualsiasi valore stringa. |(user.displayName -eq "valore") |
| facsimileTelephoneNumber |Qualsiasi valore stringa o $null |(user.facsimileTelephoneNumber -eq "valore") |
| givenName |Qualsiasi valore stringa o $null |(user.givenName -eq "valore") |
| jobTitle |Qualsiasi valore stringa o $null |(user.jobTitle -eq "valore") |
| mail |Qualsiasi valore stringa o $null (indirizzo SMTP dell'utente hello) |(user.mail -eq "valore") |
| mailNickName |Qualsiasi valore stringa (alias di posta elettronica dell'utente hello) |(user.mailNickName -eq "valore") |
| mobile |Qualsiasi valore stringa o $null |(user.mobile -eq "valore") |
| objectId |GUID dell'oggetto utente hello |(user.objectId -eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | ID di sicurezza locale (SID) per gli utenti che sono state sincronizzate dal cloud toohello in locale. |(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |Nessuno DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies -eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |Qualsiasi valore stringa o $null |(user.physicalDeliveryOfficeName -eq "valore") |
| postalCode |Qualsiasi valore stringa o $null |(user.postalCode -eq "valore") |
| preferredLanguage |Codice ISO 639-1 |(user.preferredLanguage -eq "en-US") |
| sipProxyAddress |Qualsiasi valore stringa o $null |(user.sipProxyAddress -eq "valore") |
| state |Qualsiasi valore stringa o $null |(user.state -eq "valore") |
| streetAddress |Qualsiasi valore stringa o $null |(user.streetAddress -eq "valore") |
| surname |Qualsiasi valore stringa o $null |(user.surname -eq "valore") |
| telephoneNumber |Qualsiasi valore stringa o $null |(user.telephoneNumber -eq "valore") |
| usageLocation |Codice di paese di due lettere |(user.usageLocation -eq "US") |
| userPrincipalName |Qualsiasi valore stringa. |(user.userPrincipalName -eq "alias@domain") |
| userType |membro guest $null |(user.userType -eq "Membro") |

### <a name="properties-of-type-string-collection"></a>Proprietà di tipo insieme String
Operatori consentiti

* -contains
* -notContains

| Proprietà | Valori consentiti | Utilizzo |
| --- | --- | --- |
| otherMails |Qualsiasi valore stringa. |(user.otherMails -contains "alias@domain") |
| proxyAddresses |SMTP: alias@domain smtp: alias@domain |(user.proxyAddresses -contains "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>Proprietà multivalore
Operatori consentiti

* -qualsiasi (soddisfatti quando almeno un elemento nella raccolta hello soddisfa la condizione di hello)
* -tutti (soddisfatti quando tutti gli elementi nella raccolta hello corrispondono alla condizione hello)

| Proprietà | Valori | Uso |
| --- | --- | --- |
| assignedPlans |Ogni oggetto nella raccolta hello espone hello seguenti proprietà di stringa: capabilityStatus, servizio, servicePlanId |user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled") |

Proprietà multivalore sono raccolte di oggetti di hello stesso tipo. È possibile utilizzare - a qualsiasi - tooapply operatori tooone una condizione o tutti hello di elementi nella raccolta di hello, rispettivamente. ad esempio:

assignedPlans è una proprietà multivalore che elenca tutti i piani di servizio assegnati a utente toohello. Hello seguente espressione verrà selezionare utenti con piano di servizio Exchange Online (piano di 2) hello che è anche in stato abilitato:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(identificatore Guid hello identifica il piano di servizio Exchange Online (piano di 2) hello).

> [!NOTE]
> Ciò è utile se si desidera tooidentify tutti gli utenti per i quali Office 365 (o altri servizi Online Microsoft) funzionalità è stata abilitata, per esempio tootarget con un determinato set di criteri.

Hello espressione seguente selezionerà tutti gli utenti che dispongono di qualsiasi piano di servizio associato hello servizio di Intune (identificato dal nome del servizio "SCO"):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Uso dei valori Null

toospecify, un valore null in una regola, è possibile utilizzare "null" o $null. Esempio:
```
   user.mail –ne null
```
equivale a
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a>Attributi di estensione ed attributi personalizzati
Gli attributi di estensione e gli attributi personalizzati sono supportati nelle regole di appartenenza dinamica.

Attributi di estensione vengono sincronizzati da locale Windows Server Active Directory e richiedere formato hello "ExtensionAttributeX", dove X è uguale a 1-15.
Ecco un esempio di regola che usa un attributo di estensione:
```
(user.extensionAttribute15 -eq "Marketing")
```
Attributi personalizzati vengono sincronizzati da locale Windows Server Active Directory o da un connesso SaaS applicazione hello hello formato e di "user.extension_[GUID]\__ [Attribute]", dove [GUID] è l'identificatore univoco hello in AAD per un'applicazione hello che attributo creato hello in AAD e [Attribute] è il nome di hello dell'attributo hello è stato creato.
Ecco un esempio di regola che usa un attributo personalizzato:
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
Hello nome attributo personalizzato è reperibile nella directory hello eseguendo una query su un utente dell'attributo utilizzando Esplora grafico e la ricerca per nome di attributo hello.

## <a name="direct-reports-rule"></a>Regola per i dipendenti diretti
È possibile creare un gruppo contenente tutti i dipendenti diretti di un manager. Quando hello dipendenti diretti cambiare in futuro hello, appartenenza al gruppo hello verrà regolata automaticamente.

> [!NOTE]
> 1. Per toowork regola hello, assicurarsi che hello **ID responsabile** sia impostata correttamente per gli utenti nel tenant. È possibile controllare il valore corrente di hello per un utente loro **scheda profilo**.
> 2. Questa regola supporta solo i dipendenti **diretti**. Non è attualmente possibile toocreate un gruppo per una gerarchia annidata, ad esempio, un gruppo che include i dipendenti diretti e i relativi report.

**gruppo hello tooconfigure**

1. Eseguire i passaggi da 1 a 5 dalla sezione [regola avanzata hello toocreate](#to-create-the-advanced-rule)e selezionare un **tipo di appartenenza** di **dinamica dell'utente**.
2. In hello **le regole di appartenenza dinamica** pannello, immettere la regola hello con hello la seguente sintassi:

    *Dipendenti diretti per "{obectID_of_manager}"*

    Esempio di una regola valida:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. Dopo aver salvato la regola hello, tutti gli utenti con hello specificato verrà aggiunto il valore di ID responsabile toohello gruppo.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>Utilizzando le regole toocreate di attributi per gli oggetti dispositivo
È anche possibile creare una regola che consenta di selezionare gli oggetti dispositivo per l'appartenenza a un gruppo. gli attributi di dispositivo seguenti Hello può essere utilizzato.

 Attributo del dispositivo  | Valori | Esempio
 ----- | ----- | ----------------
 accountEnabled | true false | (device.accountEnabled -eq true)
 displayName | Qualsiasi valore stringa. |(device.displayName - eq "Iphone di Rob")
 deviceOSType | Qualsiasi valore stringa. | (device.deviceOSType -eq "IOS")
 deviceOSVersion | Qualsiasi valore stringa. | (device.OSVersion -eq "9.1")
 deviceCategory | nome di una categoria di dispositivo valido | (device.deviceCategory -eq "BYOD")
 deviceManufacturer | Qualsiasi valore stringa. | (device.deviceManufacturer -eq "Samsung")
 deviceModel | Qualsiasi valore stringa. | (device.deviceModel -eq "iPad Air")
 deviceOwnership | Personale, Azienda | (device.deviceOwnership -eq "Company")
 domainName | Qualsiasi valore stringa. | (device.domainName -eq "contoso.com")
 enrollmentProfileName | Nome del profilo di registrazione dispositivi Apple | (device.enrollmentProfileName -eq "DEP iPhones")
 isRooted | true false | (device.isRooted -eq true)
 managementType | MDM (per i dispositivi mobili)<br>PC (per i computer gestiti dall'agente di hello PC di Intune) | (device.managementType -eq "MDM")
 organizationalUnit | qualsiasi valore di stringa corrisponde al nome della hello dell'unità organizzativa hello impostato da un server di Active Directory locale | (device.organizationalUnit -eq "US PCs")
 deviceId | ID dispositivo di Azure AD valido | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")
 objectId | ID oggetto di Azure AD valido |  (device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")




## <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive sui gruppi in Azure Active Directory.

* [Vedere i gruppi esistenti](active-directory-groups-view-azure-portal.md)
* [Creare un nuovo gruppo e aggiunta di membri](active-directory-groups-create-azure-portal.md)
* [Gestire le impostazioni di un gruppo](active-directory-groups-settings-azure-portal.md)
* [Gestire le appartenenze di un gruppo](active-directory-groups-membership-azure-portal.md)
* [Gestire le regole dinamiche per gli utenti in un gruppo](active-directory-groups-dynamic-membership-azure-portal.md)
