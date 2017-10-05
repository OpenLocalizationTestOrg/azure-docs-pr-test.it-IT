---
title: Eseguire il provisioning delle app con filtri per la definizione dell'ambito | Documentazione Microsoft
description: Informazioni su come usare i filtri per la definizione dell'ambito per evitare che venga eseguito il provisioning degli oggetti inclusi nelle app che supportano il provisioning automatico degli utenti se un oggetto non soddisfa i requisiti aziendali.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Provisioning dell'applicazione basato su attributi con filtri per la definizione dell'ambito
Questa sezione spiega come usare i filtri per la definizione dell'ambito per definire regole basate su attributi per determinare gli utenti per i quali viene eseguito il provisioning nell'applicazione.

## <a name="clauses-and-scope-groups"></a>Clausole e gruppi di ambiti
![Filtro per la definizione dell’ambito][1] 

I filtri per la determinazione dell'ambito sono definiti da uno o più **gruppi di ambiti**, ognuno dei quali contiene una o più **clausole**. Per visualizzare le clausole per un gruppo di ambiti specifico, espanderlo facendo clic sulla freccia a sinistra del nome del gruppo.

Una **clausola** determina gli utenti che verranno restituiti dal filtro per la definizione dell'ambito valutando gli attributi di ogni utente. Ad esempio, se una clausola richiede che l'attributo 'state' di un utente sia uguale a New York, nell'applicazione viene eseguito il provisioning solo degli utenti di New York.

![Nome del gruppo di ambiti][2] 

Ogni **gruppo di ambiti** inizia con una **clausola** obbligatoria, come mostrato nella schermata. Questa clausola indica semplicemente che l'utente deve essere assegnato all'applicazione prima di essere valutato dai filtri per la definizione dell'ambito. Questa clausola non può essere eliminata né modificata.

Per aggiungere nuove clausole o nuovi gruppi di ambiti, fare clic sul pulsante corrispondente. Per assegnare un nome a ogni gruppo di ambiti, modificare la relativa proprietà **Nome del gruppo di ambiti** .

## <a name="how-scoping-filters-are-evaluated"></a>Modalità di valutazione dei filtri per la definizione dell'ambito
Durante il provisioning, ogni utente assegnato viene verificato in base ai filtri per la definizione dell'ambito per stabilire se l'utente è autorizzato ad accedere all'applicazione. Si può pensare a una clausola come a un test che deve essere superato affinché l'utente non venga escluso. 

Se sono stati definiti più gruppi di ambiti, ogni utente deve superarne almeno uno per poter accedere all'applicazione. All'interno di ogni gruppo di ambiti, tuttavia, l'utente deve superare la clausola per soddisfare i criteri del gruppo di ambiti specifico. 

In altre parole, è come se i gruppi di ambiti fossero collegati tramite operatore OR e le clausole in essi contenute fossero collegate tramite operatore AND. Vedere ad esempio il filtro per la definizione dell'ambito seguente:

![Nome del gruppo di ambiti][3]  

In base a questo filtro per la definizione dell'ambito, affinché sia possibile eseguire il provisioning degli utenti nell'applicazione, questi devono soddisfare i criteri seguenti:

1. Devono essere assegnati all'applicazione.
2. Devono lavorare nel reparto Engineering.
3. La sede di lavoro deve trovarsi a San Francisco o in Canada.

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS](active-directory-saas-app-provisioning.md)
* [Personalizzazione dei mapping degli attributi per il Provisioning dell’utente](active-directory-saas-customizing-attribute-mappings.md)
* [Scrittura di espressioni per i mapping degli attributi](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Notifiche relative al provisioning dell'account](active-directory-saas-account-provisioning-notifications.md)
* [Uso di SCIM per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory alle applicazioni](active-directory-scim-provisioning.md)
* [Elenco di esercitazioni pratiche sulla procedura di integrazione delle applicazioni SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
