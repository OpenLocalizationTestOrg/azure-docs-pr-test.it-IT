---
title: "aaaFederating più Azure AD con ADFS single | Documenti Microsoft"
description: "In questo documento si apprenderà come toofederate più Azure AD con una singola istanza di ADFS."
keywords: "eseguire la federazione, ADFS, AD FS, più tenant, singola istanza di AD FS, unica istanza di AD FS, federazione multi-tenant, ad fs con più foreste, aad connect, federazione, federazione tra tenant"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Eseguire la federazione di più istanze di Azure AD con una singola istanza di AD FS

In una singola farm AD FS a disponibilità elevata è possibile eseguire la federazione di più foreste, se tra di esse esiste un trust bidirezionale. Più foreste può o potrebbe non corrispondere toohello stesso Azure Active Directory. In questo articolo vengono fornite istruzioni su come tooconfigure federazione tra un'unica distribuzione di ADFS e più foreste che toodifferent di sincronizzazione Azure AD.

![Federazione multi-tenant con una singola istanza di AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> Il writeback dei dispositivi e l'aggiunta automatica di dispositivi non sono supportati in questo scenario.

> [!NOTE]
> Azure AD Connect non può essere federazione tooconfigure utilizzati in questo scenario, poiché Azure AD Connect è possibile configurare la federazione per i domini in una singola AD Azure.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>Procedura per la federazione di AD FS con più istanze di Azure AD

Si consideri che un dominio contoso.com in Azure Active Directory contoso.onmicrosoft.com già è federato con ADFS hello locale installati nell'ambiente di Active Directory locale di contoso.com. e che Fabrikam.com sia un dominio nell'istanza di Azure Active Directory fabrikam.onmicrosoft.com.

##<a name="step-1-establish-a-two-way-trust"></a>Passaggio 1: Stabilire un trust bidirezionale
 
Per ADFS in contoso.com toobe tooauthenticate in grado di utenti in fabrikam.com, è necessario un trust bidirezionale tra contoso.com e fabrikam.com. Seguire la linea guida hello in questo [articolo](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello trust bidirezionale.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>Passaggio 2: Modificare le impostazioni di federazione di contoso.com 
 
Hello autorità di certificazione predefinita impostata per tooAD un singolo dominio federato ADFS è "http://ADFSServiceFQDN/adfs/services/trust", ad esempio, "http://fs.contoso.com/adfs/services/trust". Azure Active Directory richiede un'autorità di certificazione univoca per ogni dominio federato. Poiché hello stesso AD FS sta toofederate due domini, il valore di autorità di certificazione hello deve toobe modificato in modo che sia univoco per ogni dominio che ADFS la federazione con Azure Active Directory. 
 
Nel server AD FS hello, aprire Azure AD PowerShell ed eseguire hello alla procedura seguente:
 
Connettersi toohello Azure Active Directory che contiene hello dominio contoso.com Connect-MsolService aggiornamento hello impostazioni della federazione per contoso.com Update-MsolFederatedDomain - DomainName contoso.com-SupportMultipleDomain
 
Autorità emittente di impostazioni di federazione del dominio hello verrà modificato troppo "http://contoso.com/adfs/services/trust" un rilascio di attestazioni e regola sarà aggiunta per hello Azure AD Trust della Relying Party tooissue hello corretto valore issuerId in base al suffisso UPN hello.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>Passaggio 3: Eseguire la federazione di fabrikam.com con AD FS
 
Sessione di powershell di Azure AD eseguire l'hello alla procedura seguente: connessione tooAzure Active Directory che contiene hello dominio fabrikam.com

    Connect-MsolService
Convertire toofederated di dominio fabrikam.com gestiti hello:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Hello sopra operazione effettuerà la federazione hello dominio fabrikam.com con hello stesso AD FS. È possibile verificare le impostazioni del dominio hello utilizzando Get-MsolDomainFederationSettings per entrambi i domini.

## <a name="next-steps"></a>Passaggi successivi
[Connettere Active Directory ad Azure Active Directory](active-directory-aadconnect.md)
