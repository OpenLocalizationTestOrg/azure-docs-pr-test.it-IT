---
title: aaaFind out quando un utente specifico saranno in grado di tooaccess un'applicazione | Documenti Microsoft
description: Come toofind out quando un utente di estremamente importante essere in grado di tooaccess un'applicazione sono stati configurati per il provisioning utente con Azure AD
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a>Sapere quando un utente specifico sarà in grado di tooaccess un'applicazione
Quando si usa il provisioning utenti automatico con un'applicazione, Azure AD esegue automaticamente il provisioning e aggiorna gli account utente in un'app in base ad alcuni elementi, ad esempio l'[assegnazione di utenti e gruppi](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal), a intervalli regolari pianificati, in genere ogni 10 minuti.

## <a name="how-long-does-it-take"></a>Quanto tempo occorre?

Hello tempo richiesto per toobe un determinato utente provisioning dipende principalmente dal è già stata eseguita o meno una sincronizzazione iniziale "full".

Hello prima sincronizzazione tra Azure AD e un'app può richiedere ore tooseveral 20 minuti, a seconda delle dimensioni di hello di hello Azure Active directory e il numero di hello degli utenti in ambito per il provisioning. 

Le sincronizzazioni successive dopo la sincronizzazione iniziale di hello risultare più veloce (ad esempio all'interno di 10 minuti), come hello provisioning servizio archivia le soglie che rappresentano lo stato di hello di entrambi i sistemi dopo la sincronizzazione iniziale hello, migliorando le prestazioni di sincronizzazioni successive.

## <a name="how-toocheck-hello-status-of-a-user"></a>Come toocheck hello lo stato di un utente

stato di provisioning hello toosee per un utente selezionato, consultare hello i log di controllo di Azure AD.

Hello provisioning i log di controllo sono accessibili nel portale di Azure in hello hello **Azure Active Directory &gt; le app aziendali &gt; \[nome applicazione\] &gt; log di controllo**scheda. Hello filtro accede hello **Provisioning Account** tooonly categoria vedere hello provisioning gli eventi per tale applicazione. È possibile cercare utenti basati su hello "corrispondenti all'ID" che è stato configurato per tali mapping degli attributi di hello. 

Ad esempio, se è stato configurato hello "nome dell'entità utente" o "indirizzo di posta elettronica" come hello corrispondenti all'attributo sul lato di hello Azure AD, e non da il provisioning degli utenti hello ha un valore di "audrey@contoso.com", quindi di log di controllo di hello ricerca per"audrey@contoso.com" e quindi esaminare le voci restituite.

Hello provisioning controllo Registra record tutti hello le operazioni eseguite da hello provisioning del servizio, tra cui:

* Esecuzione in Azure AD di query sugli utenti assegnati che rientrano nell'ambito del provisioning
* Applicazione di destinazione hello esistenza hello di tali utenti l'esecuzione di query
* Confronto di oggetti utente hello tra sistema hello
* Aggiunta, aggiornamento o la disattivazione di account utente di hello nel sistema di destinazione hello in base a confronto hello

## <a name="next-steps"></a>Passaggi successivi
[Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)'
