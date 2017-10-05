---
title: Accedere alle app del proxy app di Azure AD in Teams | Microsoft Docs
description: Usare il proxy applicazione di Azure AD per accedere all'applicazione locale tramite Microsoft Teams.
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
ms.openlocfilehash: 24e22d7314de536714a825cd7035d2cec2112278
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Accedere alle applicazioni locali tramite Microsoft Teams

Il proxy applicazione di Azure Active Directory consente l'accesso Single Sign-On alle applicazioni locali ovunque ci si trovi e Microsoft Teams ottimizza le attività di collaborazione in un'unica posizione. Integrandoli, gli utenti e possono collaborare in modo produttivo con i colleghi in ogni situazione. 

Gli utenti possono aggiungere le app per cloud ai canali di Teams [usando le schede](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), ma, nel caso in cui un sito di SharePoint o uno strumento di pianificazione usato da tutti sia ospitato in locale, il proxy di applicazione è la soluzione ideale. Gli utenti possono aggiungere ai canali le app pubblicate tramite il proxy di applicazione usando gli stessi URL esterni che usano sempre per accedere alle app in remoto e, poiché il proxy di applicazione esegue l'autenticazione tramite Azure Active Directory, viene effettuato lo stesso accesso Single Sign-On.


## <a name="install-the-application-proxy-connector-and-publish-your-app"></a>Installare il connettore proxy applicazione e pubblicare l'app

Se necessario, [configurare il proxy di applicazione per il tenant e installare il connettore](active-directory-application-proxy-enable.md), quindi [pubblicare l'applicazione locale](application-proxy-publish-azure-portal.md) per l'accesso remoto. Quando si pubblica l'app, prendere nota dell'URL esterno perché gli utenti finali hanno bisogno di questa informazione quando aggiungono l'app a Teams.

Se le app sono già state pubblicate, ma non si ricordano gli URL esterni, cercarli nel [portale di Azure](https://portal.azure.com). Eseguire l'accesso, quindi passare ad **Azure Active Directory** > **Applicazioni aziendali** > **Tutte le applicazioni** > selezionare l'app > **Proxy dell'applicazione**.

## <a name="add-your-app-to-teams"></a>Aggiungere l'app a Teams

Dopo avere pubblicato l'app tramite il proxy di applicazione, informare gli utenti che possono aggiungerla come scheda direttamente nei canali di Teams. Far eseguire questi tre passaggi:

1. Passare al canale di Teams in cui si vuole aggiungere questa app e selezionare **+** per aggiungere una scheda.

   ![Selezionare l'opzione per aggiungere una scheda](./media/application-proxy-teams/add-tab.png)

2. Selezionare **Sito Web** dalle opzioni della scheda.

   ![Aggiungere un sito Web](./media/application-proxy-teams/website.png)

3. Assegnare un nome alla scheda e impostare l'URL su quello esterno del proxy applicazione. 

   ![Configurare il nome della scheda e l'URL](./media/application-proxy-teams/tab-name-url.png)

La scheda, dopo che è stata aggiunta da un membro di un team, viene visualizzata da tutti nel canale. Tutti gli utenti che hanno accesso all'app ottengono l'accesso Single Sign-On con le credenziali usate per Microsoft Teams. Gli utenti che non hanno accesso all'app visualizzeranno la scheda in Teams, ma saranno bloccati finché non verranno concesse le autorizzazioni per l'app locale e la versione pubblicata nel portale di Azure dell'app. 

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come [pubblicare siti di SharePoint locali](application-proxy-enable-remote-access-sharepoint.md) con il proxy di applicazione.
- Configurare le app per usare i [domini personalizzati](active-directory-application-proxy-custom-domains.md) per l'URL esterno. 
