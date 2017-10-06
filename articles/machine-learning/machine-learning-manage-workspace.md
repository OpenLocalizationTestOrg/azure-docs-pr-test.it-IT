---
title: un'area di lavoro di Machine Learning aaaManage | Documenti Microsoft
description: Gestire aree di lavoro di accesso tooAzure Machine Learning, distribuire e gestire i servizi web API ML
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a>Gestire un'area di lavoro di Azure Machine Learning

> [!NOTE]
> Per informazioni sulla gestione dei servizi Web nel portale di servizi Web di Machine Learning hello, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md).
> 
> 

È possibile gestire le aree di lavoro di Machine Learning nel portale di Azure entrambi hello o hello portale di Azure classico.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a>Utilizzare hello portale di Azure

toomanage un'area di lavoro hello portale di Azure:

1. Accedi toohello [portale di Azure](https://portal.azure.com/) utilizzando un account di amministratore della sottoscrizione di Azure.
2. Nella casella di ricerca hello nella parte superiore di hello di hello pagina, immettere "di machine learning aree di lavoro" e quindi selezionare **Machine Learning aree di lavoro**.
3. Fare clic su area di lavoro hello desiderato toomanage.

Inoltre le informazioni di gestione risorse standard toohello e le opzioni disponibili, è possibile:

- Visualizzazione **proprietà** : questa pagina consente di visualizzare informazioni su area di lavoro e risorse hello e sottoscrizione hello e gruppo di risorse collegato con l'area di lavoro, è possibile modificare.
- **Risincronizzazione di archiviazione chiavi** -area di lavoro hello gestisce l'account di archiviazione chiavi toohello. Se i tasti di modifica degli account di archiviazione hello, quindi è possibile fare clic su **Resync chiavi** chiavi hello toosynchronize con area di lavoro hello.

servizi web di hello toomanage associati a questa area di lavoro, usare il portale di servizi Web di Machine Learning hello. Vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md) per informazioni complete.

> [!NOTE]
> toodeploy o gestire i nuovi servizi web, è necessario disporre di un collaboratore o il ruolo di amministratore nel servizio web di hello sottoscrizione toowhich hello viene distribuito. Se si invita a un'altra macchina di tooa utente apprendimento dell'area di lavoro, è necessario assegnare loro ruolo di collaboratore o amministratore tooa sottoscrizione hello prima di poter distribuire o gestire i servizi web. 
> 
>Per ulteriori informazioni sull'impostazione delle autorizzazioni di accesso, vedere [visualizzare le assegnazioni di accesso per utenti e gruppi nel portale di Azure - anteprima pubblica di hello](../active-directory/role-based-access-control-manage-assignments.md).

## <a name="use-hello-azure-classic-portal"></a>Utilizzare hello portale di Azure classico

Usa hello portale di Azure classico, è possibile gestire le aree di lavoro di Machine Learning per:

* Monitorare l'utilizzo dell'area di lavoro hello
* Configurare hello dell'area di lavoro tooallow o negare l'accesso
* Gestire i servizi Web creati nell'area di lavoro hello
* Elimina area di lavoro hello

Inoltre, nella scheda dashboard hello fornisce una panoramica dell'uso dell'area di lavoro e una rapida panoramica delle informazioni dell'area di lavoro.  

> [!TIP]
> In Azure Machine Learning Studio, su hello **servizi WEB** scheda, è possibile aggiungere, aggiornare o eliminare un servizio Web di Machine Learning.
> 
> 

area di lavoro nel portale di Azure classico hello toomanage:

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) utilizzo di Microsoft Azure account, utilizzare account hello associato hello sottoscrizione di Azure.
2. Nel Pannello di servizi di Microsoft Azure hello, fare clic su **MACHINE LEARNING**.
3. Fare clic su area di lavoro hello desiderato toomanage.

Nella pagina dell'area di lavoro Hello sono presenti tre schede:

* **DASHBOARD** -consente l'utilizzo dell'area di lavoro tooview e informazioni
* **Configura** -permette l'area di lavoro toohello toomanage access
* **SERVIZI WEB** -consente i servizi Web toomanage che sono stati pubblicati dall'area di lavoro

### <a name="toomonitor-how-hello-workspace-is-being-used"></a>utilizzo dell'area di lavoro hello toomonitor
Fare clic su hello **DASHBOARD** scheda.

Dal dashboard di hello, è possibile visualizzare l'utilizzo complessivo dell'area di lavoro e ottenere un riepilogo rapido delle informazioni dell'area di lavoro.

* Hello **calcolo** grafico mostra le risorse di calcolo hello in uso dall'area di lavoro hello. È possibile modificare toodisplay visualizzazione hello relativo o assoluto valori ed è possibile modificare l'intervallo di tempo hello hello grafico visualizzato.
* **Panoramica sull'utilizzo** Visualizza l'archiviazione di Azure in uso dall'area di lavoro hello.
* **Quick glance** visualizza un riepilogo delle informazioni dell'area di lavoro e collegamenti utili.

> [!NOTE]
> Hello **Accedi tooML Studio** collegamento consente di aprire Machine Learning Studio usando l'Account Microsoft è stato eseguito l'accesso in hello. Hello Account Microsoft usato toosign in toohello toocreate portale Azure classico un'area di lavoro dispone automaticamente dell'autorizzazione tooopen area di lavoro. tooopen un'area di lavoro, è necessario essere connessi con Account Microsoft che è stato definito come proprietario di hello dell'area di lavoro hello toohello oppure è necessario un invito dall'area di lavoro di hello proprietario toojoin hello tooreceive.
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a>toogrant o sospendere l'accesso per gli utenti
Fare clic su hello **configura** scheda.

Dalla scheda Configurazione hello è possibile:

* Sospensione dell'area di lavoro di accesso toohello Machine Learning facendo clic su Nega. Gli utenti non saranno in grado di tooopen dell'area di lavoro hello in Machine Learning Studio. toorestore accedere, fare clic su Consenti.

toomanage altri account che dispongono di accesso dell'area di lavoro toohello in Machine Learning Studio, fare clic su **Accedi tooML Studio** in hello **DASHBOARD** scheda (vedere la nota che precedono hello relative  **Sign-in tooML Studio**). Verrà visualizzata l'area di lavoro hello in Machine Learning Studio. Da qui, fare clic su hello **impostazioni** scheda e quindi **utenti**. È possibile fare clic su **INVITARE utenti più** toogive utenti accedere toohello area di lavoro, oppure selezionare un utente e fare clic su **rimuovere**.

### <a name="toomanage-web-services-in-this-workspace"></a>servizi web toomanage nell'area di lavoro
Fare clic su hello **servizi WEB** scheda.

Verrà visualizzato un elenco di servizi Web pubblicati da questa area di lavoro.
toomanage un servizio web, fare clic su nome hello nella pagina del servizio Web di hello elenco tooopen hello.

Per un servizio Web possono essere definiti uno o più endpoint.

* È possibile definire più endpoint nell'endpoint "Default" toohello di addizione. tooadd hello endpoint, fare clic su **gestire endpoint** nella parte inferiore di hello del portale di servizi Web di Azure Machine Learning di hello dashboard tooopen hello.
* toodelete un endpoint (è possibile eliminare endpoint "Predefinita" hello), fare clic sulla casella di controllo hello all'inizio di hello della riga di endpoint hello e fare clic su **eliminare**. Per rimuovere endpoint hello dal servizio Web hello.
  
  > [!NOTE]
  > Se un'applicazione sta utilizzando l'endpoint del servizio web hello quando viene eliminato l'endpoint di hello, un'applicazione hello riceverà hello un errore successivo tentativo servizio hello tooaccess.
  > 
  > 

Fare clic sul nome di un tooopen di endpoint servizio Web hello è. 

Dal dashboard di hello, è possibile visualizzare l'utilizzo complessivo del servizio Web in un periodo di tempo. È possibile selezionare tooview periodo hello dal menu a discesa periodo hello in alto a destra hello di grafici relativi all'utilizzo di hello. dashboard di Hello Mostra hello le seguenti informazioni:

* **Le richieste nel tempo** Visualizza un grafico di passaggio del numero di hello di richieste su hello periodo di tempo selezionato. Può aiutare a identificare se si verificano picchi di utilizzo.
* **Le richieste di richiesta-risposta** Visualizza hello il numero totale di chiamate richiesta-risposta ricevuta dal servizio hello hello periodo di tempo selezionato e quanti di essi non riusciti.
* **Tempo medio di richiesta-risposta calcolo** consente di visualizzare una media di tempo hello necessari tooexecute hello ricevuto richieste.
* **Batch di richieste** hello Visualizza il numero totale di servizio hello richieste Batch ha ricevuto tramite hello periodo di tempo selezionato e quanti di essi non riusciti.
* **Processo latenza media** consente di visualizzare una media di tempo hello necessari tooexecute hello ricevuto richieste.
* **Errori** Visualizza hello aggregazione del numero di errori che si sono verificati nel servizio web toohello di chiamate.
* **I costi dei servizi** hello spese per il piano di fatturazione hello associato hello servizio vengono visualizzate.

Dalla pagina Configura hello, è possibile aggiornare hello le proprietà seguenti:

* **Descrizione** consente tooenter una descrizione per il servizio Web hello. La descrizione è un campo obbligatorio.
* **Registrazione** consente errore tooenable o disabilitare la registrazione su endpoint hello. Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).
* **Abilita dati di esempio** consente tooprovide dati di esempio che è possibile utilizzare il servizio di richiesta-risposta hello tootest. Se si crea servizio web hello in Machine Learning Studio, i dati di esempio hello viene recuperati dal dati hello il tootrain utilizzato il modello. Se è stato creato a livello di codice servizio hello, dati hello viene eseguiti da dati di esempio hello forniti come parte del pacchetto di hello JSON.

