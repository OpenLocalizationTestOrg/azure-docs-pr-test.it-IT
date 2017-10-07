---
title: aaaUsing un tooSaaS di accesso di gruppo toomanage applicazioni | Documenti Microsoft
description: Come toouse gruppi in Azure Active Directory Premium o Basic tooassign accedere tooSaaS applicazioni integrate con Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>Utilizzo di applicazioni di tooSaaS un gruppo toomanage accesso
Azure Active Directory (Azure AD) con una licenza Azure AD Premium o Azure AD Basic, è possibile utilizzare gruppi tooassign accesso tooa applicazione SaaS integrata con Azure AD. Ad esempio, se si desidera accedere tooassign per hello marketing reparto toouse cinque applicazioni SaaS diverse, è possibile creare un gruppo che contiene gli utenti di hello reparto marketing hello e quindi assegnare tale gruppo toothese cinque applicazioni SaaS che sono richiesta in base al reparto marketing hello. In questo modo è possibile risparmiare tempo mediante la gestione di appartenenza hello di hello marketing reparto in un'unica posizione. Gli utenti quindi assegnati toohello applicazione quando vengono aggiunti come membri del gruppo marketing hello e sono le relative assegnazioni rimosse da un'applicazione hello quando vengono rimossi dal gruppo marketing hello.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. 

Questa funzionalità è utilizzabile con centinaia di applicazioni che è possibile aggiungere all'interno di hello raccolta di applicazioni Azure AD.

**accesso tooassign per un'applicazione SaaS di tooa gruppo**

1. In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory** sulla barra di spostamento hello sul lato sinistro hello.
2. Seleziona hello **Directory** scheda e quindi aprire hello directory in cui si desidera l'accesso tooassign per un'applicazione SaaS di tooa gruppo.
3. Seleziona hello **applicazioni** scheda. Selezionare un'applicazione aggiunta dalla raccolta di applicazioni hello e quindi fare clic su hello **utenti e gruppi** scheda.
4. In hello **utenti e gruppi** scheda hello **a partire da** immettere nome hello di hello gruppo toowhich si desidera tooassign accesso e quindi selezionare hello segno di spunta in alto a destra hello. È necessario solo la prima parte hello tootype del nome di un gruppo.
5. Selezionare il gruppo di hello, quindi scegliere hello **assegna accesso** pulsante. Selezionare **Sì** quando viene visualizzato il messaggio di conferma hello. Appartenenze a gruppi nidificati non sono supportate per l'assegnazione basata su gruppo tooapplications in questo momento.
6. È inoltre possibile visualizzare quali utenti vengono assegnati applicazione toohello, direttamente o tramite l'appartenenza a un gruppo. toodo hello, questa modifica **Mostra l'elenco a discesa da "Gruppi"** troppo**'Tutti gli utenti'**. Hello sono elencati gli utenti nella directory di hello e se ogni utente è assegnato toohello applicazione. elenco di Hello Mostra anche se gli utenti assegnato hello assegnati direttamente applicazione toohello (tipo di assegnazione visualizzato come "Diretta") oppure in base l'appartenenza al gruppo (tipo di assegnazione visualizzato come "Ereditata")

> [!NOTE]
> È possibile visualizzare scheda gruppi e utenti hello solo dopo avere abilitato Azure AD Premium o Azure AD Basic.
>
>

### <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Informazioni su Azure Active Directory](active-directory-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
