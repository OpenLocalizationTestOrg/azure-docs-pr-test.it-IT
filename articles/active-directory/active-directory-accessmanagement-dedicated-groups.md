---
title: aaaDedicated gruppi in Azure Active Directory | Documenti Microsoft
description: Panoramica del funzionamento dei gruppi dedicati in Azure Active Directory e della loro creazione.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Gruppi dedicati in Azure Active Directory
In Azure Active Directory (Azure AD), funzionalità di gruppi dedicati hello creati e popolati automaticamente l'appartenenza a gruppi di Azure Active Directory predefinito. Non è possibile aggiungere i membri di gruppi dedicati o rimosso utilizzando hello Azure classico portale, cmdlet di Windows PowerShell, o a livello di codice.

> [!NOTE]
> I gruppi dedicati richiedono che venga assegnata una licenza Azure AD Premium a:
>
> * messaggio per l'amministratore che gestisce la regola hello in un gruppo
> * tutti gli utenti che sono selezionati per hello regola toobe un membro del gruppo di hello
>
>

**gruppi tooenable dedicato**

1. In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi aprire la directory dell'organizzazione.
2. Seleziona hello **gruppi** scheda e quindi aprire hello gruppo tooedit.
3. Seleziona hello **configura** scheda e quindi impostare **Abilita gruppi dedicati** troppo**Sì**.

Dopo aver impostato troppo hello abilitazione dei gruppi dedicati passare**Sì**, è possibile abilitare hello directory tooautomatically creare gruppo dedicato di hello tutti gli utenti dall'impostazione hello **"tutti gli utenti" gruppo** opzione troppo**Sì**. Quindi è possibile inoltre modificare il nome di hello di questo gruppo dedicato digitandolo nel hello **nome visualizzato per "All Users" gruppo** campo.

è possibile utilizzare il gruppo di tutti gli utenti Hello tooassign hello stesso autorizzazioni tooall hello utenti della directory. Ad esempio, è possibile concedere tutti gli utenti in tooa di accesso la directory applicazione SaaS per l'assegnazione dell'accesso per tutti gli utenti gruppo dedicato toothis applicazione hello.

gruppo di tutti gli utenti Hello dedicato include tutti gli utenti nella directory di hello, inclusi i guest e gli utenti esterni. Se è necessario un gruppo che consente di escludere gli utenti esterni, quindi questo scopo, è possibile la creazione di un gruppo con una regola dinamica basato su attributi quali seguenti hello:

                (user.userPrincipalName -notContains "#EXT#@")

Per un gruppo che esclude tutti i guest, usare una regola, come illustrato di seguito hello:

                (user.userType -ne "Guest")

toolearn sulla toocreate *avanzate* regole, che può contenere più confronti, per l'appartenenza dinamica ai gruppi, vedere [utilizzando attributi toocreate regole avanzate](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Informazioni su Azure Active Directory](active-directory-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
