---
title: App aaaProvisioning con i filtri di ambito | Documenti Microsoft
description: Informazioni su come ambito toouse Filtra gli oggetti di tooprevent nelle applicazioni che supportano il provisioning utenti automatizzato da effettivamente in corso il provisioning se un oggetto non soddisfa i requisiti aziendali.
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
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Provisioning dell'applicazione basato su attributi con filtri per la definizione dell'ambito
obiettivo di Hello di questa sezione è tooexplain come ambito toouse filtri toodefine basato su attributi regole che determinano quali utenti sono il provisioning dell'applicazione toohello.

## <a name="clauses-and-scope-groups"></a>Clausole e gruppi di ambiti
![Filtro per la definizione dell’ambito][1] 

I filtri per la determinazione dell'ambito sono definiti da uno o più **gruppi di ambiti**, ognuno dei quali contiene una o più **clausole**. clausole hello toosee per un particolare gruppo di ambito, espandere facendo clic a sinistra di hello freccia toohello hello del nome di gruppo.

Oggetto **clausola** determina quali utenti sono autorizzati toopass tramite hello definizione ambito filtro valutando gli attributi di ogni utente. Ad esempio, potrebbe essere una clausola che richiede che 'state' attributo uguale New York un utente, in modo solo gli utenti di New York vengono effettuato il provisioning in un'applicazione hello.

![Nome del gruppo di ambiti][2] 

Ogni **gruppo ambito** inizia con uno obbligatorio **clausola**, come illustrato nella schermata di hello precedente. Questa clausola indica semplicemente che l'utente hello deve essere assegnato toohello applicazione prima di essere valutato dai filtri di ambito. Questa clausola non può essere eliminata né modificata.

È possibile aggiungere nuove clausole o nuovi gruppi di ambito premendo l'apposito pulsante hello. Per assegnare un nome a ogni gruppo di ambiti, modificare la relativa proprietà **Nome del gruppo di ambiti** .

## <a name="how-scoping-filters-are-evaluated"></a>Modalità di valutazione dei filtri per la definizione dell'ambito
Durante il provisioning, ogni utente assegnato contro l'ambito toodetermine filtri verranno testate se l'applicazione di accesso toohello è idoneo. È possibile considerare ogni clausola come un test che deve essere passato affinché tooavoid utente hello venga escluso. 

Se si dispone di più gruppi di ambito definiti, ogni utente deve passare almeno uno di essi tooaccess applicazione hello. All'interno di ogni gruppo di ambito, tuttavia, hello utente deve passare toopass ogni clausola tale gruppo di ambito specifico. 

In altre parole, è possibile considerare come i gruppi di ambito o correlati con l'operatore e può essere considerato clausole hello al loro interno come AND correlati con l'operatore. Si consideri ad esempio hello definizione ambito filtro riportato di seguito:

![Nome del gruppo di ambiti][3]  

In base toothis definizione ambito filtro, gli utenti devono soddisfare seguente hello criteri, toobe il provisioning:

1. È necessario assegnare toohello applicazione.
2. Devono lavorare nel reparto Engineering hello
3. La sede di lavoro deve trovarsi a San Francisco o in Canada.

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Automatizzare applicazioni di tooSaaS Provisioning e Deprovisioning](active-directory-saas-app-provisioning.md)
* [Personalizzazione dei mapping degli attributi per il Provisioning dell’utente](active-directory-saas-customizing-attribute-mappings.md)
* [Scrittura di espressioni per i mapping degli attributi](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Notifiche relative al provisioning dell'account](active-directory-saas-account-provisioning-notifications.md)
* [Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
