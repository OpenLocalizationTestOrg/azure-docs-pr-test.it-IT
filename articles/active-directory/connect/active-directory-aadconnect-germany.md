---
title: aaaAzure AD Connect in Germania Cloud Microsoft
description: "Azure AD Connect integra le directory locali con Azure Active Directory. In questo modo tooprovide un'identità comune per le applicazioni di Office 365, Azure e SaaS integrata con Azure AD."
keywords: "Introduzione tooAzure AD Connect, panoramica di Azure AD Connect, che cos'è Azure AD Connect, installare active directory, in Germania, foresta nero"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Azure AD Connect in Microsoft Cloud per la Germania: anteprima pubblica
## <a name="introduction"></a>Introduzione
Azure AD Connect consente la sincronizzazione tra Active Directory locale e Azure Active Directory.
Attualmente, molti degli scenari di hello in [Microsoft Cloud Germania](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) deve essere eseguita dall'operatore hello. Quando si utilizza Microsoft Cloud Germania, è necessario prestare attenzione hello seguenti:

* Hello che seguenti URL deve essere aperta su un server proxy per la sincronizzazione toooccur correttamente:
  
  * *.microsoftonline.de
  * *.windows.net
  * * Elenchi di revoche dei certificati
* Quando si accede nella directory di Azure AD tooyour, è necessario utilizzare un account nel dominio onmicrosoft.de hello.
* Hello seguenti caratteristiche non sono disponibile:
  * Azure AD Connect Health
  * Aggiornamenti automatici
 
## <a name="download"></a>Scaricare
È possibile scaricare Azure AD Connect dal Pannello di hello Azure AD Connect nel portale di hello.  Utilizzare le istruzioni di hello seguito blade di toolocate hello Azure AD Connect.

### <a name="hello-azure-ad-connect-blade"></a>Hello Azure AD Connect pannello
Dopo l'accesso nel portale di Azure toohello, hello seguenti:

1. Passare tooBrowse
2. Selezionare Azure Active Directory
3. Selezionare Azure AD Connect

Verrà visualizzato hello segue:

![Pannello Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

Hello tabella seguente vengono descritte le funzionalità di hello illustrate nel pannello hello.

| Titolo | Descrizione |
| --- | --- |
| STATO SINCRONIZZAZIONE |Indica se la sincronizzazione è abilitata o disabilitata. |
| ULTIMA SINCRONIZZAZIONE |Hello ultima una sincronizzazione completata. |
| DOMINI FEDERATI |Mostra il numero di hello di domini federati attualmente configurato. |

## <a name="installation"></a>Installazione
tooinstall Azure AD Connect, è possibile utilizzare la documentazione di hello [qui](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Funzionalità avanzate e informazioni aggiuntive
Per altre informazioni e indicazioni sulle impostazioni personalizzate o sulle configurazioni avanzate, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).  Questa pagina fornisce informazioni e collegamenti tooadditional indicazioni.

