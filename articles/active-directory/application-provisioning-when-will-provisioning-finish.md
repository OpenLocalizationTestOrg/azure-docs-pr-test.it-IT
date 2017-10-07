---
title: "aaaUser provisioning applicazione raccolta tooan Azure AD è tenuto ore o più | Documenti Microsoft"
description: "Come toofind il motivo per cui effettuare il provisioning tooyour applicazione potrebbe essere richiede più tempo del previsto"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>Provisioning dell'applicazione raccolta tooan Azure AD dell'utente è tenuto ore o più

Quando si abilita innanzitutto il provisioning automatico di un'applicazione, la sincronizzazione iniziale hello può richiedere ore tooseveral 20 minuti, a seconda delle dimensioni di hello della directory di Azure AD hello e il numero di hello di utenti nell'ambito per il provisioning. 

Le sincronizzazioni successive dopo la sincronizzazione iniziale di hello risultare più veloce, come hello provisioning servizio archivia le soglie che rappresentano lo stato di hello di entrambi i sistemi dopo la sincronizzazione iniziale hello, migliorando le prestazioni di sincronizzazioni successive.

## <a name="how-tooimprove-provisioning-performance"></a>Come tooimprove provisioning delle prestazioni

Se la sincronizzazione iniziale hello richiede più di qualche ora, c'è una cosa è possibile eseguire tooimprove prestazioni:

-   **Filtri di ambito utente** I filtri di ambito consentono toofine ottimizzazione hello i dati hello provisioning servizio estrae da Azure AD filtrando gli utenti in base ai valori di attributo specifico. Per altre informazioni sui filtri di ambito, vedere [Provisioning dell'applicazione basato su attributi con filtri per la definizione dell'ambito](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

## <a name="next-steps"></a>Passaggi successivi
[Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory](active-directory-saas-app-provisioning.md)

