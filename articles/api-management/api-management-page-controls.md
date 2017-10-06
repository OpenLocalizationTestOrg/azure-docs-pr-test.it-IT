---
title: controlli di pagina di gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui controlli della pagina hello disponibili per l'utilizzo nei modelli di portale per sviluppatori in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Controlli pagina in Gestione API di Azure
Gestione API di Azure fornisce i seguenti controlli per l'utilizzo nei modelli del portale per sviluppatori di hello hello.  
  
 un controllo, toouse posizionarlo nel percorso di hello desiderato nel modello di portale per sviluppatori di hello. Alcuni controlli, ad esempio hello [app azioni](#app-actions) di controllo, dispone di parametri, come illustrato nell'esempio seguente hello.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 valori Hello hello parametri vengono passati come parte del modello di dati hello per modello hello. Nella maggior parte dei casi, è possibile semplicemente incollare hello disponibili esempio per ogni controllo toowork correttamente. Per ulteriori informazioni sui valori dei parametri di hello, è possibile visualizzare sezione modello di dati hello per ogni modello in cui è possibile utilizzare un controllo.  
  
 Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Controlli pagina per i modelli nel portale per sviluppatori  
  
-   [app-actions](#app-actions)  
  
-   [basic-signin](#basic-signin)  
  
-   [paging-control](#paging-control)  
  
-   [provider](#providers)  
  
-   [search-control](#search-control)  
  
-   [sign-up](#sign-up)  
  
-   [subscribe-button](#subscribe-button)  
  
-   [subscription-cancel](#subscription-cancel)  
  
##  <a name="app-actions"></a> app-actions  
 Hello `app-actions` controllo fornisce un'interfaccia utente per l'interazione con le applicazioni in una pagina del profilo utente hello nel portale per sviluppatori hello.  
  
 ![Controllo app&amp;#45;actions](./media/api-management-page-controls/APIM-app-actions-control.png "Controllo app-actions in Gestione API di Azure")  
  
### <a name="usage"></a>Utilizzo  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>parameters  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|appId|id di Hello dell'applicazione hello.|  
  
### <a name="developer-portal-templates"></a>Modelli del portale per sviluppatori  
 Hello `app-actions` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.  
  
-   [Applicazioni](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a> basic-signin  
 Hello `basic-signin` controllo fornisce un controllo per la raccolta di accesso degli utenti nelle informazioni di hello Accedi pagina nel portale per sviluppatori hello.  
  
 ![Controllo basic&#45;signin](./media/api-management-page-controls/APIM-basic-signin-control.png "Controllo basic-signin in Gestione API di Azure")  
  
### <a name="usage"></a>Utilizzo  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>parameters  
 Nessuna.  
  
### <a name="developer-portal-templates"></a>Modelli del portale per sviluppatori  
 Hello `basic-signin` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.  
  
-   [Accesso](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> paging-control  
 Hello `paging-control` offre funzionalità di paging in developer pagine del portale che consentono di visualizzare un elenco di elementi.  
  
 ![paging-control](./media/api-management-page-controls/APIM-paging-control.png "paging-control in Gestione API di Azure")  
  
### <a name="usage"></a>Utilizzo  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>parameters  
 Nessuna.  
  
### <a name="developer-portal-templates"></a>Modelli del portale per sviluppatori  
 Hello `paging-control` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.  
  
-   [Elenco API](api-management-api-templates.md#APIList)  
  
-   [Elenco di problemi](api-management-issue-templates.md#IssueList)  
  
-   [Elenco dei prodotti](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> providers  
 Hello `providers` controllo fornisce un controllo per la selezione dei provider di autenticazione in una pagina nel portale per sviluppatori hello hello accesso.  
  
 ![Controllo providers](./media/api-management-page-controls/APIM-providers-control.png "Controllo providers in Gestione API di Azure")  
  
### <a name="usage"></a>Utilizzo  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>parameters  
 Nessuna.  
  
### <a name="developer-portal-templates"></a>Modelli del portale per sviluppatori  
 Hello `providers` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.  
  
-   [Accesso](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> search-control  
 Hello `search-control` offre funzionalità di ricerca in developer pagine del portale che consentono di visualizzare un elenco di elementi.  
  
 ![search- control](./media/api-management-page-controls/APIM-search-control.png "search-control in Gestione API di Azure")  
  
### <a name="usage"></a>Utilizzo  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>parameters  
 Nessuna.  
  
### <a name="developer-portal-templates"></a>Modelli del portale per sviluppatori  
 Hello `search-control` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.  
  
-   [Elenco API](api-management-api-templates.md#APIList)  
  
-   [Elenco dei prodotti](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> sign-up  
 Hello `sign-up` controllo offre un controllo per la raccolta di informazioni sul profilo utente nella pagina nel portale per sviluppatori hello di iscrizione hello.  
  
 ![Controllo sign&amp;#45;up](./media/api-management-page-controls/APIM-sign-up-control.png "Controllo sign-up in Gestione API di Azure")  
  
### <a name="usage"></a>Utilizzo  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>parameters  
 Nessuna.  
  
### <a name="developer-portal-templates"></a>Modelli del portale per sviluppatori  
 Hello `sign-up` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.  
  
-   [Iscrizione](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> subscribe-button  
 Hello `subscribe-button` fornisce un controllo per la sottoscrizione di un prodotto tooa utente.  
  
 ![Controllo subscribe&amp;#45;button](./media/api-management-page-controls/APIM-subscribe-button-control.png "Controllo subscribe-button in Gestione API di Azure")  
  
### <a name="usage"></a>Utilizzo  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>parameters  
 Nessuna.  
  
### <a name="developer-portal-templates"></a>Modelli del portale per sviluppatori  
 Hello `subscribe-button` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.  
  
-   [Prodotto](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> subscription-cancel  
 Hello `subscription-cancel` controllo fornisce un controllo per l'annullamento di un prodotto tooa sottoscrizione nella pagina del profilo utente hello nel portale per sviluppatori hello.  
  
 ![Controllo subscription&amp;#45;cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Controllo subscription-cancel in Gestione API di Azure")  
  
### <a name="usage"></a>Utilizzo  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>parameters  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|subscriptionId|id di Hello di hello toocancel di sottoscrizione.|  
|cancelUrl|sottoscrizione Hello annullare URL.|  
  
### <a name="developer-portal-templates"></a>Modelli del portale per sviluppatori  
 Hello `subscription-cancel` controllo può essere utilizzato nei seguenti modelli portale per sviluppatori hello.  
  
-   [Prodotto](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).
