---
title: aaaQuickstart per hello Azure AD Graph API | Documenti Microsoft
description: Hello API di Graph di Azure Active Directory fornisce l'accesso programmatico tooAzure AD attraverso gli endpoint dell'API REST OData. Le applicazioni possono utilizzare hello API Graph tooperform creare, leggere, aggiornare e l'eliminazione (CRUD) sui dati di directory e oggetti.
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Avvio rapido per hello API Azure AD Graph
Hello API Graph di Azure Active Directory (AD) fornisce l'accesso programmatico tooAzure AD attraverso gli endpoint dell'API REST OData. Le applicazioni possono utilizzare hello API Graph tooperform creare, leggere, aggiornare e l'eliminazione (CRUD) sui dati di directory e oggetti. Ad esempio, è possibile utilizzare hello API Graph toocreate un nuovo utente, vista o aggiornare le proprietà dell'utente, modificare la password utente, verificare l'appartenenza al gruppo per l'accesso basato sui ruoli, disabilitare o eliminare hello utente. Per ulteriori informazioni sulle funzionalità dell'API Graph hello e sugli scenari di applicazione, vedere [API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) e [prerequisiti di Azure AD Graph API](https://msdn.microsoft.com/library/hh974476.aspx). 

> [!IMPORTANT]
> È consigliabile utilizzare [Microsoft Graph](https://developer.microsoft.com/graph) anziché tooaccess API Azure AD Graph risorse di Azure Active Directory. Le attività di sviluppo sono ora concentrate su Microsoft Graph e non sono previsti altri miglioramenti all'API Graph di Azure AD. Esistono un numero molto limitato di scenari per cui Azure AD Graph API potrebbe essere ancora appropriata; Per ulteriori informazioni, vedere hello [Microsoft Graph o hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) post di blog in hello Office Dev Center.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>Come tooconstruct un URL dell'API Graph
Nell'API Graph, i dati di directory tooaccess e oggetti (in altre parole, le risorse o le entità) con cui eseguire le operazioni CRUD tooperform, è possibile utilizzare l'URL in base alle hello protocollo Open Data (OData). Hello gli URL usati nell'API Graph sono costituiti da quattro parti principali: radice, identificatore del tenant, percorso della risorsa e le opzioni di stringa di query del servizio: `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`. Nell'esempio hello di hello seguente URL: `https://graph.windows.net/contoso.com/groups?api-version=1.6`.

* **Radice del servizio**: nell'API Graph di Azure Active Directory radice del servizio hello è sempre https://graph.windows.net.
* **Identificatore del tenant**: in questa sezione può essere un nome di dominio (registrato) verificato, come nell'esempio sopra riportato, hello contoso.com. Può anche essere un tenant oggetto ID o hello "myorganization" o "me" alias. Per ulteriori informazioni, vedere [indirizzamento di entità e operazioni nell'API Graph hello](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **Percorso della risorsa**: in questa sezione di un URL identifica una risorsa hello toobe interagire (utenti, gruppi, un utente specifico, o un gruppo specifico e così via) Nell'esempio hello sopra, è tooaddress "gruppi di primo livello" hello set di risorse. È anche possibile risolvere un'entità specifica, ad esempio "users/{objectId}" o "users/userPrincipalName".
* **Parametri di query**: un punto interrogativo (?) separa sezione di percorso hello risorse dalla sezione parametri di query hello. parametro di query "api-version" Hello è necessario in tutte le richieste in hello API Graph. Hello API Graph supporta anche le opzioni di query OData seguenti hello: **$filter**, **$orderby**, **$expand**, **$top**e **$format**. Hello le opzioni di query seguenti non è attualmente supportato: **$count**, **$inlinecount**, e **$skip**. Per altre informazioni, vedere [Query, opzioni di paging e filtri supportati nell'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options).

## <a name="graph-api-versions"></a>Versioni dell'API Graph
Specificare la versione di hello per una richiesta all'API Graph nel parametro di query "api-version" hello. Per la versione 1.5 e successive, usare un valore di versione numerico: api-version=1.6. Per le versioni precedenti, si utilizza una stringa di data che rispetti toohello formato AAAA-MM-GG; ad esempio, api-version = 2013-11-08. Funzionalità di anteprima, utilizzare la stringa hello "beta"; ad esempio, api-version = beta. Per altre informazioni sulle differenze tra le versioni dell'API Graph, vedere [Controllo delle versioni dell'API di Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

## <a name="graph-api-metadata"></a>Metadati dell'API Graph
hello tooreturn file di metadati API Graph, aggiungere il segmento "$metadata" hello dopo l'identificatore del tenant hello in hello URL ad esempio, hello seguente URL restituisce i metadati per una società demo: `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`. È possibile immettere l'URL nella barra degli indirizzi del web browser toosee hello i metadati hello. Hello documento di metadati CSDL restituito descrive hello entità e tipi complessi, le proprietà e funzioni hello e azioni esposte dalla versione di hello dell'API Graph è stato richiesto. L'omissione di parametro api-version hello restituisce i metadati per la versione più recente di hello.

## <a name="common-queries"></a>Query comuni
[Azure AD Graph query comuni dell'API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) vengono elencate query comuni che può essere utilizzata con hello Azure AD Graph, incluse le query che possono essere risorse di primo livello tooaccess utilizzati nelle operazioni tooperform directory e le query nella directory.

Ad esempio, `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` restituisce informazioni sulla società per la directory contoso.com.

O `https://graph.windows.net/contoso.com/users?api-version=1.6` Elenca tutti gli oggetti utente hello directory contoso.com.

## <a name="using-hello-graph-explorer"></a>Utilizzo di hello Esplora grafico
È possibile utilizzare Esplora grafico hello per dati di directory di Azure AD Graph API tooquery hello hello mentre si compila l'applicazione.

di seguito Hello è output di hello verrebbe visualizzato se si toonavigate toohello Esplora grafico, accedi e immettere `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` toodisplay tutti hello utenti nella directory dell'utente connesso di hello:

![API Graph di Azure AD explorer](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**Hello carico Esplora grafico**: hello tooload strumento, passare troppo[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/). Fare clic su **accesso** e Accedi con il toorun credenziali account di Azure AD hello Esplora grafico sul tenant. Se si esegue il proprio tenant Esplora grafico, l'utente o l'amministratore deve tooconsent durante l'accesso. Se si ha una sottoscrizione di Office 365, si ha automaticamente un tenant di Azure AD. credenziali Hello è utilizzare toosign tooOffice 365 sono, in realtà, gli account di Azure AD, si possono usare le credenziali con Esplora grafico.

**Eseguire una query**: toorun una query, digitare la query nella casella di testo di richiesta hello e fare clic su **ottenere** oppure fare clic su hello **immettere** chiave. Hello risultati vengono visualizzati nella casella risposta hello. Ad esempio, `https://graph.windows.net/myorganization/groups?api-version=1.6` Elenca tutti gli oggetti gruppo nella directory hello eseguito l'accesso dell'utente.

Hello nota seguenti funzionalità e limitazioni di hello Esplora grafico:

* Funzionalità di completamento automatico in set di risorse. richiesta di questa funzionalità, fare clic su hello toosee casella di testo (in cui appare hello società URL). È possibile selezionare una risorsa impostato dall'elenco a discesa hello.
* Supporta hello "me" e "myorganization" indirizzare gli alias. Ad esempio, è possibile utilizzare `https://graph.windows.net/me?api-version=1.6` oggetto utente di hello tooreturn dell'utente connesso di hello o `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn tutti gli utenti nella directory corrente hello.
* Una sezione di intestazioni di risposta. Può essere utilizzata in questa sezione toohelp di risolvere i problemi che si verificano durante l'esecuzione di query.
* Un visualizzatore JSON per la risposta hello con le funzionalità di espansione e compressione.
* Nessun supporto per la visualizzazione di una foto di anteprima.

## <a name="using-fiddler-toowrite-toohello-directory"></a>Tramite Fiddler toowrite toohello directory
Ai fini di hello di questa Guida rapida, è possibile utilizzare toopractice Debugger Web Fiddler hello esegue '' le operazioni di scrittura in directory di Azure AD. Per ulteriori informazioni e tooinstall Fiddler, vedere [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler).

Nell'esempio hello seguente, utilizzare il Debugger Web Fiddler toocreate un nuovo gruppo di sicurezza 'MyTestGroup' nella directory di Azure AD.

**Ottenere un token di accesso**: tooaccess Azure AD Graph, i client sono necessari toosuccessfully tooAzure AD prima autenticati. Per altre informazioni, vedere [Scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md).

**Creare ed eseguire una query**: hello completo alla procedura seguente:

1. Aprire il Debugger Web Fiddler e passare toohello **Composer** scheda.
2. Poiché si desidera toocreate un nuovo gruppo di sicurezza, selezionare **Post** come metodo HTTP dal menu a discesa hello hello. Per ulteriori informazioni sulle operazioni e le autorizzazioni su un oggetto di gruppo, vedere [gruppo](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) all'interno di hello [riferimento sull'API REST Graph AD Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
3. In hello campo accanto troppo**Post**, digitare seguito hello come URL della richiesta di hello: `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`.
   
   > [!NOTE]
   > È necessario sostituire mytenantdomain con il nome di dominio hello per le directory di Azure AD.
   > 
   > 
4. Nel campo hello direttamente sotto a discesa Post digitare seguente hello:
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > Sostituire il &lt;il token di accesso&gt; con token di accesso hello per le directory di Azure AD.
   > 
   > 
5. In hello **corpo della richiesta** , digitare il seguente hello:
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    Per altre informazioni sulla creazione di gruppi, vedere [Crea gruppo](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup).

Per ulteriori informazioni sulle entità di Azure AD e tipi esposti da Graph e informazioni sulle operazioni di hello che possono essere eseguite su di essi con Graph, vedere [riferimento sull'API REST Graph AD Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su hello [API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* Per altre informazioni, vedere [Ambiti di autorizzazione dell'API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

