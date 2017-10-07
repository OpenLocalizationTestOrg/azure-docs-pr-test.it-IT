---
title: attributi di shadow del servizio di sincronizzazione di aaaAzure AD Connect | Documenti Microsoft
description: Descrive il funzionamento degli attributi shadow con il servizio di sincronizzazione Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Attributi shadow del servizio di sincronizzazione Azure AD Connect
La maggior parte degli attributi sono rappresentati stesso hello in Azure AD come se fossero in Active Directory locale. Ma alcuni attributi hanno alcune una gestione speciale e il valore dell'attributo hello in Azure AD può essere diverso rispetto a ciò che esegue la sincronizzazione Azure AD Connect.

## <a name="introducing-shadow-attributes"></a>Introduzione agli attributi shadow
Alcuni attributi hanno due rappresentazioni in Azure AD. Valore locale hello sia un valore calcolato vengono archiviati. Questi attributi aggiuntivi sono chiamati attributi shadow. Hello due attributi più comuni in cui si verifica questo problema sono **userPrincipalName** e **proxyAddress**. modifica di Hello nei valori di attributo si verifica quando sono presenti valori in questi attributi che rappresentano i domini non verificati. Tuttavia, il motore di sincronizzazione hello in Connect legge hello valore nell'attributo shadow hello scopo dal relativo punto di vista, attributo hello è stata confermata da Azure AD.

È possibile visualizzare gli attributi di ombreggiatura hello utilizzando hello portale di Azure o con PowerShell. Ma il concetto di hello comprensione aiuta si tootroubleshoot determinati scenari dove hello presenta valori diversi in locale e nel cloud hello.

toobetter comprendere il comportamento di hello, esaminare questo esempio da Fabrikam:  
![Domini](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
Includono più suffissi UPN nel servizio Active Directory locale, ma ne è stato verificato solo uno.

### <a name="userprincipalname"></a>userPrincipalName
Un utente dispone di hello seguenti valori di attributo in un dominio non verificato:

| Attributo | Valore |
| --- | --- |
| userPrincipalName locale | lee.sperry@fabrikam.com |
| shadowUserPrincipalName in Azure AD | lee.sperry@fabrikam.com |
| userPrincipalName in Azure AD | lee.sperry@fabrikam.onmicrosoft.com |

attributo userPrincipalName Hello è il valore di hello che viene visualizzato quando l'utilizzo di PowerShell.

Poiché il valore dell'attributo hello reale locale viene archiviato in Azure AD, quando si verifica dominio fabrikam.com hello, Azure Active Directory Aggiorna attributo userPrincipalName hello con valore hello shadowUserPrincipalName hello. Non si dispone toosynchronize tutte le modifiche da Azure AD Connect per toobe questi valori aggiornati.

### <a name="proxyaddresses"></a>proxyAddresses
Hello stesso processo per includere solo i domini verificati si verifica anche proxyAddresses, ma con una logica aggiuntiva. controllo Hello per domini verificati avviene solo per gli utenti delle cassette postali. Un utente abilitato alla posta elettronica o un contatto rappresentano un utente in un'altra organizzazione di Exchange ed è possibile aggiungere tutti i valori negli oggetti toothese proxyAddresses.

Per un utente della cassetta postale, in locale o in Exchange Online, vengono visualizzati solo i valori per i domini verificati. L'aspetto è simile al seguente:

| Attributo | Valore |
| --- | --- |
| proxyAddresses locale | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| proxyAddresses in Exchange Online | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

In questo caso **smtp:abbie.spencer@fabrikam.com** è stato rimosso poiché tale dominio non è stato verificato. Ma Exchange ha aggiunto anche **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam non ha usato Lync/Skype in locale, ma Azure AD ed Exchange Online sono in fase di preparazione.

Questa logica per proxyAddresses è tooas cui **ProxyCalc**. ProxyCalc viene richiamato con ogni modifica a un utente quando:

- utente Hello è stato assegnato un piano di servizio che include Exchange Online, anche se l'utente hello non è stato concesso in licenza per Exchange. Ad esempio, se hello utente è assegnato hello SKU di Office E3, ma è stata assegnata solo SharePoint Online. Questo vale anche se la cassetta postale dell'utente è ancora in locale.
- Hello msExchRecipientTypeDetails di attributo ha un valore.
- Rendere un tooproxyAddresses modifica userPrincipalName.

ProxyCalc potrebbe richiedere una modifica di alcune tooprocess tempo su un utente e non è sincrono con processo di esportazione hello Azure AD Connect.

> [!NOTE]
> Hello ProxyCalc logica presenta alcuni comportamenti aggiuntivi per scenari avanzati non documentati in questo argomento. In questo argomento viene fornita automaticamente toounderstand hello comportamento e non tutta la logica interna del documento.

### <a name="quarantined-attribute-values"></a>Valori di attributo in quarantena
Gli attributi shadow vengono usati anche quando sono presenti valori di attributo duplicati. Per altre informazioni, vedere [Resilienza degli attributi duplicati](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="see-also"></a>Vedere anche
* [Servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
