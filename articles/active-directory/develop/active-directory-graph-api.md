---
title: API di Active Directory Graph aaaAzure | Documenti Microsoft
description: Una Guida di panoramica e Guida introduttiva per Graph API che consente a livello di codice hello accedere tooAzure AD attraverso gli endpoint dell'API REST.
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>API Graph di Azure Active Directory
> [!IMPORTANT]
> È consigliabile utilizzare [Microsoft Graph](https://graph.microsoft.io/) anziché tooaccess API Azure AD Graph risorse di Azure Active Directory. Le attività di sviluppo sono ora concentrate su Microsoft Graph e non sono previsti altri miglioramenti all'API Graph di Azure AD. Esistono un numero molto limitato di scenari per cui Azure AD Graph API potrebbe essere ancora appropriata; Per ulteriori informazioni, vedere hello [Microsoft Graph o hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) post di blog in hello Office Dev Center.
> 
> 

Hello API di Graph di Azure Active Directory fornisce l'accesso programmatico tooAzure AD attraverso gli endpoint dell'API REST. Le applicazioni possono utilizzare hello API Graph tooperform creare, leggere, aggiornare e l'eliminazione (CRUD) sui dati di directory e oggetti. Ad esempio, hello API Graph supporta hello operazioni comuni di un oggetto utente di seguenti:

* Creare un nuovo utente nella directory
* Recuperare le proprietà dettagliate dell'utente, ad esempio i gruppi a cui appartiene
* Aggiornare le proprietà dell'utente, ad esempio indirizzo e numero di telefono, oppure modifica della password
* Verificare l'appartenenza a gruppi di un utente per l'accesso in base al ruolo
* Disabilitare o eliminare completamente l'account di un utente

Negli oggetti toouser aggiunta, è possibile eseguire operazioni simili su altri oggetti, ad esempio i gruppi e applicazioni. hello toocall API Graph in una directory, l'applicazione hello deve essere registrato con Azure AD e di essere configurato tooallow accesso toohello directory. A tale scopo, viene in genere eseguito un flusso di consenso utente o amministratore.

utilizzando toobegin hello API Graph di Azure Active Directory, vedere hello [Guida rapida di Graph API](active-directory-graph-api-quickstart.md), o visualizzazione hello [interattiva documentazione di riferimento sull'API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="features"></a>Funzionalità
Hello API Graph offre hello seguenti caratteristiche:

* **Gli endpoint dell'API REST**: hello API Graph è un servizio RESTful include endpoint accessibili mediante richieste HTTP standard. Hello API Graph supporta i tipi di contenuto XML o Javascript Object Notation (JSON) per le richieste e risposte. Per altre informazioni, vedere [Riferimento all'API REST di Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **L'autenticazione con Azure AD**: toohello ogni richiesta API Graph deve essere autenticata aggiungendo un JSON Web Token (JWT) nell'intestazione di autorizzazione hello della richiesta di hello. Questo token viene acquisito effettua endpoint token tooAzure una richiesta di AD e fornendo credenziali valide. È possibile usare il flusso di credenziali client OAuth 2.0 hello o concessione del codice di autorizzazione hello tooacquire flusso hello un token toocall grafico. Per altre informazioni, vedere [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Autorizzazione basata sui ruoli (RBAC)**: gruppi di sicurezza sono utilizzati tooperform RBAC in hello API Graph. Ad esempio, se si desidera toodetermine se un utente ha accesso tooa di risorse, un'applicazione hello può chiamare hello [controllare l'appartenenza al gruppo (transitiva)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) , operazione che restituisce true o false.
* **Query differenziale**: se si desidera toocheck per le modifiche in una directory tra due periodi di tempo senza toomake frequenti query toohello API Graph, è possibile effettuare una richiesta di query differenziale. Questo tipo di richiesta restituirà solo le modifiche apportate hello tra hello richiesta precedente e la richiesta corrente hello. Per altre informazioni, vedere [Query differenziale dell'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Le estensioni di directory**: se si sviluppa un'applicazione che richiede proprietà univoche tooread o di scrittura per gli oggetti directory, è possibile registrare e utilizzare i valori di estensione utilizzando hello API Graph. Ad esempio, se l'applicazione richiede una proprietà ID Skype per ciascun utente, è possibile registrare una nuova proprietà hello nella directory hello e sarà disponibile in ogni oggetto utente. Per altre informazioni, vedere [Estensioni dello schema di directory dell'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **Protetta da ambiti di autorizzazione**: API di Azure ad Graph espone gli ambiti di autorizzazione che consentono di proteggere acconsentito accesso tooAAD dati e supportano un'ampia gamma di tipi di app client, inclusi:
  
  * con un'interfaccia utente viene assegnato un delegato tramite toodata tramite autorizzazione hello utente connesso (delegato)
  * quelli che utilizzano il controllo degli accessi in base al ruolo definito dall’applicazione, ad esempio i client di servizio/daemon (ruoli app)
    
    Entrambi delegati e gli ambiti di autorizzazione ruolo app rappresentano un privilegio esposto dall'API Graph hello e possono essere richiesti dalle applicazioni client tramite le autorizzazioni di registrazione applicazione [funzionalità nel portale di Azure hello](https://portal.azure.com). I client è possono verificare gli ambiti di autorizzazione hello concesso toothem controllando l'attestazione di ambito ("scp") hello ricevuta nel token di accesso hello per le autorizzazioni delegate e attestazione ruoli hello ("ruoli") per le autorizzazioni del ruolo applicazione. Altre informazioni sugli [ambiti di autorizzazione dell'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).

## <a name="scenarios"></a>Scenari
API Graph Hello apre molti scenari di applicazione. Hello seguenti scenari è hello più comune:

* **Applicazione line-of-business (single-tenant)**: in questo scenario, uno sviluppatore aziendale lavora per un'organizzazione con un abbonamento a Office 365. Hello sviluppatore un'applicazione web che interagisce con le attività di Azure AD tooperform ad assegna una licenza tooa un utente. Questa attività richiede accesso toohello API Graph, in modo developer hello registra un'applicazione hello single-tenant in Azure AD e configura le autorizzazioni lettura e scrittura per hello API Graph. Hello quindi l'applicazione è configurata toouse le proprie credenziali o quelle di hello attualmente Accedi utente tooacquire un token toocall hello API Graph.
* **Applicazione SaaS (multi-tenant)**: in questo scenario, un fornitore di software indipendente (ISV) sviluppa un'applicazione Web multi-tenant ospitata che fornisce funzionalità per la gestione degli utenti per altre organizzazioni che usano Azure AD. Queste funzionalità richiedono l'accesso toodirectory oggetti, e pertanto un'applicazione hello deve toocall hello API Graph. sviluppatore Hello registra un'applicazione hello in Azure AD, configura toorequire lettura e scrittura le autorizzazioni per l'API Graph hello e quindi Abilita l'accesso esterno in modo che altre organizzazioni possano accettare un'applicazione hello toouse nella propria directory. Quando un utente in un'altra organizzazione autentica toohello applicazione hello per la prima volta, viene visualizzata una finestra di dialogo di consenso dell'utente con autorizzazioni di hello richiede un'applicazione hello.  Concessione dell'autorizzazione verrà quindi assegnare un'applicazione hello quelle richieste autorizzazioni toohello API Graph nella directory dell'utente hello. Per ulteriori informazioni sul framework di consenso hello, vedere [Panoramica del Framework di consenso hello](active-directory-integrating-applications.md).

## <a name="see-also"></a>Vedere anche
[Guida introduttiva per l'API Graph di Azure AD](active-directory-graph-api-quickstart.md)

[Documentazione di riferimento all'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Guida per gli sviluppatori di Azure Active Directory](active-directory-developers-guide.md)

