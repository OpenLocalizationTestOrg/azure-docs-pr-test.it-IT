---
title: Proxy App di Azure AD App nei team aaaAccess | Documenti Microsoft
description: Utilizzare tooaccess Proxy dell'applicazione Azure Active Directory dell'applicazione locale tramite Teams Microsoft.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Accedere alle applicazioni locali tramite Microsoft Teams

Proxy di Active Directory dell'applicazione Azure offre applicazioni single sign-on tooon locale indipendentemente da dove si è e Microsoft Teams semplifica le attività di collaborazione in un'unica posizione. L'integrazione di hello due insieme significa che gli utenti possono essere produttivi con i propri colleghi in qualsiasi situazione. 

Gli utenti possono aggiungere cloud App tootheir team canali [utilizzando schede](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), ma cosa accade se il sito di SharePoint o un strumento di pianificazione tutte utilizzano è ospitato in locale? Proxy dell'applicazione è la soluzione hello. È possibile aggiungere le app pubblicate tramite il Proxy di applicazione tootheir canali utilizzando hello stesso URL esterni, essi utilizzano sempre tooaccess delle App in modalità remota. E perché esegue l'autenticazione tramite Azure Active Directory, hello stesso esperienza single sign-on esegue tramite Proxy dell'applicazione.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Installare il connettore Proxy dell'applicazione hello e pubblicare l'app

Se hai già fatto, [configurare il Proxy di applicazione per il tenant e installare il connettore hello](active-directory-application-proxy-enable.md). quindi [pubblicare l'applicazione locale](application-proxy-publish-azure-portal.md) per l'accesso remoto. Quando si pubblica l'applicazione hello, prendere nota dell'URL esterno hello perché gli utenti finali è necessario che tali informazioni durante l'aggiunta di hello app tooTeams.

Se già App pubblicata ma non memorizza i relativi URL esterni, cercarli in hello [portale di Azure](https://portal.azure.com). Eseguire l'accesso, quindi passare troppo**Azure Active Directory** > **applicazioni aziendali** > **tutte le applicazioni** > selezionare l'app > **Proxy dell'applicazione**.

## <a name="add-your-app-tooteams"></a>Aggiungere il tooTeams app

Dopo avere pubblicato l'applicazione hello mediante il Proxy di applicazione, informare gli utenti che è possibile aggiungere sotto forma di una scheda direttamente i canali del team. Far eseguire questi tre passaggi:

1. Passare toohello team del canale in cui si desidera tooadd questa app e selezionare  **+**  tooadd una scheda.

   ![Selezionare l'opzione per aggiungere una scheda](./media/application-proxy-teams/add-tab.png)

2. Selezionare **sito Web** da opzioni della scheda hello.

   ![Aggiungere un sito Web](./media/application-proxy-teams/website.png)

3. Assegnare un nome di scheda hello e impostare l'URL esterno di hello URL toohello Proxy dell'applicazione. 

   ![Configurare il nome della scheda e l'URL](./media/application-proxy-teams/tab-name-url.png)

Una volta che un membro di un team aggiunge una scheda di hello, viene visualizzato per tutti gli utenti nel canale hello. Tutti gli utenti che dispongono di accesso toohello app ottengono l'accesso single sign-on con credenziali hello che usano per Teams Microsoft. Tutti gli utenti non dispongono di accesso toohello app verranno visualizzata la scheda hello in team, ma vengono bloccati finché non si assegnare loro autorizzazioni toohello locale app e hello Azure versione pubblicata del portale di app hello. 

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come troppo[pubblicare i siti SharePoint locali](application-proxy-enable-remote-access-sharepoint.md) con Proxy dell'applicazione.
- Configurare il toouse app [domini personalizzati](active-directory-application-proxy-custom-domains.md) per i relativi URL esterni. 
