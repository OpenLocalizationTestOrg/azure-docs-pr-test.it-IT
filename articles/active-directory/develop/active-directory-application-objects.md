---
title: "aaaAzure applicativa Active Directory e oggetti entità servizio | Documenti Microsoft"
description: "Una descrizione della relazione di hello tra applicazioni e oggetti entità servizio in Azure Active Directory"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Oggetti applicazione e oggetti entità servizio in Azure Active Directory (Azure AD)
In alcuni casi hello significato del termine hello "applicazione" può essere interpretati erroneamente utilizzata nel contesto di hello di Azure Active Directory. obiettivo di Hello di questo articolo è toomake è chiaro, indicando concettuali e concreti aspetti dell'integrazione dell'applicazione Azure AD, con un'illustrazione di registrazione e di consenso per un [applicazione multi-tenant](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Panoramica
Un'applicazione che è stata integrata con Azure AD ha implicazioni che vanno oltre aspetto software hello. "Application" viene spesso utilizzato come un termine concettuale, che fa riferimento toonot solo hello hello software dell'applicazione, ma la registrazione di Azure AD e ruolo di autenticazione/autorizzazione "conversazioni" in fase di esecuzione. Per definizione, un'applicazione può funzionare in un [client](active-directory-dev-glossary.md#client-application) ruolo (utilizzo di una risorsa), un [server delle risorse](active-directory-dev-glossary.md#resource-server) ruolo (che espone le API tooclients) o anche a entrambi. protocollo di conversazione Hello è definito da un [flusso di concessione di autorizzazione OAuth 2.0](active-directory-dev-glossary.md#authorization-grant), consentendo hello client o risorse tooaccess/proteggere dei dati una risorsa rispettivamente. Ora passiamo un livello più interno e vedere come modello di applicazione hello Azure AD rappresenta un'applicazione in fase di progettazione e in fase di esecuzione. 

## <a name="application-registration"></a>Registrazione dell'applicazione
Quando si registra un'applicazione Azure AD in hello [portale di Azure][AZURE-Portal], vengono creati due oggetti nel tenant di Azure AD: un oggetto applicazione e un oggetto entità servizio.

#### <a name="application-object"></a>Oggetto applicazione
Un'applicazione Azure AD è definita dal relativo l'unico oggetto applicazione che si trova nel tenant di Azure AD hello in cui è stata registrata un'applicazione hello, noto come tenant "home" dell'applicazione hello. Hello Azure AD Graph [entità applicazione] [ AAD-Graph-App-Entity] definisce lo schema di hello per le proprietà dell'oggetto di un'applicazione. 

#### <a name="service-principal-object"></a>Oggetto entità servizio
oggetto entità servizio Hello definisce i criteri di hello e le autorizzazioni per l'utilizzo di un'applicazione in un tenant specifico, fornendo la base hello per un'applicazione hello toorepresent dell'entità di sicurezza in fase di esecuzione. Hello Azure AD Graph [entità ServicePrincipal] [ AAD-Graph-Sp-Entity] definisce lo schema di hello per le proprietà dell'oggetto principale un servizio. 

#### <a name="application-and-service-principal-relationship"></a>Relazione tra applicazione e entità servizio
Si consideri l'oggetto applicazione hello come hello *globale* rappresentazione dell'applicazione per l'utilizzo in tutti i tenant e dell'entità servizio hello come hello *locale* rappresentazione per l'utilizzo in uno specifico tenant. Hello oggetto applicazione funge da hello modello dal quale comuni e le proprietà predefinite sono *derivato* per la creazione di oggetti entità di servizio corrispondente. Pertanto, un oggetto applicazione ha una relazione 1:1 con un'applicazione software hello e una relazione 1: molti con i relativi oggetti principale di servizio corrispondente.

Quando un'applicazione hello verrà utilizzata, abilitarlo tooestablish un'identità per l'accesso e/o tooresources accesso protetto dal tenant hello, è necessario creare un'entità servizio in ogni tenant. Un'applicazione single-tenant avrà solamente un'entità servizio (nel relativo tenant principale), in genere creata e autorizzata per essere usata durante la registrazione dell'applicazione. O API di applicazione Web di multi-tenant disporrà di un'entità di servizio creata in ogni tenant in cui un utente di tenant ha accettato le condizioni tooits utilizzare.  

> [!NOTE]
> Le modifiche apportate tooyour oggetto applicazione, si riflettono anche nell'oggetto entità servizio dell'applicazione hello home tenant solo (tenant hello in cui è stata registrata). Per le applicazioni multi-tenant, le modifiche toohello applicazione non sono riportate negli oggetti dell'entità servizio di qualsiasi tenant consumer, fino a quando non viene rimosso l'accesso di hello tramite hello [Pannello di accesso dell'applicazione](https://myapps.microsoft.com) e concedere nuovamente.
><br>  
> Si noti anche che le applicazioni native sono registrate come multi-tenant per impostazione predefinita.
> 
> 

## <a name="example"></a>Esempio
Hello diagramma seguente viene illustrata hello relazione tra un'applicazione oggetto di applicazione e servizio corrispondente oggetti entità, nel contesto di hello di un'applicazione multi-tenant di esempio denominati **app HR**. In questo scenario sono presenti tre tenant di Azure AD: 

* **Adatum** : hello tenant utilizzata dalla società hello sviluppato hello **app HR**
* **Contoso** : hello tenant usato dall'organizzazione Contoso, che funge da consumer di hello hello **app HR**
* **Fabrikam** : hello tenant usato dall'organizzazione di Fabrikam, che utilizza anche hello hello **app HR**

![Relazione tra un oggetto applicazione e un oggetto entità servizio](./media/active-directory-application-objects/application-objects-relationship.png)

Nel diagramma precedente hello, passaggio 1 è il processo di hello di creazione di un'applicazione hello e oggetti entità servizio nel tenant principale dell'applicazione hello.

Nel passaggio 2, quando gli amministratori di Contoso e Fabrikam completa ottenuto il consenso, un oggetto entità servizio viene creato nel tenant di Azure AD della propria azienda e le autorizzazioni assegnate hello concesso tale messaggio per l'amministratore. Si noti inoltre che app HR hello può essere configurato progettato tooallow consenso da parte degli utenti per l'uso di singoli.

Nel passaggio 3, i tenant consumer hello di hello HR applicazione (Contoso e Fabrikam ogni) hanno proprio oggetto entità servizio. Ogni oggetto rappresenta l'uso di un'istanza di un'applicazione hello in fase di esecuzione disciplinato hello acconsentite autorizzazioni da amministratore rispettivi hello.

## <a name="next-steps"></a>Passaggi successivi
Oggetto applicazione di un'applicazione accessibile tramite API di Azure AD Graph, hello hello [portale di Azure] [ AZURE-Portal] editor del manifesto dell'applicazione, o [cmdlet di Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), come rappresentato dal relativo OData [entità applicazione][AAD-Graph-App-Entity].

Oggetto entità servizio dell'applicazione è possibile accedere tramite API Azure AD Graph hello o [i cmdlet di Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), come rappresentato dal relativo OData [entità ServicePrincipal] [ AAD-Graph-Sp-Entity].

Hello [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) è utile per l'esecuzione di query sia un'applicazione hello e oggetti entità servizio.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
