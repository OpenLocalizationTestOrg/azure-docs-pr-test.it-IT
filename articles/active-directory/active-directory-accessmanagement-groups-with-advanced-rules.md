---
title: gruppi aaaPopulate dinamicamente in base agli attributi di oggetto in Azure Active Directory | Documenti Microsoft
description: "Modalità-per toocreate avanzate di regole per gruppo, tra cui l'appartenenza supportati operatori di regole di espressione e i parametri."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 04813a42-d40a-48d6-ae96-15b7e5025884
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: fe22829118ed8f5137a619d93fa6f9bf80835863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="populate-groups-dynamically-based-on-object-attributes"></a>Compilare i gruppi in modo dinamico in base agli attributi degli oggetti
portale di Azure classico Hello fornisce hello possibilità tooenable più complesso basato su attributi appartenenza dinamica ai gruppi di Azure Active Directory (Azure AD).  

Quando gli attributi di una modifica utente o dispositivo, sistema hello valuta tutte le regole gruppo dinamico in una directory di toosee se Attiva modifica hello qualsiasi gruppo aggiunge o rimuove. Se un utente o un dispositivo soddisfa una regola in un gruppo, viene aggiunto come membro a tale gruppo. Se non soddisfano la regola hello, questi vengono rimossi.

> [!NOTE]
> - È possibile configurare una regola per l'appartenenza dinamica nei gruppi di sicurezza o nei gruppi di Office 365.
>
> - Questa funzionalità richiede una licenza Azure AD Premium P1 per ogni gruppo di utenti membro tooat aggiunto almeno una dinamica.
>
> - Sebbene sia possibile creare un gruppo dinamico per i dispositivi o gli utenti, non è possibile creare una regola che contenga sia oggetti utente che dispositivo.

> - Al momento di hello non è possibile toocreate un gruppo di dispositivi in base agli attributi dell'utente proprietario. Le regole di appartenenza dispositivo possono solo immediato attributi di riferimento degli oggetti dispositivo hello directory.

## <a name="toocreate-an-advanced-rule"></a>toocreate una regola avanzata
1. In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi aprire la directory dell'organizzazione.
2. Seleziona hello **gruppi** scheda e quindi aprire hello gruppo tooedit.
3. Seleziona hello **configura** scheda, seleziona hello **regola avanzata** opzione e quindi immettere hello regola avanzata nella casella di testo hello.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Corpo hello costruzione di una regola avanzata
Hello la regola avanzata che è possibile creare per hello appartenenza dinamica ai gruppi è essenzialmente un'espressione binaria costituita da tre parti e dai risultati in un risultato true o false. Hello tre parti sono:

* Parametro sinistro
* Operatore binario
* Costante destra

Una regola avanzata completa sarà simile toothis: (leftParameter binaryOperator "RightConstant"), dove hello apertura e la parentesi di chiusura è necessaria per l'intera espressione binaria di hello, le virgolette doppie sono necessari per la costante di destra hello e sintassi hello per hello parametro di sinistra è User. Può essere costituiti da una regola avanzata di più espressioni binarie separate dagli hello- e- o e - operatori logici non.
Hello di seguito è riportati esempi di una regola avanzata creata correttamente:

* (user.department -eq "Vendite") -or (user.department -eq "Marketing")
* (user.department -eq "Vendite") -and -not (user.jobTitle -contains "SDE")

Per l'elenco completo di hello dei parametri supportati e operatori di regole di espressione, vedere le sezioni seguenti.


Si noti che la proprietà hello deve essere preceduta da tipo di oggetto corretto hello: utente o dispositivo.
Hello seguito regola supererà la convalida di hello: posta elettronica: ne null

regola di Hello corretto sarebbe:

user.mail –ne null

lunghezza totale di Hello del corpo hello della regola avanzata non può superare i 2048 caratteri.

> [!NOTE]
> Le operazioni di stringa ed espressione regolare non fanno distinzione tra maiuscole e minuscole.
> Le stringhe contenenti virgolette (") devono essere precedute dal carattere di escape ', ad esempio user.department -eq \`"Sales".
> Usare le virgolette solo per i valori di tipo stringa e usare solo le virgolette singole.
>
>

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

Di seguito sono elencati tutti gli operatori per la priorità da toohigher inferiore, l'operatore nella stessa riga sono uguale hanno la precedenza-qualsiasi - all - o - e - non - eq, ne - startsWith - notStartsWith-contiene - notContains-corrispondono notMatch –-in - notIn

Tutti gli operatori possono essere usati con o senza trattino come prefisso.

Si noti che non sono sempre necessari parentesi, parentesi tooadd è necessario solo quando la priorità non soddisfa i requisiti, ad esempio:

   user.department –eq "Marketing" –and user.country –eq "US"

Equivale a:

   (user.department –eq "Marketing") –and (user.country –eq "US")

## <a name="using-hello--in-and--notin-operators"></a>Utilizzando hello - In e gli operatori - notIn

Se si desidera toocompare hello valore di un attributo utente con un numero di valori diversi è possibile utilizzare hello - In o - notIn operatori. Di seguito è riportato un esempio utilizzando hello - nell'operatore:

    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]

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

   user.mail –ne null equivale a user.mail –ne $null

## <a name="extension-attributes-and-custom-attributes"></a>Attributi di estensione ed attributi personalizzati
Gli attributi di estensione e gli attributi personalizzati sono supportati nelle regole di appartenenza dinamica.

Attributi di estensione vengono sincronizzati da locale Windows Server Active Directory e richiedere formato hello "ExtensionAttributeX", dove X è uguale a 1-15.
Ecco un esempio di regola che usa un attributo di estensione:

(user.extensionAttribute15 -eq "Marketing")

Attributi personalizzati vengono sincronizzati da locale Windows Server Active Directory o da un connesso SaaS applicazione hello hello formato e di "user.extension_[GUID]\__ [Attribute]", dove [GUID] è l'identificatore univoco hello in AAD per un'applicazione hello che attributo creato hello in AAD e [Attribute] è il nome di hello dell'attributo hello è stato creato.
Ecco un esempio di regola che usa un attributo personalizzato:

user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  

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
È anche possibile creare una regola che consenta di selezionare gli oggetti dispositivo per l'appartenenza a un gruppo. è possibile utilizzare Hello gli attributi di dispositivo seguenti:

| Proprietà              | Valori consentiti                  | Utilizzo                                                       |
|-------------------------|---------------------------------|-------------------------------------------------------------|
| accountEnabled          | true false                      | (device.accountEnabled -eq true)                            |
| displayName             | Qualsiasi valore stringa.                | (device.displayName - eq "Iphone di Rob")                       |
| deviceOSType            | Qualsiasi valore stringa.                | (device.deviceOSType -eq "IOS")                             |
| deviceOSVersion         | Qualsiasi valore stringa.                | (device.OSVersion -eq "9.1")                                |
| deviceCategory          | Qualsiasi valore stringa.                | (device.deviceCategory -eq "")                              |
| deviceManufacturer      | Qualsiasi valore stringa.                | (device.deviceManufacturer -eq "Microsoft")                 |
| deviceModel             | Qualsiasi valore stringa.                | (device.deviceModel -eq "IPhone 7+")                        |
| deviceOwnership         | Qualsiasi valore stringa.                | (device.deviceOwnership -eq "")                             |
| domainName              | Qualsiasi valore stringa.                | (device.domainName -eq "contoso.com")                       |
| enrollmentProfileName   | Qualsiasi valore stringa.                | (device.enrollmentProfileName -eq "")                       |
| isRooted                | true false                      | (device.deviceOSType -eq true)                              |
| managementType          | Qualsiasi valore stringa.                | (device.managementType -eq "")                              |
| organizationalUnit      | Qualsiasi valore stringa.                | (device.organizationalUnit -eq "")                          |
| deviceId                | un deviceId valido                | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d") |
| objectId                | un objectId AAD valido            | (device.objectId -eq "76ad43c9-32c5-45e8-a272-7b58b58f596d") |

> [!NOTE]
> Queste regole di dispositivo non è possibile creare utilizzando l'elenco a discesa "regola semplice" hello in hello portale di Azure classico.
>
>

## <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Risoluzione dei problemi di appartenenza dinamica per i gruppi](active-directory-accessmanagement-troubleshooting.md)
* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
