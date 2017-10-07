---
title: aaaLearn sulla verifica in due fasi in Azure MFA | Documenti Microsoft
description: "Che cos'è Azure multi-factor Authentication, motivo per cui utilizzare autenticazione a più fattori, informazioni sui client di multi-factor Authentication hello e diversi metodi di hello e le versioni disponibili. "
keywords: "Introduzione tooMFA, panoramica di autenticazione a più fattori, che cos'è mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>Informazioni su Azure Multi-Factor Authentication
Verifica in due passaggi è un metodo di autenticazione che richiede più di un metodo di verifica e aggiunge un secondo livello critico di sicurezza toouser accessi e le transazioni. Funziona richiedendo due o più dei seguenti metodi di verifica hello:

* Un'informazione nota (in genere una password)
* Un oggetto che si possiede (un dispositivo attendibile non facile da duplicare, ad esempio un telefono)
* Una caratteristica fisica dell'utente (biometrica)

<center>![Nome utente e password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificati](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart card virtuale](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nome utente e password](./media/multi-factor-authentication/cert.png)</center>

Azure Multi-Factor Authentication (MFA) è una soluzione di verifica in due passaggi di Microsoft. Azure MFA consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo. Offre autenticazione avanzata tramite una gamma di metodi di verifica, fra cui una telefonata, un SMS o una verifica dell'app per dispositivi mobili.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>Vantaggi dell'uso di Azure Multi-Factor Authentication
Oggi più che mai le persone sono sempre più connesse. Con Smartphone, Tablet, laptop e PC, gli utenti sono disponibili varie opzioni in modalità sta tooconnect e rimanere connessi in qualsiasi momento. Le persone possono accedere ai propri account e alle applicazioni da qualsiasi luogo e questo significa poter svolgere più attività e servire meglio i clienti.

Azure multi-Factor Authentication è un semplice toouse, scalabile e soluzione affidabile che offre un secondo metodo di autenticazione in modo gli utenti sono sempre protetti.

| ![TooUse semplice](./media/multi-factor-authentication/simple.png) | ![Scalabile](./media/multi-factor-authentication/scalable.png) | ![Sempre protetti](./media/multi-factor-authentication/protected.png) | ![Affidabile](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Toouse semplice** |**Scalabile** |**Sempre protetti** |**Affidabile** |

* **Facile tooUse** -Azure multi-Factor Authentication è semplice tooset backup e usare. Hello protezione aggiuntiva fornita con Azure multi-Factor Authentication consente agli utenti toomanage i propri dispositivi. L'aspetto più importante è che in molti casi può essere configurata con pochi semplici clic.
* **Scalabile** -Azure multi-Factor Authentication Usa power hello del cloud hello e si integra con locale Active Directory e le applicazioni personalizzate. Questa protezione viene estesa anche tooyour scenari di volumi elevati di importanza critica.
* **Sempre protetti** -Azure multi-Factor Authentication fornisce autenticazione avanzata mediante massimi standard del settore di hello.
* **Affidabile** : la disponibilità di Azure Multi-Factor Authentication è garantita al 99,9%. Hello servizio verrà considerato non disponibile quando è in grado di richieste di verifica tooreceive o un processo di verifica in due passaggi hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Passaggi successivi

- Informazioni su [come funziona Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)

- Informazioni sulle diversa hello [versioni e i metodi di utilizzo per Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md)
