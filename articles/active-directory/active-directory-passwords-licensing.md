---
title: 'Licenze: reimpostazione password self-service di Azure AD | Microsoft Docs'
description: Requisiti di licenza per la reimpostazione password self-service di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Requisiti di licenza per la reimpostazione password self-service di Azure AD

Affinché la reimpostazione della Password AD Azure toofunction, si **deve avere almeno una licenza assegnata all'interno dell'organizzazione**. Non si applica sull'esperienza di reimpostazione della password hello di licenza per utente. conformità toomaintain con contratto di licenza Microsoft, è necessario agli utenti di tooany licenze tooassign che usano le funzionalità premium.

* **Solo utenti del cloud** - Office 365 (O365) e SKU a pagamento o Azure AD Basic
* **Utenti cloud** e/o **utenti locali** - Azure AD P1 Premium o Azure AD P2 Premium, Enterprise Mobility + Security (EMS) o Secure Productive Enterprise (SPE)

## <a name="licenses-required-for-password-writeback"></a>Licenze richieste per il writeback delle password

il writeback delle password toouse, è necessario uno dei seguenti licenze assegnate nel tenant di hello.

* Azure AD Premium P1
* Azure AD P2 Premium
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> I piani di licenza autonoma Office 365 **non supportano il writeback delle password** e richiedono una di hello che precede i piani per toowork questa funzionalità.

Informazioni sulle licenze aggiuntive, inclusi i costi di sono reperibili nelle seguenti pagine hello

* [Sito sui prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>Abilitare le licenze per gruppi o per utente

Azure AD supporta ora in base al gruppo di licenza che consente agli amministratori tooassign licenze gruppo tooa bulk di utenti, anziché assegnando loro uno alla volta. [Assegnare, verificare e risolvere i problemi relativi alle licenze](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Alcuni servizi Microsoft non sono disponibili in tutte le posizioni. Prima che può essere assegnata una licenza utente tooa, amministratore hello specificare proprietà "Località di utilizzo" hello utente hello. Assegnazione delle licenze possa essere consentita nell'ambito di utente > profilo > della sezione Impostazioni hello portale di Azure. **Quando si utilizza l'assegnazione del gruppo di licenze, tutti gli utenti senza specificata una località di utilizzo ereditano percorso hello della directory di hello.**

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Domande frequenti**](active-directory-passwords-faq.md) - Come Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR

