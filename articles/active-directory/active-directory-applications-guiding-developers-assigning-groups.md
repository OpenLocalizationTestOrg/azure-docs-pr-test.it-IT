---
title: Assegnare gruppi alle app Azure AD | Documentazione Microsoft
description: Come implementare l'assegnazione di gruppo per le applicazioni Azure.
services: active-directory
documentationcenter: 
author: kgremban
manager: mtillman
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: 471099c58a7fc1dfd520e693873a76f64c0fbf0a
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a>Assegnare gruppi di Azure Active Directory a un'applicazione
Prima di assegnare utenti e gruppi a un'applicazione, è necessario richiedere l'assegnazione dell’utente. Per informazioni su come richiedere l'assegnazione dell'utente, vedere l'articolo [Richiedere l'assegnazione utente](active-directory-applications-guiding-developers-requiring-user-assignment.md) .

In questo articolo si presuppone che siano già stati creati gruppi nella active directory che si utilizza per questa applicazione.

## <a name="assigning-groups-to-an-application"></a>Assegnazione dei gruppi a un'applicazione
1. Accedere al portale di Azure con un account amministratore.
2. Fare clic sulla voce **Tutti gli elementi** del menu principale.
3. Scegliere la directory utilizzata per l'applicazione.
4. Fare clic sulla scheda **APPLICAZIONI** .
5. Selezionare l'applicazione dall'elenco di applicazioni associate a questa directory.
6. Fare clic sulla scheda **UTENTI E GRUPPI** .
7. Filtrare l'elenco dei gruppi nella active directory utilizzando l’elenco a discesa **Gruppi** .
8. Selezionare il gruppo.
9. Fare clic su **ASSEGNARE**.
10. Fare clic su **sì** quando richiesto.

## <a name="next-steps"></a>Fasi successive
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
