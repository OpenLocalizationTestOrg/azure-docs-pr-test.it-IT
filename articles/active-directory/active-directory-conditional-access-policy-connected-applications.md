---
title: criteri di accesso condizionale basato su dispositivo di Azure Active Directory aaaConfigure | Documenti Microsoft
description: Informazioni su come criteri di accesso condizionale basato su dispositivi di tooconfigure Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Configurare i criteri di accesso condizionale basato su dispositivo di Azure Active Directory

Con l'[accesso condizionale di Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), è possibile ottimizzare la modalità in cui gli utenti autorizzati possono accedere alle risorse. Ad esempio, si limita hello accedere toocertain risorse tootrusted ai dispositivi. Un criterio di accesso condizionale che richiede un dispositivo attendibile è noto anche come criterio di accesso condizionale basato su dispositivo.

In questo argomento fornisce informazioni su come criteri per le applicazioni connessi AD Azure di accesso condizionale basato su dispositivi tooconfigure. 


## <a name="before-you-begin"></a>Prima di iniziare

L'accesso condizionale basato su dispositivo lega l'**accesso condizionale di Azure AD** e la **gestione dei dispositivi di Azure AD**. Se non si ha familiarità con una di queste aree, è consigliabile leggere i seguenti argomenti, innanzitutto hello:

- **[Accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -questo argomento offre una panoramica concettuale di condizionale accedere e hello la terminologia correlata.

- **[Gestione toodevice introduzione in Azure Active Directory](device-management-introduction.md)**  -questo argomento viene fornita una panoramica di hello varie opzioni sono tooconnect dispositivi con Azure AD. 


## <a name="trusted-devices"></a>Dispositivi attendibili

In un ambiente mobile-first, prima di cloud, Azure Active Directory consente di single sign-on toodevices, applicazioni e servizi da qualsiasi posizione. Per alcune risorse nel proprio ambiente, concessione dell'accesso di utenti appropriati toohello potrebbero non essere sufficiente. Inoltre toohello utenti appropriati, si potrebbero anche richiedere che un toobe attendibile di dispositivo utilizzato tooaccess una risorsa. Nell'ambiente in uso, è possibile definire un dispositivo attendibile ciò che si basa su hello seguenti componenti:

- Hello [piattaforme per dispositivi](active-directory-conditional-access-azure-portal.md#device-platforms) in un dispositivo
- Se un dispositivo è conforme
- Se un dispositivo è aggiunto al dominio 

Hello [piattaforme per dispositivi](active-directory-conditional-access-azure-portal.md#device-platforms) è caratterizzato dal sistema operativo hello che è in esecuzione sul dispositivo. Nei criteri di accesso condizionale basato su dispositivo, è possibile limitare l'accesso toocertain toospecific risorse piattaforme del dispositivo.



In un criterio di accesso condizionale basato su dispositivo, è possibile richiedere toobe dispositivi attendibili segnato come conforme.

![App cloud](./media/active-directory-conditional-access-policy-connected-applications/24.png)

I dispositivi possono essere contrassegnati come conformi nella directory hello da:

- Intune 
- Un sistema di gestione di dispositivi mobili di terze parti che si integra con Azure AD  

Solo i dispositivi che sono connessi tooAzure Active Directory possono essere contrassegnati come conformi. tooconnect tooAzure un dispositivo Active Directory, è necessario hello le opzioni seguenti: 

- Registrazione in Azure AD
- Aggiunta ad Azure AD
- Aggiunta all'identità ibrida di Azure AD

    ![App cloud](./media/active-directory-conditional-access-policy-connected-applications/26.png)

Se si dispone di un footprint di Active Directory (AD) locale, è possibile i dispositivi che non sono connessi tooAzure AD ma toobe tooyour aggiunti a un Active Directory trusted.

![App cloud](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>Passaggi successivi

Prima di configurare un criterio di accesso condizionale basato su dispositivi nell'ambiente in uso, è consigliabile dare un'occhiata hello [procedure consigliate per l'accesso condizionale in Azure Active Directory](active-directory-conditional-access-best-practices.md).

