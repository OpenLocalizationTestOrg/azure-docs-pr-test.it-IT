---
title: "Anteprima di gestione aaaAdministrative unità in Azure Active Directory"
description: "Utilizzo delle unità amministrative per la delega più granulare delle autorizzazioni in Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Gestione delle unità amministrative in Azure AD - Anteprima pubblica
In questo articolo viene descritto come unità amministrative, un nuovo contenitore di Azure Active Directory delle risorse che può essere usato per delegare le autorizzazioni amministrative a subset di utenti e applicare criteri tooa sottoinsieme gli utenti. In Azure Active Directory, le unità amministrative consentono agli amministratori degli amministratori centrali toodelegate autorizzazioni tooregional o tooset criteri a un livello granulare.

Ciò risulta utile nelle organizzazioni con divisioni indipendenti, ad esempio, una grande università è costituita da molte scuole autonome (facoltà di gestione aziendale, facoltà di ingegneria, ecc.) indipendenti tra loro. Tali divisioni dispongono dei propri amministratori IT che controllano l'accesso, gestiscono gli utenti e impostano i criteri in modo specifico per la propria facoltà. Gli amministratori centrali desidera toobe in grado di concedere queste autorizzazioni amministrative agli amministratori utenti hello nelle proprie divisioni. In particolare, utilizzando questo esempio, un amministratore centrale può, ad esempio, creare un'unità amministrativa per un particolare reparto (economia) e popolarla con solo hello dell'istituto di istruzione gli utenti di Business. Un amministratore centrale può aggiungere economia hello ruolo tooa con ambito di personale IT, in altre parole, concedere hello personale IT di economia autorizzazioni amministrative solo su hello unità amministrativa di economia.

> [!IMPORTANT]
> È possibile assegnare ruoli di amministratore con ambito unità amministrativa solo se si abilita Azure Active Directory Premium. Per altre informazioni, vedere [Introduzione a Azure AD Premium](active-directory-get-started-premium.md).
>


Dal punto di vista dell'amministratore centrale hello, un'unità amministrativa è un oggetto directory che può essere creato e popolato con le risorse. **In questa versione di anteprima, queste risorse possono essere solo gli utenti.** Una volta creata e popolata, è possibile utilizzare l'unità amministrativa hello come un hello toorestrict ambito concesso l'autorizzazione solo su risorse contenute nell'unità amministrativa hello.

## <a name="managing-administrative-units"></a>Gestione delle unità amministrative
In questa versione di anteprima, è possibile creare e gestire le unità amministrative utilizzando i cmdlet di hello modulo di Azure Active Directory per Windows PowerShell. altre informazioni su come toolearn toodo che, vedere [utilizzano unità amministrative](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Per ulteriori informazioni sui requisiti software e l'installazione modulo hello Azure AD e per informazioni su hello cmdlet del modulo di Azure AD per la gestione delle unità amministrative, inclusi la sintassi, le descrizioni dei parametri ed esempi, vedere [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Passaggi successivi
[Edizioni di Azure Active Directory](active-directory-editions.md)
