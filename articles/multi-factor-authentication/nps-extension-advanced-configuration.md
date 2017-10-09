---
title: hello aaaConfigure estensione dei criteri di rete di Azure MFA | Documenti Microsoft
description: "Dopo aver installato l'estensione dei criteri di rete hello, è possibile usare questi passaggi per la configurazione avanzata come whitelist IP e la sostituzione di UPN."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>Configurazione opzioni avanzate per hello estensione dei criteri di rete multi-Factor Authentication

Hello estensione dei criteri di rete Server () estende le funzionalità di Azure multi-Factor Authentication basato sul cloud nell'infrastruttura locale. Questo articolo si presuppone che si dispone già di estensione hello installato e si decide tooknow come estensione hello toocustomize è necessario. 

## <a name="alternate-login-id"></a>ID di accesso alternativo

Poiché l'estensione dei criteri di rete hello collega tooboth locale e cloud directory, si potrebbe riscontrare un problema in cui i nomi dell'entità utente locale (UPN) non corrispondono nomi hello nel cloud hello. toosolve questo problema, l'uso ID di accesso alternativo. 

All'interno di hello estensione dei criteri di rete, è possibile designare un toobe di attributi di Active Directory utilizzato al posto di hello UPN per Azure multi-Factor Authentication. In questo modo si tooprotect le risorse locali con la verifica senza modificare i nomi UPN locale. 

account di accesso alternativo tooconfigure ID, andare troppo`HKLM\SOFTWARE\Microsoft\AzureMfa` e modificare hello valori del Registro di sistema seguente:

| Nome | Tipo | Valore predefinito | Descrizione |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | string | Empty | Definire nome hello dell'attributo di Active Directory che si desidera toouse anziché hello UPN. Questo attributo viene utilizzato come attributo AlternateLoginId hello. Se questo valore del Registro di sistema è impostato tooa [attributo di Active Directory valido](https://msdn.microsoft.com/library/ms675090.aspx) (ad esempio, posta elettronica o displayName), quindi hello valore dell'attributo è usato al posto UPN dell'utente hello per l'autenticazione. Se questo valore del Registro di sistema è vuoto o non configurato, quindi AlternateLoginId è disabilitata e UPN dell'utente hello viene utilizzato per l'autenticazione. |
| LDAP_FORCE_GLOBAL_CATALOG | boolean | False | Utilizzare questo flag tooforce hello di catalogo globale per le ricerche LDAP per la ricerca di AlternateLoginId. Configurare un controller di dominio come catalogo globale, aggiungere hello AlternateLoginId attributo toohello catalogo globale e quindi abilitare questo flag. <br><br> Se è stato configurato (non vuoto), LDAP_LOOKUP_FORESTS **questo flag viene applicato come true**, indipendentemente dal valore di hello dell'impostazione del Registro di sistema di hello. In questo caso, hello estensione dei criteri di rete richiede toobe di catalogo globale hello configurato con l'attributo AlternateLoginId hello per ogni foresta. |
| LDAP_LOOKUP_FORESTS | string | Empty | Specificare un elenco separato da punto e virgola di foreste toosearch. Ad esempio, *contoso.com;foobar.com*. Se questo valore del Registro di sistema è configurato, hello estensione dei criteri di rete in modo iterativo Cerca tutte le foreste hello in ordine di hello in cui sono elencate e restituisce il valore di AlternateLoginId di hello primo ha esito positivo. Se questo valore del Registro di sistema non è configurato, ricerca AlternateLoginId hello è toohello ristretto di dominio corrente.|

tootroubleshoot problemi con l'account di accesso alternativo ID, utilizzare hello indicata le procedure per [errori di ID di accesso alternativo](multi-factor-authentication-nps-errors.md#alternate-login-id-errors).

## <a name="ip-exceptions"></a>Eccezioni IP

Se è necessario toomonitor disponibilità del server, ad esempio se i servizi di bilanciamento del carico verificare quali server sono in esecuzione prima di inviare i carichi di lavoro, non si desidera toobe questi controlli bloccata da richieste di verifica. Creare quindi un elenco di indirizzi IP sicuramente usati dagli account del servizio e disattivare i requisiti di Multi-Factor Authentication per tale elenco. 

tooconfigure una whitelist IP, andare troppo`HKLM\SOFTWARE\Microsoft\AzureMfa` e configurare hello il valore del Registro di sistema seguente: 

| Nome | Tipo | Valore predefinito | Descrizione |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | string | Empty | Specificare un elenco separato da punti e virgola degli indirizzi IP. Includere gli indirizzi IP hello dei computer in cui hanno origine le richieste di servizio, ad esempio hello server NAS/VPN. Gli intervalli IP di subnet non sono supportati. <br><br> Ad esempio: *10.0.0.1;10.0.0.2;10.0.0.3*.

Quando arriva una richiesta da un indirizzo IP presente nell'elenco elementi consentiti hello, verifica in due passaggi viene ignorata. whitelist IP Hello è indirizzo IP toohello confrontati fornito in hello *ratNASIPAddress* attributi della richiesta RADIUS hello. Se arriva una richiesta RADIUS senza attributo ratNASIPAddress hello, viene registrato hello seguente avviso: "Whitelist P_WHITE_LIST_WARNING::IP verrà ignorato perché non è presente nella richiesta RADIUS nell'attributo NasIpAddress IP di origine."

## <a name="next-steps"></a>Passaggi successivi

[Risolvere i messaggi di errore di hello estensione dei criteri di rete per Azure multi-Factor Authentication](multi-factor-authentication-nps-errors.md)
