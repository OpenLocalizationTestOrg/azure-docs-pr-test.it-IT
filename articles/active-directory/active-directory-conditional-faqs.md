---
title: Active Directory l'accesso condizionale FAQ aaaAzure | Documenti Microsoft
description: Ottenere risposte toofrequently domande frequenti sull'accesso condizionale in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Domande frequenti sull'accesso condizionale di Azure Active Directory

## <a name="which-applications-work-with-conditional-access-policies"></a>Quali applicazioni funzionano con i criteri di accesso condizionale?

Per informazioni sulle applicazioni che usano i criteri di accesso condizionale, vedere [Applicazioni e browser che usano regole di accesso condizionale in Azure Active Directory](active-directory-conditional-access-supported-apps.md).

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>I criteri di accesso condizionale vengono applicati a Collaborazione B2B e agli utenti guest?

I criteri vengono applicati agli utenti di Collaborazione business-to-business (B2B). Tuttavia, in alcuni casi, un utente potrebbe non essere i requisiti dei criteri hello toosatisfy in grado di. È possibile, ad esempio, che l'organizzazione di un utente guest non supporti l'autenticazione a più fattori. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>Un criterio di SharePoint Online anche applica tooOneDrive for Business?

Sì. Un criterio di SharePoint Online tooOneDrive si applica anche per le aziende.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>Perché non è possibile impostare criteri nelle app client, ad esempio Word o Outlook?

I criteri di accesso condizionale impostano i requisiti per l'accesso a un servizio Viene applicato quando si verifica servizio toothat di autenticazione. criteri di Hello non sono impostato direttamente su un'applicazione client. ma vengono applicati quando un client chiama un servizio. Ad esempio, i criteri impostati in SharePoint applicano tooclients chiamata SharePoint. Un criterio impostato su Exchange applica tooOutlook.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>Criteri di accesso condizionale applica tooservice account?

Criteri di accesso condizionale si applicano gli account utente tooall. inclusi gli account utente usati come account del servizio. Spesso, un account del servizio che esegue automatico non è possibile soddisfare i requisiti di hello di criteri di accesso condizionale. È possibile, ad esempio, che sia richiesta l'autenticazione a più fattori. Gli account del servizio possono essere esclusi dai criteri usando le impostazioni di gestione dei criteri di accesso condizionale. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>Sono disponibili API Graph per configurare i criteri di accesso condizionale?

Attualmente no. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>Novità di criteri di esclusione predefiniti hello per le piattaforme di dispositivi non supportate?

Attualmente i criteri di accesso condizionale sono applicati in modo selettivo per gli utenti che usano dispositivi iOS e Android. Le applicazioni su altre piattaforme di dispositivo, per impostazione predefinita, non sono interessate dal criterio di accesso condizionale hello per dispositivi iOS e Android. Un amministratore tenant può scegliere toooverride hello criteri globali toodisallow accesso toousers su piattaforme che non sono supportate.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>Come funzionano i criteri di accesso condizionale per Microsoft Teams?  

Microsoft Teams si basa principalmente su Exchange Online e SharePoint Online per gli scenari di produttività di base, come riunioni, calendari e condivisione di file. Criteri di accesso condizionale impostati per queste App cloud applicano tooMicrosoft team quando un utente accede.

Microsoft Teams è supportato anche separatamente come app cloud nei criteri di accesso condizionale di Azure Active Directory. I criteri di Autorità certificato impostati per un'applicazione cloud applicano tooMicrosoft team quando un utente accede.

I client desktop di Microsoft Teams per Windows e Mac supportano l'autenticazione moderna. L'autenticazione moderna consente l'accesso in base alle applicazioni client di hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office su piattaforme diverse. 
