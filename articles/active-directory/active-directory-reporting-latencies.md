---
title: Latenze dei report di Azure Active Directory | Microsoft Docs
description: Tempo necessario per la visualizzazione in Azure Active Directory degli eventi dei report
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 346b14f8-d16d-4b07-8211-e6c5eec07062
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 9443a00232420d58dea52ed01f31a4ef964a1620
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-report-latencies"></a>Latenze dei report di Azure Active Directory
*Questo documento fa parte della [guida alla creazione di report in Azure Active Directory](active-directory-reporting-guide.md).*

| Report | Minima | Media | Massima |
| --- | --- | --- | --- |
| **Report sulla sicurezza** | | | |
| Attività di accesso irregolare |2 ore |4 ore |8 ore |
| Accessi da origini sconosciute |2 ore |4 ore |8 ore |
| Accessi dopo più errori |2 ore |4 ore |8 ore |
| Accessi da più aree geografiche |2 ore |4 ore |8 ore |
| Accessi da indirizzi IP con attività sospette |2 ore |4 ore |8 ore |
| Accessi da dispositivi potenzialmente infetti |2 ore |4 ore |8 ore |
| Utenti con anomalie dell'attività di accesso |2 ore |4 ore |8 ore |
| Utenti con credenziali perse |2 ore |4 ore |8 ore |
| Attività di accesso di tutti gli utenti |2 ore |4 ore |8 ore |
| **Report sull'applicazione** | | | |
| Attività di provisioning dell'account |2 ore |4 ore |8 ore |
| Errori di provisioning dell'account |2 ore |4 ore |8 ore |
| Utilizzo applicazioni |2 ore |4 ore |8 ore |
| Stato rollover della password |2 ore |4 ore |8 ore |
| **Report di controllo e sull'attività** | | | |
| Report di controllo |1 minuto |15 minuti |30 minuti |
| Attività di reimpostazione password (Azure AD) |2 ore |4 ore |8 ore |
| Attività di reimpostazione password (Gestione delle identità) |2 ore |4 ore |8 ore |
| Attività di registrazione per la reimpostazione password (Azure AD) |2 ore |4 ore |8 ore |
| Attività di registrazione di reimpostazione della password (Gestione delle identità) |2 ore |4 ore |8 ore |
| Attività dei gruppi self-service (Azure AD) |2 ore |4 ore |8 ore |
| Attività dei gruppi self-service (Gestione delle identità) |2 ore |4 ore |8 ore |
| **Report RMS** | | | |
| Utenti RMS più attivi |2 ore |4 ore |8 ore |
| Utilizzo di RMS |2 ore |4 ore |8 ore |
| Utilizzo dispositivi RMS |2 ore |4 ore |8 ore |
| Utilizzo applicazioni abilitate per RMS |2 ore |4 ore |8 ore |

