---
title: "Oggetti applicazione e oggetti entità servizio di Azure Active Directory"
description: "Descrizione della relazione tra oggetti applicazione e oggetti entità servizio in Azure Active Directory"
documentationcenter: dev-center-name
author: bryanla
manager: mtillman
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 10/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 85731afd18304e848f8577d8a6665dca3f9ee5d8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Oggetti applicazione e oggetti entità servizio in Azure Active Directory (Azure AD)
Spesso il significato del termine "applicazione" può essere frainteso quando usato nel contesto di Azure AD. Questo articolo intende chiarire gli aspetti concettuali e concreti dell'integrazione dell'applicazione di Azure AD, con un esempio di registrazione e consenso per un'[applicazione multi-tenant](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Panoramica
Un'applicazione che è stata integrata con Azure AD ha delle implicazioni che vanno oltre l'aspetto del software. "Applicazione" viene spesso usato come termine concettuale, che fa riferimento non solo al software applicativo, ma anche alla sua registrazione in Azure AD e al suo ruolo nelle "conversazioni" di autenticazione/autorizzazione in fase di runtime. Per definizione, un'applicazione può funzionare in un ruolo [client](active-directory-dev-glossary.md#client-application) (che utilizza una risorsa), in un ruolo [server di risorse](active-directory-dev-glossary.md#resource-server) (che espone le API ai client) o in entrambi i ruoli. Il protocollo di conversazione è definito da un [flusso di concessione di autorizzazione OAuth 2.0](active-directory-dev-glossary.md#authorization-grant), consentendo al client e alla risorsa di accedere e proteggere, rispettivamente, i dati di una risorsa. Verrà ora approfondito come il modello applicativo di Azure AD rappresenta un'applicazione in fase di progettazione e in fase di esecuzione. 

## <a name="application-registration"></a>Registrazione dell'applicazione
Quando si registra un'applicazione di Azure AD nel [portale di Azure][AZURE-Portal], vengono creati due oggetti nel tenant di Azure AD: un oggetto applicazione e un oggetto entità servizio.

#### <a name="application-object"></a>Oggetto applicazione
Un'applicazione di Azure AD è definita da un solo oggetto applicazione che risiede nel tenant di Azure AD in cui l'applicazione è stata registrata, noto come tenant "home" dell'applicazione. L'[entità applicativa][AAD-Graph-App-Entity] di Azure AD Graph definisce lo schema per le proprietà di un oggetto applicazione. 

#### <a name="service-principal-object"></a>Oggetto entità servizio
Per accedere alle risorse protette da un tenant di Azure AD, l'entità che richiede l'accesso deve essere rappresentata da un'entità di sicurezza. Questo vale sia per gli utenti (entità utente) che per le applicazioni (entità servizio). L'entità di sicurezza definisce i criteri di accesso e le autorizzazioni per l'utente/applicazione nel tenant. Ciò abilita le funzionalità di base, ad esempio l'autenticazione dell'utente/applicazione durante l'accesso e l'autorizzazione durante l'accesso alle risorse.

Quando a un'applicazione viene concesso di accedere alle risorse in un tenant (al momento della registrazione o del [consenso](active-directory-dev-glossary.md#consent)), viene creato un oggetto entità servizio. L'[entità ServicePrincipal][AAD-Graph-Sp-Entity] di Azure AD Graph definisce lo schema delle proprietà di un oggetto entità servizio.  

#### <a name="application-and-service-principal-relationship"></a>Relazione tra applicazione e entità servizio
Si può considerare l'oggetto applicazione come la rappresentazione *globale* dell'applicazione usata in tutti i tenant, e l'entità servizio come la rappresentazione *locale* usata in uno specifico tenant. L'oggetto applicazione funge da modello da cui *derivano* le proprietà comuni e predefinite per l'uso nella creazione di oggetti entità servizio corrispondenti. Un oggetto applicazione ha quindi una relazione 1:1 con l'applicazione software e relazioni 1:molti con gli oggetti entità servizio corrispondenti.

In ogni tenant in cui viene usata l'applicazione è necessario creare un'entità servizio per poter stabilire un'identità per l'iscrizione e/o l'accesso alle risorse che venga protetta da un tenant. Un'applicazione single-tenant ha una sola entità servizio (nel relativo tenant principale), creata e autorizzata per essere usata durante la registrazione dell'applicazione. Un'applicazione Web/API multi-tenant ha anche un'entità servizio creata in ogni tenant in cui l'utente ha dato il consenso all'uso.  

> [!NOTE]
> Qualsiasi modifica apportata all'oggetto applicazione verrà riflessa solo nell'oggetto entità servizio nel tenant home dell'applicazione, ovvero nel tenant in cui è stata registrata. Per le applicazioni multi-tenant, le modifiche apportate all'oggetto applicazione non vengono riflesse negli oggetti entità servizio dei tenant consumer fino a quando non viene rimosso l'accesso tramite il [Pannello di accesso all'applicazione](https://myapps.microsoft.com) e poi concesso nuovamente.
><br>  
> Si noti anche che le applicazioni native sono registrate come multi-tenant per impostazione predefinita.
> 
> 

## <a name="example"></a>Esempio
Il diagramma seguente illustra la relazione tra l'oggetto applicazione e i corrispondenti oggetti entità servizio di un'applicazione, nel contesto di un'applicazione multi-tenant di esempio denominata **app HR**. In questo scenario sono presenti tre tenant di Azure AD: 

* **Adatum**, il tenant usato dalla società che ha sviluppato l'**app HR**
* **Contoso**, il tenant usato dall'organizzazione Contoso, che utilizza l'**app HR**
* **Fabrikam**, il tenant usato dall'organizzazione Fabrikam, che utilizza anch'essa l'**app HR**

![Relazione tra un oggetto applicazione e un oggetto entità servizio](./media/active-directory-application-objects/application-objects-relationship.png)

Nel diagramma qui sopra, il passaggio 1 è il processo di creazione degli oggetti applicazione ed entità servizio nel tenant home dell'applicazione.

Nel passaggio 2, quando gli amministratori di Contoso e Fabrikam completano il consenso, nel tenant di Azure AD della rispettiva società viene creato un oggetto entità servizio a cui vengono assegnate le autorizzazioni concesse dall'amministratore. Si noti anche che l'app HR potrebbe essere configurata/progettata per permettere il consenso da parte di utenti per l'uso individuale.

Nel Passaggio 3, ogni tenant consumer dell'applicazione HR (Contoso e Fabrikam) dispone del proprio oggetto di entità servizio. Ognuno rappresenta l'uso di un'istanza dell'applicazione in fase di runtime, gestito tramite le autorizzazioni concesse dall'amministratore.

## <a name="next-steps"></a>Passaggi successivi
L'oggetto applicazione di un'applicazione è accessibile tramite l'API Graph di Azure AD, l'editor del manifesto dell'applicazione del [portale di Azure][AZURE-Portal] o i [cmdlet PowerShell di Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), come rappresentato dall'[Entità applicativa][AAD-Graph-App-Entity] di OData.

L'oggetto entità servizio di un'applicazione è accessibile tramite l'API Graph di Azure AD o i [cmdlet PowerShell di Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), come rappresentato dall'[Entità ServicePrincipal][AAD-Graph-Sp-Entity] di OData.

L'[Explorer Graph di Azure AD](https://graphexplorer.azurewebsites.net/) è utile per eseguire query sugli oggetti applicazione ed entità servizio.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
