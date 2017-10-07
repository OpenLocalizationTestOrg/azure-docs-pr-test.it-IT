---
title: 'Azure Active Directory Domain Services: abilitare la delega vincolata Kerberos | Documentazione Microsoft'
description: Abilitare la delega vincolata Kerberos in domini gestiti di Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Configurare la delega vincolata Kerberos (KCD) in un dominio gestito
Molte applicazioni necessitano risorse di tooaccess nel contesto di hello dell'utente hello. Active Directory supporta un meccanismo denominato delega Kerberos che consente questo caso d'uso. Inoltre, è possibile limitare la delega in modo che solo le risorse specifiche accessibili nel contesto di hello dell'utente hello. I domini gestiti di Azure AD Domain Services sono diversi dai domini di Active Directory tradizionali perché sono bloccati in modo più sicuro.

Questo articolo illustra come tooconfigure kerberos vincolata delega in un dominio gestito di servizi di dominio Active Directory di Azure.

## <a name="kerberos-constrained-delegation-kcd"></a>Delega vincolata Kerberos (KCD)
La delega Kerberos consente un tooimpersonate account le risorse di un altro sicurezza tooaccess principale (ad esempio un utente). Si consideri un'applicazione web che accede a un'API web back-end nel contesto di hello di un utente. In questo esempio hello applicazione web (in esecuzione nel contesto di hello di un account del servizio o un account del computer o computer) rappresenta hello utente quando si accede a risorse hello (back-end web API). Poiché non limita hello hello risorse rappresentazione account accessibile nel contesto di hello di hello utente, la delega Kerberos non è protetta.

La delega vincolata Kerberos (KCD) limita hello/risorse dei servizi toowhich hello specificato server possono operare per conto di hello di un utente. La delega vincolata Kerberos tradizionali richiede tooconfigure privilegi di amministratore dominio un account di dominio per un servizio e limita singolo dominio tooa account hello.

Alla delega vincolata Kerberos tradizionale sono anche associati alcuni problemi. Nei sistemi operativi precedenti in amministratore di dominio hello configurato il servizio di hello, amministratore del servizio hello non dispone di alcun tooknow un modo utile per i servizi front-end delegato servizi risorsa toohello che loro proprietà. E qualsiasi servizio front-end che può delegare tooa servizio relativo alle risorse rappresenta un potenziale punto di attacco. È stato compromesso un server che ospita un servizio front-end, se è stato configurato toodelegate tooresource services, servizi di risorse hello inoltre potrebbe essere compromessa.

> [!NOTE]
> In un dominio gestito di Azure AD Domain Services non si hanno privilegi di amministratore di dominio. Di conseguenza, **non è possibile configurare la delega vincolata Kerberos tradizionale in un dominio gestito**. Usare la delega vincolata Kerberos basata su risorse, come illustrato in questo articolo. Questo meccanismo è anche più sicuro.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>Delega vincolata Kerberos basata sulle risorse
In Windows Server 2012 R2 e Windows Server 2012, la delega vincolata tooconfigure possibilità hello per servizio hello è stata trasferita dall'amministratore del servizio toohello hello dominio amministratore. In questo modo, amministratore del servizio back-end hello può consentire o negare i servizi front-end. Questo modello è noto come **delega vincolata Kerberos basata sulle risorse**.

È possibile configurare la delega vincolata Kerberos basata sulle risorse usando PowerShell. Utilizzare Set-ADComputer hello o i cmdlet Set-ADUser, a seconda che hello rappresenta l'account sia un account computer o un account di servizio o account utente.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>Configurare la delega vincolata Kerberos basata sulle risorse per un account del computer in un dominio gestito
Si supponga di avere un'app web in esecuzione nel computer di hello ' contoso100-webapp.contoso100.com'. È necessario risorse hello tooaccess (un'API web in esecuzione in ' contoso100-api.contoso100.com') nel contesto di hello utenti del dominio. Di seguito viene illustrato come impostare la delega vincolata Kerberos basata su risorse per questo scenario.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>Configurare la delega vincolata Kerberos basata sulle risorse per un account utente in un dominio gestito
Si supponga che un'App web in esecuzione come account del servizio 'appsvc' e deve risorse hello tooaccess (un'API web in esecuzione come account del servizio - 'backendsvc') nel contesto di hello utenti del dominio. Di seguito viene illustrato come impostare la delega vincolata Kerberos basata su risorse per questo scenario.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Panoramica della delega vincolata Kerberos](https://technet.microsoft.com/library/jj553400.aspx)
