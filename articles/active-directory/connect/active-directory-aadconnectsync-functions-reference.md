---
title: 'Servizio di sincronizzazione Azure AD Connect: Riferimento alle funzioni | Documentazione Microsoft'
description: Riferimento delle espressioni di provisioning dichiarativo nel servizio di sincronizzazione Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Servizio di sincronizzazione Azure AD Connect: Riferimento alle funzioni
In Azure AD Connect, le funzioni sono toomanipulate utilizzato un valore di attributo durante la sincronizzazione.  
Sintassi delle funzioni hello Hello viene espresso nel formato hello seguente formato:  
`<output type> FunctionName(<input type> <position name>, ..)`

Se una funzione è in overload e accetta più sintassi, verranno elencate tutte quelle valide.  
le funzioni Hello sono fortemente tipizzate e verificano che il tipo di hello passato nel tipo hello documentato corrispondenze.  
Se il tipo di hello non corrisponde, viene generato un errore.

tipi di Hello sono espressi con hello la seguente sintassi:

* **bin** : binario
* **bool** : booleano
* **dt** : data/ora UTC
* **enum** : enumerazione di costanti note
* **EXP** : espressione, è previsto tooevaluate tooa booleano
* **mvbin** : binario multivalore
* **mvstr** : stringa multivalore
* **mvref** : riferimento multivalore
* **num** : numerico
* **ref** : riferimento
* **str** : stringa
* **var** : variante di (quasi) tutti gli altri tipi
* **void** : non restituisce un valore

funzioni con i tipi di hello Hello **mvbin**, **mvstr**, e **mvref** può funzionare solo su attributi multivalore. Le funzioni con **bin**, **str** e **ref** operano con gli attributi a valore singolo e multivalore.

## <a name="functions-reference"></a>Riferimento alle funzioni
| Elenco di funzioni |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Certificate** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[ CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **Conversione** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Data/Ora** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Now](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **Directory** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **Versione di valutazione** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Matematiche** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **A più valori** | | | | |
| [Contiene](#contains) |[Numero](#count) |[Elemento](#item) |[ItemOrNull](#itemornull) | |
| [Join](#join) |[RemoveDuplicates](#removeduplicates) |[Split](#split) | | |
| **Flusso del programma** | | | | |
| [Errore](#error) |[IIF](#iif) |[Selezionare](#select) |[Switch](#switch) | |
| [Dove](#where) |[With](#with) | | | |
| **Text** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Left](#left) |[Len](#len) |[LTrim](#ltrim) |[Mid](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Replace](#replace) | |
| [ReplaceChars](#replacechars) |[Right](#right) |[RTrim](#rtrim) |[Trim](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**Descrizione:**  
Hello funzione BitAnd imposta i bit specificati su un valore.

**Sintassi:**  
`num BitAnd(num value1, num value2)`

* value1, value2: valori numerici da unire con AND

**Osservazioni:**  
Questa funzione converte una rappresentazione binaria di toohello entrambi i parametri e imposta un bit:

* 0 - se uno o entrambi i bit corrispondenti di hello *mask* e *flag* sono pari a 0
* 1 - se nessuno dei bit corrispondenti hello è 1.

In altre parole, restituisce 0 in tutti i casi tranne quando hello bit corrispondenti di entrambi i parametri hanno valore 1.

**Esempio:**  
`BitAnd(&HF, &HF7)`  
Restituisce 7 esadecimale "F" e "F7" restituiscono il valore toothis.

- - -
### <a name="bitor"></a>BitOr
**Descrizione:**  
Hello funzione BitOr imposta i bit specificati su un valore.

**Sintassi:**  
`num BitOr(num value1, num value2)`

* value1, value2: valori numerici da unire con OR

**Osservazioni:**  
Questa funzione converte una rappresentazione binaria di toohello entrambi i parametri e imposta un too1 bit se uno o entrambi i bit corrispondenti di hello nella maschera e nel flag sono 1 e too0 se entrambi i bit corrispondenti hello è 0. In altre parole, restituisce 1 in tutti i casi tranne dove hello bit corrispondenti di entrambi i parametri hanno valore 0.

- - -
### <a name="cbool"></a>CBool
**Descrizione:**  
Hello funzione CBool restituisce che un valore booleano basato su espressione valutata hello

**Sintassi:**  
`bool CBool(exp Expression)`

**Osservazioni:**  
Se l'espressione hello restituisce tooa valore diverso da zero, CBool restituisce True, altrimenti restituisce False.

**Esempio:**  
`CBool([attrib1] = [attrib2])`  

Restituisce True se entrambi attributi hanno hello stesso valore.

- - -
### <a name="cdate"></a>CDate
**Descrizione:**  
Hello funzione CDate restituisce un valore DateTime UTC da una stringa. DateTime non è un attributo nativo in Sync, ma viene usato da alcune funzioni.

**Sintassi:**  
`dt CDate(str value)`

* Value: una stringa con una data, un'ora e facoltativamente un fuso orario

**Osservazioni:**  
Hello restituito è sempre di stringa in formato UTC.

**Esempio:**  
`CDate([employeeStartTime])`  
Restituisce un valore DateTime in base a ora di inizio del dipendente hello

`CDate("2013-01-10 4:00 PM -8")`  
Restituisce un valore di data/ora che rappresenta "2013-01-11 12:00 AM"








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**Descrizione:**  
Restituisce hello Oid valori di tutte le estensioni critiche hello di un oggetto del certificato.

**Sintassi:**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certformat"></a>CertFormat
**Descrizione:**  
Restituisce hello nome del formato di hello del certificato x. 509v3.

**Sintassi:**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**Descrizione:**  
Restituisce l'alias di un certificato associato hello.

**Sintassi:**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certhashstring"></a>CertHashString
**Descrizione:**  
Restituisce hello valore hash SHA1 per il certificato x. 509v3 hello sotto forma di stringa esadecimale.

**Sintassi:**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certissuer"></a>CertIssuer
**Descrizione:**  
Restituisce hello nome dell'autorità di certificazione hello che ha emesso il certificato di x. 509v3 hello.

**Sintassi:**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**Descrizione:**  
Restituisce hello nome distinto dell'autorità di certificazione hello.

**Sintassi:**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**Descrizione:**  
Restituisce hello Oid dell'autorità di certificazione hello.

**Sintassi:**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**Descrizione:**  
Restituisce le informazioni dell'algoritmo delle chiavi di hello per il certificato x. 509v3 sotto forma di stringa.

**Sintassi:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**Descrizione:**  
Restituisce i parametri dell'algoritmo delle chiavi di hello certificato x. 509v3 hello sotto forma di stringa esadecimale.

**Sintassi:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**Descrizione:**  
Restituisce autorità emittente e oggetto hello nomi da un certificato.

**Sintassi:**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.
*   X509NameType: hello X509NameType valore per il soggetto hello.
*   includesIssuerName: nome dell'autorità emittente di hello tooinclude true; in caso contrario, false.

- - -
### <a name="certnotafter"></a>CertNotAfter
**Descrizione:**  
Restituisce la data hello nell'ora locale dopo il quale un certificato non è più valido.

**Sintassi:**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**Descrizione:**  
Restituisce la data hello nell'ora locale in cui un certificato diventa valido.

**Sintassi:**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**Descrizione:**  
Restituisce hello Oid della chiave pubblica di hello certificato x. 509v3 hello.

**Sintassi:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**Descrizione:**  
Restituisce hello Oid dei parametri di chiave pubblica hello certificato x. 509v3 hello.

**Sintassi:**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**Descrizione:**  
Restituisce il numero di serie hello del certificato x. 509v3 hello.

**Sintassi:**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**Descrizione:**  
Restituisce hello Oid dell'algoritmo hello utilizzato firma hello toocreate di un certificato.

**Sintassi:**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certsubject"></a>CertSubject
**Descrizione:**  
Ottiene hello nome distinto del soggetto da un certificato.

**Sintassi:**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**Descrizione:**  
Restituisce hello nome distinto del soggetto da un certificato.

**Sintassi:**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**Descrizione:**  
Restituisce hello Oid del nome soggetto hello da un certificato.

**Sintassi:**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certthumbprint"></a>CertThumbprint
**Descrizione:**  
Restituisce hello identificazione personale del certificato.

**Sintassi:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="certversion"></a>CertVersion
**Descrizione:**  
Restituisce hello versione del formato di un certificato x. 509.

**Sintassi:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.

- - -
### <a name="cguid"></a>CGuid
**Descrizione:**  
Hello funzione CGuid Converte la rappresentazione di stringa hello della rappresentazione binaria di tooits GUID.

**Sintassi:**  
`bin CGuid(str GUID)`

* Stringa formattata con questo schema: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Contiene
**Descrizione:**  
funzione Contains Hello trova una stringa all'interno di un attributo multivalore

**Sintassi:**  
`num Contains (mvstring attribute, str search)` - distinzione maiuscole/minuscole  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)` - distinzione maiuscole/minuscole

* attributo: hello toosearch di un attributo multivalore.
* ricerca: stringa toofind nell'attributo hello.
* Casetype: CaseInsensitive o CaseSensitive.

Restituisce l'indice nell'attributo multivalore hello in cui trovare la stringa hello. Se la stringa hello non viene trovata, viene restituito 0.

**Osservazioni:**  
Per gli attributi di stringa multivalore, ricerca hello trova le sottostringhe nei valori hello.  
Per gli attributi di riferimento, hello stringa cercata deve corrispondere esattamente toobe valore hello considerata una corrispondenza.

**Esempio:**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Se l'attributo proxyAddresses hello dispone di un indirizzo di posta elettronica primario (indicato da lettere maiuscole "SMTP:"), quindi restituire l'attributo proxyAddress hello, in caso contrario, restituisce un errore.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**Descrizione:**  
Hello ConvertFromBase64 funzione converte hello specificato stringa regolare tooa di valore con codificata base64.

**Sintassi:**  
`str ConvertFromBase64(str source)`: presuppone l'uso di Unicode per la codifica  
`str ConvertFromBase64(str source, enum Encoding)`

* source: stringa con codifica Base 64  
* Encoding: Unicode, ASCII, UTF8

**Esempio**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

Entrambi gli esempi restituiscono "*Hello world!*"

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**Descrizione:**  
Hello ConvertFromUTF8Hex funzione converte hello specificato stringa tooa di valore con codifica Hex UTF8.

**Sintassi:**  
`str ConvertFromUTF8Hex(str source)`

* source: stringa con codifica a 2 byte UTF8

**Osservazioni:**  
Hello differenza tra questa funzione e ConvertFromBase64([],UTF8) tale risultato hello è descrittivo per l'attributo DN hello.  
Questo formato viene utilizzato da Azure Active Directory come DN.

**Esempio:**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
Restituisce "*Hello world!*"

- - -
### <a name="converttobase64"></a>ConvertToBase64
**Descrizione:**  
Hello funzione ConvertToBase64 converte una stringa base 64 Unicode di tooa stringa.  
Converte il valore di hello di una matrice di interi tooits equivalente rappresentazione di stringa codificata con cifre base 64.

**Sintassi:**  
`str ConvertToBase64(str source)`

**Esempio:**  
`ConvertToBase64("Hello world!")`  
Restituisce "SABlAGwAbABvACAAdwBvAHIAbABkACEA"

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**Descrizione:**  
Hello funzione ConvertToUTF8Hex converte tooa una stringa valore Hex UTF8.

**Sintassi:**  
`str ConvertToUTF8Hex(str source)`

**Osservazioni:**  
formato di output di Hello di questa funzione viene usato da Azure Active Directory come formato di attributo DN.

**Esempio:**  
`ConvertToUTF8Hex("Hello world!")`  
Restituisce 48656C6C6F20776F726C6421

- - -
### <a name="count"></a>Numero
**Descrizione:**  
Hello funzione Count restituisce il numero di hello di elementi in un attributo multivalore

**Sintassi:**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**Descrizione:**  
Hello funzione CNum accetta una stringa e restituisce un tipo di dati numerici.

**Sintassi:**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**Descrizione:**  
Converte un attributo di riferimento di stringa tooa

**Sintassi:**  
`ref CRef(str value)`

**Esempio:**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**Descrizione:**  
Hello dalla funzione CStr converte il tipo di dati stringa tooa.

**Sintassi:**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* value: può essere un valore numerico, un attributo di riferimento o un valore booleano.

**Esempio:**  
`CStr([dn])`  
Può restituire "cn=Joe,dc=contoso,dc=com"

- - -
### <a name="dateadd"></a>DateAdd
**Descrizione:**  
Restituisce un valore Date contenente un toowhich data che è stato aggiunto un intervallo di tempo specificato.

**Sintassi:**  
`dt DateAdd(str interval, num value, dt date)`

* intervallo: espressione stringa che rappresenta l'intervallo di hello dell'ora in cui si desidera tooadd. la stringa Hello deve avere uno dei seguenti valori hello:
  * yyyy Year
  * q Quarter
  * m Month
  * y Day of year
  * d Day
  * w Weekday
  * ww Week
  * h Hour
  * n Minute
  * s Second
* valore: hello numero di unità si desidera tooadd. Può essere positivo (tooget date nel futuro hello) o negativo (tooget date in hello precedente).
* Data: DateTime che rappresenta data toowhich hello intervallo viene aggiunto.

**Esempio:**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
Aggiunge 3 mesi e restituisce un valore di data/ora che rappresenta "2001-04-01".

- - -
### <a name="datefromnum"></a>DateFromNum
**Descrizione:**  
Hello funzione DateFromNum converte un valore in tooa di formato data AD tipo DateTime.

**Sintassi:**  
`dt DateFromNum(num value)`

**Esempio:**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
Restituisce un valore di data/ora che rappresenta 2012-01-01 23:00:00

- - -
### <a name="dncomponent"></a>DNComponent
**Descrizione:**  
Hello funzione DNComponent restituisce il valore di hello di un componente DN specificato da sinistra.

**Sintassi:**  
`str DNComponent(ref dn, num ComponentNumber)`

* DN: hello riferimento attributo toointerpret
* ComponentNumber: componente di hello hello DN tooreturn

**Esempio:**  
`DNComponent([dn],1)`  
Se dn è "cn=Joe,ou=…," verrà restituito Joe

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**Descrizione:**  
Hello funzione DNComponentRev restituisce il valore di hello di un componente DN specificato da destra (fine hello).

**Sintassi:**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* DN: hello riferimento attributo toointerpret
* ComponentNumber - componente hello tooreturn hello DN
* Options: DC - Ignora tutti i componenti con "dc="

**Esempio:**  
Se dn è "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com", allora  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
restituiscono entrambi US.

- - -
### <a name="error"></a>Errore
**Descrizione:**  
funzione di errore Hello è tooreturn usato un errore personalizzato.

**Sintassi:**  
`void Error(str ErrorMessage)`

**Esempio:**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Se hello attributo accountName non è presente, verrà generato un errore nell'oggetto hello.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**Descrizione:**  
Hello funzione EscapeDNComponent accetta un componente di un DN e utilizza caratteri di escape in modo può essere rappresentato in LDAP.

**Sintassi:**  
`str EscapeDNComponent(str value)`

**Esempio:**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
Assicura che l'oggetto di hello può essere creato in una directory LDAP, anche se l'attributo displayName hello contiene caratteri che devono essere sottoposti a escape in LDAP.

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Descrizione:**  
Funzione FormatDateTime Hello è tooformat utilizzata una stringa tooa DateTime con un formato specificato

**Sintassi:**  
`str FormatDateTime(dt value, str format)`

* valore: un valore in formato DateTime hello
* formato: una stringa che rappresenta hello formato tooconvert per.

**Osservazioni:**  
Hello i valori possibili per il formato di hello è disponibili qui: [formati di data/ora definiti dall'utente (funzione Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**Esempio:**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
Il risultato è "2007-12-25".

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
Può restituire "20140905081453.0Z"

- - -
### <a name="guid"></a>GUID
**Descrizione:**  
funzione Hello GUID genera un nuovo GUID casuale

**Sintassi:**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**Descrizione:**  
Hello funzione IIF restituisce un set di valori possibili in base a una condizione specificata.

**Sintassi:**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* condizione: qualsiasi valore o espressione che può essere valutata tootrue o false.
* valueIfTrue: se hello Condition tootrue, hello restituito di valore.
* valueIfFalse: se hello Condition toofalse, hello restituito di valore.

**Esempio:**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Se l'utente di hello è un interno, restituisce hello alias di un utente con"t" aggiunto toohello inizio, else restituisce hello alias utente è.

- - -
### <a name="instr"></a>InStr
**Descrizione:**  
Hello funzione InStr trova hello prima occorrenza di una sottostringa in una stringa

**Sintassi:**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* StringCheck: toobe la ricerca di stringhe
* StringMatch: stringa toobe trovato
* Start: avvio posizione toofind hello sottostringa
* compare: vbTextCompare o vbBinaryCompare

**Osservazioni:**  
Posizione di hello restituisce in cui è stata trovata la sottostringa hello o 0 se non trovato.

**Esempio:**  
`InStr("hello quick brown fox","quick")`  
/ / Restituisce too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Valuta too7

- - -
### <a name="instrrev"></a>InStrRev
**Descrizione:**  
Hello funzione InStrRev trova hello l'ultima occorrenza di una sottostringa in una stringa

**Sintassi:**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* StringCheck: toobe la ricerca di stringhe
* StringMatch: stringa toobe trovato
* Start: avvio posizione toofind hello sottostringa
* compare: vbTextCompare o vbBinaryCompare

**Osservazioni:**  
Posizione di hello restituisce in cui è stata trovata la sottostringa hello o 0 se non trovato.

**Esempio:**  
`InStrRev("abbcdbbbef","bb")`  
Restituisce 7

- - -
### <a name="isbitset"></a>IsBitSet
**Descrizione:**  
funzione Hello IsBitSet verifica se un bit è impostato o non

**Sintassi:**  
`bool IsBitSet(num value, num flag)`

* valore: un valore numerico valutato. flag: un valore numerico che è hello bit toobe valutata

**Esempio:**  
`IsBitSet(&HF,4)`  
Restituisce True perché bit "4" è impostato il valore esadecimale di hello "F"

- - -
### <a name="isdate"></a>IsDate
**Descrizione:**  
Se può essere espressione hello valuta come tipo DateTime, hello funzione IsDate restituisce tooTrue.

**Sintassi:**  
`bool IsDate(var Expression)`

**Osservazioni:**  
Utilizzare toodetermine se CDate () può avere esito positivo.

- - -
### <a name="iscert"></a>IsCert
**Descrizione:**  
Restituisce true se i dati non elaborati hello possono essere serializzati in oggetto certificato X509Certificate2 .NET.

**Sintassi:**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509. Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.
- - -
### <a name="isempty"></a>IsEmpty
**Descrizione:**  
Se l'attributo hello è presente in hello CS o MV, ma restituisce una stringa vuota tooan, funzione IsEmpty hello valuta tooTrue.

**Sintassi:**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**Descrizione:**  
Se la stringa hello può essere convertito tooa GUID, funzione isguid restituisce hello valutata tootrue.

**Sintassi:**  
`bool IsGuid(str GUID)`

**Osservazioni:**  
Un GUID viene definito come stringa in base a uno degli schemi seguenti: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

Utilizzare toodetermine se cguid () può avere esito positivo.

**Esempio:**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Se hello StrAttribute ha un formato GUID, restituisce una rappresentazione binaria, in caso contrario, restituire un valore Null.

- - -
### <a name="isnull"></a>IsNull
**Descrizione:**  
Se hello espressione tooNull, funzione IsNull hello restituisce true.

**Sintassi:**  
`bool IsNull(var Expression)`

**Osservazioni:**  
Per un attributo, un valore Null è espresso dall'assenza di hello dell'attributo hello.

**Esempio:**  
`IsNull([displayName])`  
Restituisce True se l'attributo hello non è presente in hello CS o MV.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**Descrizione:**  
Se l'espressione di hello è null o una stringa vuota, funzione IsNullOrEmpty hello restituisce true.

**Sintassi:**  
`bool IsNullOrEmpty(var Expression)`

**Osservazioni:**  
Per un attributo, verrà restituito tooTrue se attributo hello è assente o è presente ma è una stringa vuota.  
funzione inversa di Hello di questa funzione è denominata IsPresent.

**Esempio:**  
`IsNullOrEmpty([displayName])`  
Restituisce True se l'attributo hello non è presente o è una stringa vuota in hello CS o MV.

- - -
### <a name="isnumeric"></a>IsNumeric
**Descrizione:**  
Hello funzione IsNumeric restituisce un valore booleano che indica se un'espressione può essere valutata come tipo di numero.

**Sintassi:**  
`bool IsNumeric(var Expression)`

**Osservazioni:**  
Utilizzare toodetermine se cnum () può essere espressione hello tooparse ha esito positivo.

- - -
### <a name="isstring"></a>IsString
**Descrizione:**  
Se l'espressione hello può essere valutata tooa tipo stringa, quindi funzione IsString hello valuta tooTrue.

**Sintassi:**  
`bool IsString(var expression)`

**Osservazioni:**  
Utilizzare toodetermine se CStr () può essere espressione hello tooparse ha esito positivo.

- - -
### <a name="ispresent"></a>IsPresent
**Descrizione:**  
Se hello espressione stringa tooa che non è Null e non è vuoto, quindi hello IsPresent restituisce true.

**Sintassi:**  
`bool IsPresent(var expression)`

**Osservazioni:**  
funzione inversa di Hello di questa funzione è denominata IsNullOrEmpty.

**Esempio:**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Elemento
**Descrizione:**  
Hello funzione Item restituisce un elemento da una stringa o un attributo multivalore.

**Sintassi:**  
`var Item(mvstr attribute, num index)`

* attribute: attributo multivalore
* indice: elemento tooan indice stringa multivalore hello.

**Osservazioni:**  
Hello funzione Item è utile insieme hello funzione Contains perché hello quest'ultima restituisce l'elemento tooan hello indice nell'attributo multivalore hello.

Genera un errore se l'indice non è compreso nell'intervallo.

**Esempio:**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
Restituisce hello indirizzo di posta elettronica primario.

- - -
### <a name="itemornull"></a>ItemOrNull
**Descrizione:**  
Hello funzione ItemOrNull restituisce un elemento da una stringa o un attributo multivalore.

**Sintassi:**  
`var ItemOrNull(mvstr attribute, num index)`

* attribute: attributo multivalore
* indice: elemento tooan indice stringa multivalore hello.

**Osservazioni:**  
funzione ItemOrNull Hello è utile insieme hello funzione Contains perché hello quest'ultima restituisce l'elemento tooan hello indice nell'attributo multivalore hello.

Se l'indice non è compreso nell'intervallo, restituisce un valore Null.

- - -
### <a name="join"></a>Join
**Descrizione:**  
funzione Join Hello accetta una stringa multivalore e restituisce una stringa a valore singolo con il separatore specificato inserito tra ogni elemento.

**Sintassi:**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* attributo: attributo multivalore contenente stringhe toobe unita in join.
* delimitatore: qualsiasi stringa, tooseparate utilizzati hello sottostringhe hello ha restituito una stringa. Se omesso, hello carattere spazio ("") viene utilizzato. Se Delimiter è una stringa di lunghezza zero ("") o Nothing, tutti gli elementi nell'elenco di hello vengono concatenati senza delimitatori.

**Osservazioni**  
Vi è parità tra hello Join e le funzioni di divisione. Hello funzione Join accetta una matrice di stringhe e le unisce con una stringa di delimitazione tooreturn un'unica stringa. Hello funzione Split accetta una stringa e la separa in corrispondenza delimitatore hello, tooreturn una matrice di stringhe. Tuttavia, la differenza principale consiste nel fatto che Join può concatenare stringhe con qualsiasi stringa delimitatore, mentre Split può separare stringhe usando unicamente un delimitatore di un solo carattere.

**Esempio:**  
`Join([proxyAddresses],",")`  
Può restituire: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"

- - -
### <a name="lcase"></a>LCase
**Descrizione:**  
Hello funzione LCase converte tutti i caratteri in una stringa toolower maiuscole.

**Sintassi:**  
`str LCase(str value)`

**Esempio:**  
`LCase("TeSt")`  
Restituisce "test".

- - -
### <a name="left"></a>Left
**Descrizione:**  
funzione Left Hello restituisce un numero specificato di caratteri da sinistra hello di una stringa.

**Sintassi:**  
`str Left(str string, num NumChars)`

* stringa: hello tooreturn caratteri della stringa da
* NumChars: un numero che identifica il numero di hello di tooreturn caratteri dall'inizio di hello (sinistra) della stringa

**Osservazioni:**  
Stringa contenente i primi caratteri numChars hello nella stringa:

* Se numChars = 0, restituisce una stringa vuota.
* Se numChars < 0, restituisce una stringa di input.
* Se string è Null, restituisce una stringa vuota.

Se string contiene un minor numero di caratteri hello numero specificato in numChars, viene restituito un toostring identici stringa (che è, contenente tutti i caratteri nel parametro 1).

**Esempio:**  
`Left("John Doe", 3)`  
Restituisce "Joh".

- - -
### <a name="len"></a>Len
**Descrizione:**  
Hello funzione Len restituisce numero di caratteri in una stringa.

**Sintassi:**  
`num Len(str value)`

**Esempio:**  
`Len("John Doe")`  
Restituisce 8

- - -
### <a name="ltrim"></a>LTrim
**Descrizione:**  
Hello funzione LTrim rimuove gli spazi vuoti iniziali da una stringa.

**Sintassi:**  
`str LTrim(str value)`

**Esempio:**  
`LTrim(" Test ")`  
Restituisce "Test"

- - -
### <a name="mid"></a>Mid
**Descrizione:**  
Hello Mid restituisce un numero specificato di caratteri da una posizione specificata in una stringa.

**Sintassi:**  
`str Mid(str string, num start, num NumChars)`

* stringa: hello tooreturn caratteri della stringa da
* Start: numero che identifica hello in caratteri della stringa tooreturn dalla posizione iniziale
* NumChars: un numero che identifica il numero di hello di tooreturn caratteri dalla posizione nella stringa

**Osservazioni:**  
Restituisce i caratteri in numChars a partire dalla posizione start nella stringa.  
Stringa contenente i caratteri specificati in numChars a partire dalla posizione start nella stringa:

* Se numChars = 0, restituisce una stringa vuota.
* Se numChars < 0, restituisce una stringa di input.
* Se start > hello lunghezza della stringa, per restituire una stringa di input.
* Se start <= 0, restituisce la stringa di input.
* Se string è Null, restituisce una stringa vuota.

Se nella stringa non ci sono caratteri numChar rimanenti dalla posizione start, vengono restituiti quanti più caratteri possibile.

**Esempio:**  
`Mid("John Doe", 3, 5)`  
Restituisce "hn Do".

`Mid("John Doe", 6, 999)`  
Restituisce "Doe"

- - -
### <a name="now"></a>Now
**Descrizione:**  
Hello ora funzione restituisce un valore DateTime specificando hello data corrente e l'ora, in base tooyour data di sistema del computer e l'ora.

**Sintassi:**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**Descrizione:**  
Hello funzione NumFromDate restituisce una data nel formato di data dell'annuncio.

**Sintassi:**  
`num NumFromDate(dt value)`

**Esempio:**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
Restituisce 129699324000000000

- - -
### <a name="padleft"></a>PadLeft
**Descrizione:**  
Hello PadLeft funzione sinistra Pad tooa una stringa specificata lunghezza utilizzando un carattere di riempimento specificato.

**Sintassi:**  
`str PadLeft(str string, num length, str padCharacter)`

* stringa: hello toopad stringa.
* lunghezza: valore intero che rappresenta hello desiderato lunghezza della stringa.
* padCharacter: stringa costituita da un singolo carattere toouse come carattere di riempimento hello

**Osservazioni:**

* Se hello lunghezza della stringa è minore della lunghezza, padCharacter viene aggiunto ripetutamente toohello inizio (sinistra) della stringa fino a quando non ha un toolength di uguale lunghezza.
* PadCharacter può essere uno spazio, ma non un valore null.
* Se la lunghezza hello della stringa è uguale tooor maggiore lunghezza, stringa viene restituita invariata.
* Se string ha una lunghezza maggiore di o uguale toolength, viene restituito un toostring identiche di stringa.
* Se la lunghezza hello della stringa è minore della lunghezza, una nuova stringa di hello desiderato lunghezza viene restituita contenente string con l'aggiunta di padCharacter.
* Se string è null, la funzione hello restituisce una stringa vuota.

**Esempio:**  
`PadLeft("User", 10, "0")`  
Restituisce "000000User".

- - -
### <a name="padright"></a>PadRight
**Descrizione:**  
Hello PadRight funzione destra riempie tooa una stringa specificata lunghezza utilizzando un carattere di riempimento specificato.

**Sintassi:**  
`str PadRight(str string, num length, str padCharacter)`

* stringa: hello toopad stringa.
* lunghezza: valore intero che rappresenta hello desiderato lunghezza della stringa.
* padCharacter: stringa costituita da un singolo carattere toouse come carattere di riempimento hello

**Osservazioni:**

* Se hello lunghezza della stringa è minore della lunghezza, padCharacter viene aggiunto ripetutamente toohello fine (destra) della stringa fino a quando non ha un toolength di uguale lunghezza.
* PadCharacter può essere uno spazio, ma non un valore null.
* Se la lunghezza hello della stringa è uguale tooor maggiore lunghezza, stringa viene restituita invariata.
* Se string ha una lunghezza maggiore di o uguale toolength, viene restituito un toostring identiche di stringa.
* Se la lunghezza hello della stringa è minore della lunghezza, una nuova stringa di hello desiderato lunghezza viene restituita contenente string con l'aggiunta di padCharacter.
* Se string è null, la funzione hello restituisce una stringa vuota.

**Esempio:**  
`PadRight("User", 10, "0")`  
Restituisce "User000000".

- - -
### <a name="pcase"></a>PCase
**Descrizione:**  
Hello funzione PCase converte hello primo carattere di ogni parola delimitato da spazi in un caso tooupper stringa e tutti gli altri caratteri vengono convertiti toolower case.

**Sintassi:**  
`String PCase(string)`

**Osservazioni:**

* Questa funzione non fornisce attualmente tooconvert di maiuscole e minuscole appropriata una parola interamente in maiuscolo, ad esempio un acronimo.

**Esempio:**  
`PCase("TEsT")`  
Restituisce "test".

`PCase(LCase("TEST"))`  
Restituisce "Test"

- - -
### <a name="randomnum"></a>RandomNum
**Descrizione:**  
Hello funzione RandomNum restituisce un numero casuale tra un intervallo specificato.

**Sintassi:**  
`num RandomNum(num start, num end)`

* Start: un numero identificativo hello limite inferiore di hello valore casuale toogenerate
* fine: un numero identificativo hello limite massimo di hello valore casuale toogenerate

**Esempio:**  
`Random(100,999)`  
Può restituire 734.

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**Descrizione:**  
Hello funzione RemoveDuplicates accetta una stringa multivalore e assicurarsi che ogni valore univoco.

**Sintassi:**  
`mvstr RemoveDuplicates(mvstr attribute)`

**Esempio:**  
`RemoveDuplicates([proxyAddresses])`  
Restituisce un attributo proxyAddress purificato in cui sono stati rimossi tutti i valori duplicati.

- - -
### <a name="replace"></a>Replace
**Descrizione:**  
Hello funzione Replace sostituisce tutte le occorrenze di una stringa tooanother stringa.

**Sintassi:**  
`str Replace(str string, str OldValue, str NewValue)`

* stringa: tooreplace una stringa i valori.
* OldValue: hello stringa toosearch per e tooreplace.
* NewValue: hello stringa tooreplace per.

**Osservazioni:**  
funzione Hello riconosce hello moniker speciali seguenti:

* \n - Nuova riga
* \r - Ritorno a capo
* \t - Tabulazione

**Esempio:**  
`Replace([address],"\r\n",", ")`  
Sostituisce CRLF con una virgola e uno spazio e provocare troppo "Uno Microsoft modo, Redmond, WA, USA"

- - -
### <a name="replacechars"></a>ReplaceChars
**Descrizione:**  
Hello funzione ReplaceChars sostituisce tutte le occorrenze dei caratteri trovati nella stringa ReplacePattern hello.

**Sintassi:**  
`str ReplaceChars(str string, str ReplacePattern)`

* stringa: tooreplace una stringa di caratteri.
* ReplacePattern: una stringa contenente un dizionario con tooreplace caratteri.

formato hello è {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetN} in cui origine è hello carattere toofind e destinazione hello stringa tooreplace con.

**Osservazioni:**

* funzione Hello accetta ogni occorrenza dei valori Source definiti e li sostituisce con destinazioni hello.
* origine Hello deve essere esattamente un carattere (unicode).
* Hello origine non può essere vuoto o più di un carattere (errore di analisi).
* destinazione Hello può contenere più caratteri, ad esempio ö: OE, β: ss.
* destinazione Hello può essere vuoto che indica che il carattere di hello deve essere rimosse.
* origine Hello tra maiuscole e minuscole e deve essere una corrispondenza esatta.
* Hello, (virgola) e: (due punti) sono riservati e non può essere sostituito con questa funzione.
* Gli spazi e altri caratteri vuoti nella stringa ReplacePattern hello vengono ignorati.

**Esempio:**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
Restituisce Raksmorgas

`ReplaceChars("O’Neil",%ReplaceString%)`  
Restituisce "ONeil", singolo tick hello è definito toobe rimosso.

- - -
### <a name="right"></a>Right
**Descrizione:**  
funzione Right Hello restituisce un numero specificato di caratteri da hello destra (fine) di una stringa.

**Sintassi:**  
`str Right(str string, num NumChars)`

* stringa: hello tooreturn caratteri della stringa da
* NumChars: un numero che identifica il numero di hello di tooreturn caratteri dalla fine di hello (destra) della stringa

**Osservazioni:**  
Caratteri NumChars vengono restituiti dall'ultima posizione di hello della stringa.

Stringa contenente hello ultimi caratteri numChars in string:

* Se numChars = 0, restituisce una stringa vuota.
* Se numChars < 0, restituisce una stringa di input.
* Se string è Null, restituisce una stringa vuota.

Se string contiene un numero di caratteri inferiore a hello numero specificato in NumChars, viene restituito un toostring identiche di stringa.

**Esempio:**  
`Right("John Doe", 3)`  
Restituisce "Doe".

- - -
### <a name="rtrim"></a>RTrim
**Descrizione:**  
Hello funzione RTrim rimuove gli spazi vuoti finali da una stringa.

**Sintassi:**  
`str RTrim(str value)`

**Esempio:**  
`RTrim(" Test ")`  
Restituisce "test".

- - -
### <a name="select"></a>Selezionare
**Descrizione:**  
Elabora tutti i valori in un attributo multivalore, o nell'output di un'espressione, in base alla funzione specificata.

**Sintassi:**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* elemento: rappresenta un elemento nell'attributo multivalore hello
* attributo: attributo multivalore hello
* expression: un'espressione che restituisce una raccolta di valori
* condizione: qualsiasi funzione in grado di elaborare un elemento nell'attributo hello

**Esempi:**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Restituire tutti i valori hello in telefono di un attributo multivalore hello dopo avere rimosso trattini (-).

- - -
### <a name="split"></a>Split
**Descrizione:**  
Hello funzione Split accetta una stringa separata dal delimitatore e lo rende una stringa multivalore.

**Sintassi:**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* valore: hello stringa con un tooseparate carattere delimitatore.
* delimitatore: single toobe di carattere utilizzato come delimitatore di hello.
* limit: numero massimo di valori che saranno restituiti.

**Esempio:**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Restituisce una stringa multivalore con 2 elementi utili per l'attributo proxyAddress hello.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**Descrizione:**  
Hello funzione StringFromGuid accetta un GUID binario e lo converte in stringa tooa

**Sintassi:**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**Descrizione:**  
Hello funzione StringFromSid converte una matrice di byte contenente una stringa tooa identificatore di sicurezza.

**Sintassi:**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Switch
**Descrizione:**  
funzione Switch Hello è tooreturn utilizzato un singolo valore in base a condizioni valutate.

**Sintassi:**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* Expr: espressione Variant da tooevaluate.
* valore: toobe valore restituito se l'espressione corrispondente hello è True.

**Osservazioni:**  
argomento della funzione Switch elenco è costituito da coppie di espressioni e valori Hello. Hello espressioni vengono valutate da sinistra tooright e viene restituito il valore di hello associato hello prima espressione tooevaluate tooTrue. Se non vengono accoppiate correttamente parti hello, si verifica un errore di run-time.

Ad esempio, se expr1 è True, Switch restituisce value1. Se expr-1 è False, ma expr-2 è True, Switch restituisce value-2 e così via.

Switch restituisce Nothing se:

* Nessuna delle espressioni di hello è True.
* prima espressione True Hello ha un valore corrispondente è Null.

Switch valuta tutte le espressioni, anche se ne restituisce una sola. Per questo motivo, è opportuno considerare attentamente gli effetti collaterali indesiderati. Ad esempio, se i risultati di valutazione di hello di un'espressione in una divisione per zero, si verifica un errore.

Valore può essere anche funzione di errore hello, che restituisce una stringa personalizzata.

**Esempio:**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
Restituisce hello lingua parlata in alcune città importanti, in caso contrario, restituisce un errore.

- - -
### <a name="trim"></a>Trim
**Descrizione:**  
funzione Trim Hello rimuove iniziali e finali di spazi da una stringa.

**Sintassi:**  
`str Trim(str value)`  

**Esempio:**  
`Trim(" Test ")`  
Restituisce "test".

`Trim([proxyAddresses])`  
Rimuove spazi per ogni valore nell'attributo proxyAddress hello iniziali e finali.

- - -
### <a name="ucase"></a>UCase
**Descrizione:**  
Hello funzione UCase converte tutti i caratteri in una stringa tooupper maiuscole.

**Sintassi:**  
`str UCase(str string)`

**Esempio:**  
`UCase("TeSt")`  
Restituisce "test".

- - -
### <a name="where"></a>Where

**Descrizione:**  
Restituisce un subset di valori di un attributo multivalore, o dell'output di un'espressione, in base alla condizione specifica.

**Sintassi:**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* elemento: rappresenta un elemento nell'attributo multivalore hello
* attributo: attributo multivalore hello
* condizione: qualsiasi espressione che può essere valutata tootrue o false
* expression: un'espressione che restituisce una raccolta di valori

**Esempio:**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
Restituire i valori del certificato hello in hello userCertificate di un attributo multivalore che non sono scaduti.

- - -
### <a name="with"></a>With
**Descrizione:**  
Hello con funzione fornisce un toosimplify modo un'espressione complessa utilizzando una variabile toorepresent una sottoespressione che viene visualizzato uno o più volte nell'espressione complessa hello.

**Sintassi**
`With(var variable, exp subExpression, exp complexExpression)`  
* variabile: rappresenta hello sottoespressione.
* subExpression: sottoespressione rappresentata dalla variabile.
* complexExpression: un'espressione complessa.

**Esempio:**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
Dal punto di vista funzionale equivale a:  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
Che restituisce solo i valori del certificato non scadute nell'attributo userCertificate hello.


- - -
### <a name="word"></a>Word
**Descrizione:**  
Hello funzione Word restituisce una parola contenuta in una stringa, in base ai parametri che descrivono toouse delimitatori hello e hello word numero tooreturn.

**Sintassi:**  
`str Word(str string, num WordNumber, str delimiters)`

* stringa: hello tooreturn di stringa di una parola.
* WordNumber: numero che identifica il numero di parole da restituire.
* delimitatori: una stringa che rappresenta hello/i delimitatore / deve essere utilizzato tooidentify parole

**Osservazioni:**  
Ogni stringa di caratteri nella stringa separati da hello uno dei caratteri hello delimitatori vengono identificati come parole:

* Se number è < 1, restituisce una stringa vuota.
* Se string è Null, restituisce una stringa vuota.

Se la stringa contiene meno delle parole specificate in number o se non contiene alcuna parola identificata da delimiters, viene restituita una stringa vuota.

**Esempio:**  
`Word("hello quick brown fox",3," ")`  
Restituisce "brown"

`Word("This,string!has&many separators",3,",!&#")`  
Restituisce "has"

## <a name="additional-resources"></a>Risorse aggiuntive
* [Informazioni sulle espressioni di provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Servizio di sincronizzazione Azure AD Connect: Personalizzazione delle opzioni di sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
