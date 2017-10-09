---
title: 'Azure AD Connect: Espressioni di provisioning dichiarativo | Documentazione Microsoft'
description: Vengono illustrate le espressioni di provisioning dichiarativo hello.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Servizio di sincronizzazione Azure AD Connect: Informazioni sulle espressioni di provisioning dichiarativo
Il servizio di sincronizzazione Azure AD Connect si basa sul provisioning dichiarativo introdotto inizialmente in Forefront Identity Manager 2010. Consente di tooimplement la logica di business di integrazione completa delle identità senza hello necessità toowrite codice compilato.

Una parte essenziale del provisioning dichiarativo è il linguaggio di espressioni hello utilizzato nei flussi di attributi. linguaggio Hello utilizzato è un subset di Microsoft® Visual Basic for Applications (VBA). Questo linguaggio viene usato in Microsoft Office e verrà riconosciuto anche dagli utenti con esperienza in VBScript. Hello linguaggio delle espressioni di Provisioning dichiarativo Usa solo funzioni e non è un linguaggio strutturato. né include metodi o istruzioni. Le funzioni sono invece annidate tooexpress flusso di programma.

Per ulteriori informazioni, vedere [benvenuto toohello Visual Basic per riferimenti al linguaggio di applicazioni per Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).

gli attributi di Hello sono fortemente tipizzati. Una funzione accetta solo attributi di tipo corretto di hello. Fa anche distinzione tra maiuscole e minuscole. Se per i nomi delle funzioni e degli attributi non viene rispettata correttamente la distinzione maiuscole/minuscole, viene generato un errore.

## <a name="language-definitions-and-identifiers"></a>Definizioni e identificatori del linguaggio
* I nomi delle funzioni sono seguiti dagli argomenti racchiusi tra parentesi: NomeFunzione(argomento 1,argomento N).
* Gli attributi sono identificati da parentesi quadre: [attributeName].
* I parametri sono identificati dal segno di percentuale: %ParameterName%
* Le costanti di stringa sono racchiuse tra virgolette: ad esempio, "Contoso" (Nota: è necessario usare le virgolette semplici "", non quelle non inglesi “”)
* Valori numerici sono espressi senza virgolette e toobe previsto decimale. Ai valori esadecimali viene aggiunto un prefisso di tipo &H. Ad esempio, 98052, &HFF
* I valori booleani sono espressi con costanti: True, False.
* Le costanti predefinite sono espresse solo tramite il relativo nome: NULL, CRLF, IgnoreThisFlow

### <a name="functions"></a>Funzioni
Provisioning dichiarativo utilizza molte funzioni tooenable hello possibilità tootransform valori di attributo. Queste funzioni possono essere annidate in modo hello risultato di una funzione viene passato nella funzione tooanother.

`Function1(Function2(Function3()))`

elenco completo di Hello delle funzioni è reperibile in hello [riferimento alla funzione](active-directory-aadconnectsync-functions-reference.md).

### <a name="parameters"></a>parameters
Un parametro è definito da un connettore o da un amministratore tramite PowerShell. I parametri contengono in genere valori diversi da toosystem di sistema, ad esempio nome hello hello hello di utente del dominio si trova. Questi parametri possono essere usati nei flussi degli attributi.

Hello Active Directory Connector fornito hello seguenti parametri per le regole di sincronizzazione in entrata:

| Nome parametro | Commento |
| --- | --- |
| Domain.Netbios |Formato NetBIOS del dominio hello attualmente importato, ad esempio FABRIKAMSALES |
| Domain.FQDN |Formato FQDN del dominio hello attualmente importato, ad esempio sales.fabrikam.com |
| Domain.LDAP |Il formato LDAP del dominio hello attualmente importato, ad esempio DC = vendite, DC = fabrikam, DC = com |
| Forest.Netbios |Formato NetBIOS del nome dell'insieme di strutture hello attualmente importato, ad esempio FABRIKAMCORP |
| Forest.FQDN |Formato FQDN del nome dell'insieme di strutture hello attualmente importato, ad esempio fabrikam.com |
| Forest.LDAP |Il formato LDAP del nome dell'insieme di strutture hello attualmente importato, ad esempio DC = fabrikam, DC = com |

sistema di Hello fornisce hello seguenti parametro, che è usato tooget hello identificatore hello connettore attualmente in esecuzione:  
`Connector.ID`

Di seguito è riportato un esempio che popola il dominio dell'attributo metaverse hello con il nome netbios hello del dominio hello in cui si trova utente hello:  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>Operatori
è possibile utilizzare Hello seguenti operatori:

* **Confronto**: &lt;, &lt;=, &lt;&gt;, =, &gt;, &gt;=
* **Matematici**: +, -, \*, -
* **Stringa**: & (concatenazione)
* **Logici**: &amp;&amp; (AND), || (OR)
* **Ordine di valutazione**: ( )

Gli operatori sono valutato tooright a sinistra e avere hello stessa priorità di valutazione. Vale a dire hello \* (moltiplicatore) non viene valutato prima - (sottrazione). 2\*(5 + 3) è non hello uguale a 2\*5 + 3. Hello parentesi () vengono utilizzati valutazione hello toochange ordine quando rimane tooright ordine di valutazione non è appropriato.

## <a name="multi-valued-attributes"></a>Attributi multivalore
le funzioni Hello possono operare su attributi a valore singolo e multivalore. Per gli attributi multivalore, la funzione hello agisce su ogni valore e applica hello stessa funzione tooevery valore.

ad esempio:  
`Trim([proxyAddresses])`Eseguire l'ottimizzazione Trim di ogni valore nell'attributo proxyAddress hello.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`Per ogni valore con un @-sign, sostituire dominio hello con @contoso.com.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Cercare l'indirizzo SIP hello e rimuoverlo dai valori hello.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su modello di configurazione hello in [Provisioning dichiarativo comprensione](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Vedere come dichiarativa provisioning è usato out-of-box in [informazioni su configurazione predefinita di hello](active-directory-aadconnectsync-understanding-default-configuration.md).
* Vedere come una pratica toomake cambiano con provisioning dichiarativo [toomake toohello una modifica la modalità di configurazione predefinite](active-directory-aadconnectsync-change-the-configuration.md).

**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)

**Argomenti di riferimento**

* [Servizio di sincronizzazione Azure AD Connect: Riferimento alle funzioni](active-directory-aadconnectsync-functions-reference.md)

