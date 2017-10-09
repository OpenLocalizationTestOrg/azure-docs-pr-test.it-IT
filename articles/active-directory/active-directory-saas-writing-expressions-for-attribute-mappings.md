---
title: le espressioni per i mapping degli attributi in Azure Active Directory aaaWriting | Documenti Microsoft
description: Informazioni su come toouse espressione mapping tootransform i valori di attributo in un formato accettabile durante il provisioning automatico degli oggetti di app SaaS in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Scrittura di espressioni per il mapping degli attributi in Azure Active Directory
Quando si configura l'applicazione SaaS di provisioning tooa, uno dei tipi di hello di mapping degli attributi che è possibile specificare è il mapping di un'espressione. Per questo motivo, è necessario scrivere un'espressione analoga a uno script che consente di tootransform i dati utente in formati più idonei per un'applicazione SaaS hello.

## <a name="syntax-overview"></a>Panoramica della sintassi
sintassi di Hello per le espressioni per i mapping degli attributi è simile a quella di Visual Basic per le funzioni Applications (VBA).

* espressione intera Hello deve essere definito in termini di funzioni, costituiti da un nome seguito dagli argomenti tra parentesi: <br>
  *NomeFunzione(&lt;&lt;argomento 1&gt;&gt;,&lt;<argument N>&gt;)*
* È possibile annidare le funzioni in altre funzioni. Ad esempio: <br> *FunzioneUno(FunzioneDue(&lt;<argument1>&gt;))*
* È possibile passare tre tipi diversi di argomenti nelle funzioni:
  
  1. Attributi, che devono essere racchiusi tra parentesi quadre. Ad esempio: [NomeAttributo]
  2. Costanti di stringa, che devono essere racchiuse tra virgolette doppie. Ad esempio: "Stati Uniti"
  3. Altre funzioni. Ad esempio: FunzioneUno(<<argument1>>, FunzioneDue(<<argument2>>))
* Per le costanti di stringa, se occorre una barra rovesciata (\) o virgolette (") nella stringa hello, è necessario sottoporli a escape con il simbolo di barra rovesciata (\) hello. Ad esempio: "Nome società: \"Contoso\""

## <a name="list-of-functions"></a>Elenco di funzioni
[Append](#append)&nbsp;&nbsp;&nbsp;&nbsp;[FormatDateTime](#formatdatetime)&nbsp;&nbsp;&nbsp;&nbsp;[Join](#join)&nbsp;&nbsp;&nbsp;&nbsp;[Mid](#mid)&nbsp;&nbsp;&nbsp;&nbsp;[Not](#not)&nbsp;&nbsp;&nbsp;&nbsp;[Replace](#replace)&nbsp;&nbsp;&nbsp;&nbsp;[StripSpaces](#stripspaces)&nbsp;&nbsp;&nbsp;&nbsp;[Switch](#switch)

- - -
### <a name="append"></a>Append
**Funzione:**<br> Append(source, suffix)

**Descrizione:**<br> Accetta un valore di stringa di origine e aggiunge hello suffisso toohello fine.

**Parametri:**<br> 

| Nome | Obbligatorio/Ripetuto | Tipo | Note |
| --- | --- | --- | --- |
| **source** |Obbligatorio |String |In genere nome dell'attributo dell'oggetto di origine hello hello |
| **suffix** |Obbligatorio |String |stringa Hello che si desidera tooappend toohello fine del valore di origine hello. |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Funzione:**<br> FormatDateTime(source, inputFormat, outputFormat)

**Descrizione:**<br> Accetta una stringa data in un formato e la converte in un formato diverso.

**Parametri:**<br> 

| Nome | Obbligatorio/Ripetuto | Tipo | Note |
| --- | --- | --- | --- |
| **source** |Obbligatorio |String |In genere nome dell'attributo hello hello oggetto di origine. |
| **inputFormat** |Obbligatorio |String |Formato previsto del valore di origine hello. Per informazioni sui formati supportati, vedere [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx). |
| **outputFormat** |Obbligatorio |String |Formato della data di output di hello. |

- - -
### <a name="join"></a>Join
**Funzione:**<br> Join(separator, source1, source2, …)

**Descrizione:**<br> Join () è tooAppend() simili, ad eccezione del fatto che è possibile combinare più **origine** i valori di stringa in un'unica stringa e ogni valore sarà separato da un **separatore** stringa.

Se uno dei valori di origine hello è un attributo multivalore, ogni valore in tale attributo è il valore di separatore hello aggiunti a un insieme, separati.

**Parametri:**<br> 

| Nome | Obbligatorio/Ripetuto | Tipo | Note |
| --- | --- | --- | --- |
| **separator** |Obbligatorio |String |Stringa utilizzata tooseparate i valori di origine quando sono concatenati in un'unica stringa. Può essere "" se non sono necessari separatori. |
| **source1 … sourceN** |Obbligatorio per un numero variabile di volte |String |Unite toobe valori stringa. |

- - -
### <a name="mid"></a>Mid
**Funzione:**<br> Mid(source, start, length)

**Descrizione:**<br> Restituisce una sottostringa del valore di origine hello. Una sottostringa è una stringa che contiene solo alcuni caratteri hello dalla stringa di origine hello.

**Parametri:**<br> 

| Nome | Obbligatorio/Ripetuto | Tipo | Note |
| --- | --- | --- | --- |
| **source** |Obbligatorio |String |In genere nome dell'attributo hello. |
| **start** |Obbligatorio |numero intero |Indice in hello **origine** stringa in cui inizio della sottostringa. Primo carattere nella stringa hello avranno indice 1, secondo carattere indice 2 e così via. |
| **length** |Obbligatorio |numero intero |Lunghezza della sottostringa hello. Se lunghezza termina hello esterno **origine** stringa, funzione restituirà una sottostringa da **avviare** indice fino alla fine della **origine** stringa. |

- - -
### <a name="not"></a>not
**Funzione:**<br> Not(source)

**Descrizione:**<br> Capovolge hello valore booleano di hello **origine**. Se il valore di **source** è "*True*", restituisce "*False*". In caso contrario, restituisce "*True*".

**Parametri:**<br> 

| Nome | Obbligatorio/Ripetuto | Tipo | Note |
| --- | --- | --- | --- |
| **source** |Obbligatorio |Stringa booleana |I valori previsti per **source** sono "True" o "False". |

- - -
### <a name="replace"></a>Replace
**Funzione:**<br> ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)

**Descrizione:**<br>
Sostituisce i valori all'interno di una stringa. Funziona in modo diverso a seconda dei parametri di hello fornito:

* Se vengono forniti **oldValue** e **replacementValue**:
  
  * Sostituisce tutte le occorrenze di oldValue nell'origine hello con replacementValue
* Se vengono forniti **oldValue** e **template**:
  
  * Sostituisce tutte le occorrenze di hello **oldValue** in hello **modello** con hello **origine** valore
* Se vengono forniti **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue**:
  
  * Sostituisce tutti i valori corrispondenti nella stringa di origine hello con replacementValue oldValueRegexPattern
* Se vengono forniti **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName**:
  
  * Se è presente un valore per **source**, verrà restituito **source**
  * Se **origine** non ha alcun valore, utilizza **oldValueRegexPattern** e **oldValueRegexGroupName** tooextract valore di sostituzione dalla proprietà hello con  **replacementPropertyName**. Valore di sostituzione viene restituito come risultato di hello

**Parametri:**<br> 

| Nome | Obbligatorio/Ripetuto | Tipo | Note |
| --- | --- | --- | --- |
| **source** |Obbligatorio |String |In genere nome dell'attributo hello hello oggetto di origine. |
| **oldValue** |Facoltativo |String |Valore toobe sostituiti in **origine** o **modello**. |
| **regexPattern** |Facoltativo |String |Modello Regex per hello valore toobe sostituiti in **origine**. Oppure, se si usa replacementPropertyName, tooextract valore dalla proprietà di sostituzione di schema. |
| **regexGroupName** |Facoltativo |String |Nome del gruppo di hello all'interno di **regexPattern**. Solo se si usa replacementPropertyName, il valore di questo gruppo verrà estratto come replacementValue dalla proprietà di sostituzione. |
| **replacementValue** |Facoltativo |String |Nuovo valore tooreplace precedente con. |
| **replacementAttributeName** |Facoltativo |String |Nome di hello attributo toobe usato per il valore di sostituzione, quando l'origine non ha alcun valore. |
| **template** |Facoltativo |String |Quando **modello** valore è specificato, verrà cercato **oldValue** hello modello all'interno e sostituirlo con il valore di origine. |

- - -
### <a name="stripspaces"></a>StripSpaces
**Funzione:**<br> StripSpaces(source)

**Descrizione:**<br> Rimuove tutti gli spazi ("") stringa di caratteri da hello origine.

**Parametri:**<br> 

| Nome | Obbligatorio/Ripetuto | Tipo | Note |
| --- | --- | --- | --- |
| **source** |Obbligatorio |String |**origine** tooupdate valore. |

- - -
### <a name="switch"></a>Switch
**Funzione:**<br> Switch(source, defaultValue, key1, value1, key2, value2, …)

**Descrizione:**<br> Quando il valore **source** corrisponde a **key**, verrà restituito un parametro **value** per tale oggetto **key**. Se il valore del parametro **source** non corrisponde ad alcuna chiave, verrà restituito **defaultValue**.  I parametri **key** e **value** devono essere sempre accoppiati. funzione Hello prevede sempre un numero pari di parametri.

**Parametri:**<br> 

| Nome | Obbligatorio/Ripetuto | Tipo | Note |
| --- | --- | --- | --- |
| **source** |Obbligatorio |String |**Origine** tooupdate valore. |
| **defaultValue** |Facoltativo |String |Toobe di valore predefinito utilizzato quando l'origine non corrisponde ad alcuna chiave. Può essere una stringa vuota (""). |
| **key** |Obbligatorio |String |**Chiave** toocompare **origine** valore con. |
| **value** |Obbligatorio |String |Valore sostitutivo per hello **origine** chiave hello corrispondente. |

## <a name="examples"></a>esempi
### <a name="strip-known-domain-name"></a>Rimuovere un nome di dominio noto
È necessario toostrip un nome di dominio noto dal tooobtain di posta elettronica dell'utente un nome utente. <br>
Ad esempio, se è "contoso.com" hello, è possibile utilizzare hello espressione seguente:

**Espressione:** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**Input/output di esempio:** <br>

* **INPUT** (mail): "john.doe@contoso.com"
* **OUTPUT**: "john.doe"

### <a name="append-constant-suffix-toouser-name"></a>Aggiungere il suffisso costante toouser nome
Se si utilizza un ambiente Salesforce Sandbox, potrebbe essere tooappend tooall un suffisso i nomi utente prima di sincronizzarli.

**Espressione:** <br>
`Append([userPrincipalName], ".test"))`

**Input/output di esempio:** <br>

* **INPUT** (userPrincipalName): "John.Doe@contoso.com"
* **OUTPUT**: "John.Doe@contoso.com.test"

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>Generare un alias utente concatenando parti del nome e del cognome
È necessario un alias utente toogenerate adottando i primi 3 lettere del nome dell'utente e le prime 5 lettere del cognome dell'utente.

**Espressione:** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**Input/output di esempio:** <br>

* **INPUT** (givenName): "John"
* **INPUT** (surname): "Doe"
* **OUTPUT**: "JohDoe"

### <a name="output-date-as-a-string-in-a-certain-format"></a>Eseguire l'output della data come stringa in un formato specifico
Si desidera toosend applicazione SaaS tooa di date in un formato specifico. <br>
Ad esempio, si desidera tooformat date per ServiceNow.

**Espressione:** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**Input/output di esempio:**

* **INPUT** (extensionAttribute1): "20150123105347.1Z"
* **OUTPUT**: "2015-01-23"

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>Sostituire un valore in base a un set di opzioni predefinito
È necessario toodefine hello fuso orario dell'utente hello in base al codice di stato hello archiviati in Azure AD. <br>
Se il codice di stato hello non corrisponde a una delle opzioni di hello predefinito, utilizzare il valore predefinito di "Australia/Sydney".

**Espressione:** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**Input/output di esempio:**

* **INPUT** (state): "QLD"
* **OUTPUT**: "Australia/Brisbane"

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Automatizzare tooSaaS utente Provisioning o Deprovisioning App](active-directory-saas-app-provisioning.md)
* [Personalizzazione dei mapping degli attributi per il Provisioning dell’utente](active-directory-saas-customizing-attribute-mappings.md)
* [Ambito dei filtri per il Provisioning utente](active-directory-saas-scoping-filters.md)
* [Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notifiche relative al provisioning dell'account](active-directory-saas-account-provisioning-notifications.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS](active-directory-saas-tutorial-list.md)

