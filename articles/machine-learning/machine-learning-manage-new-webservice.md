---
title: portale di servizi Web di Azure Machine Learning hello aaaUse | Documenti Microsoft
description: Gestire aree di lavoro di accesso tooAzure Machine Learning, distribuire e gestire i servizi web API ML
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>Gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello
È possibile gestire i servizi Web classico e il Machine Learning nuovo tramite il portale di servizi Web di Microsoft Azure Machine Learning hello. Poiché i servizi Web classici e nuovi sono basati su tecnologie diverse, sono disponibili funzionalità di gestione leggermente diverse.

Nel portale di servizi Web di Machine Learning hello è possibile:

* Monitorare l'utilizzo di servizio web hello.
* Configurare una descrizione di hello, aggiornare le chiavi di hello per il web hello (solo nuovo) del servizio, l'archiviazione account chiave (solo nuova), attivare la registrazione, aggiornare e attivare o disabilitare i dati di esempio.
* Eliminare il servizio web hello.
* Creare, eliminare o aggiornare i piani di fatturazione (solo servizi nuovi).
* Aggiungere ed eliminare gli endpoint (solo servizi classici)

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>Autorizzazioni toomanage nuovo gestore di risorse basato su servizi web

I nuovi servizi Web vengono distribuiti come risorse di Azure. Di conseguenza, è necessario avere toodeploy delle autorizzazioni corrette hello e gestire nuovi servizi web.  toodeploy o gestire i nuovi servizi web, è necessario disporre di un collaboratore o il ruolo di amministratore nel servizio web di hello sottoscrizione toowhich hello viene distribuito. Se si invita a un'altra macchina di tooa utente apprendimento dell'area di lavoro, è necessario assegnare loro ruolo di collaboratore o amministratore tooa sottoscrizione hello prima di poter distribuire o gestire i servizi web. 

Se hello insufficienti hello correggere risorse tooaccess autorizzazioni nel portale di servizi Web di Azure Machine Learning hello, riceveranno il seguente errore durante il tentativo di un servizio web toodeploy hello:

*Web Service deployment failed. Questo account non dispone di sufficienti accesso toohello sottoscrizione di Azure che contiene hello dell'area di lavoro. Toodeploy tooAzure un servizio Web, hello stesso account deve essere invitati toohello dell'area di lavoro ed essere toohello di accesso specificata sottoscrizione di Azure che contiene hello dell'area di lavoro.*

Per altre informazioni sulla creazione di un'area di lavoro, vedere [Creare e condividere un'area di lavoro di Azure Machine Learning](machine-learning-create-workspace.md).

Per ulteriori informazioni sull'impostazione delle autorizzazioni di accesso, vedere [visualizzare le assegnazioni di accesso per utenti e gruppi nel portale di Azure - anteprima pubblica di hello](../active-directory/role-based-access-control-manage-assignments.md).


## <a name="manage-new-web-services"></a>Gestire i nuovi servizi Web
toomanage i servizi Web di nuovo:

1. Accedi toohello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) hello di portale utilizzando l'account di Microsoft Azure - Usa account hello associato alla sottoscrizione di Azure.
2. Scegliere dal menu hello **servizi Web**.

Verrà visualizzato un elenco di servizi Web distribuiti per la sottoscrizione. 

toomanage un servizio Web, fare clic su servizi Web. Dalla pagina Web Services hello è possibile:

* Fare clic su hello web servizio toomanage è.
* Fare clic su hello piano di fatturazione per hello web servizio tooupdate è.
* Eliminare un servizio Web.
* Copiare un servizio web e distribuirlo tooanother area.

Quando si fa clic su un servizio web, verrà visualizzata la pagina avvio rapido del servizio web di hello. pagina di avvio rapido del servizio web Hello è disponibili due opzioni di menu che consentono di toomanage il servizio web:

* **DASHBOARD** -consente l'utilizzo di servizi Web tooview.
* **Configura** : consente un testo descrittivo tooadd, chiave hello di aggiornamento per account di archiviazione hello associati hello al servizio Web e abilitare o disabilitare i dati di esempio.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Monitoraggio utilizzo servizio web hello
Fare clic su hello **DASHBOARD** scheda.

Dal dashboard di hello, è possibile visualizzare l'utilizzo complessivo del servizio Web in un periodo di tempo. È possibile selezionare tooview periodo hello dal menu a discesa periodo hello in alto a destra hello di grafici relativi all'utilizzo di hello. dashboard di Hello Mostra hello le seguenti informazioni:

* **Le richieste nel tempo** Visualizza un grafico di passaggio del numero di hello di richieste su hello periodo di tempo selezionato. Può aiutare a identificare se si verificano picchi di utilizzo.
* **Le richieste di richiesta-risposta** Visualizza hello il numero totale di chiamate richiesta-risposta ricevuta dal servizio hello hello periodo di tempo selezionato e quanti di essi non riusciti.
* **Tempo medio di richiesta-risposta calcolo** consente di visualizzare una media di tempo hello necessari tooexecute hello ricevuto richieste.
* **Batch di richieste** hello Visualizza il numero totale di servizio hello richieste Batch ha ricevuto tramite hello periodo di tempo selezionato e quanti di essi non riusciti.
* **Processo latenza media** consente di visualizzare una media di tempo hello necessari tooexecute hello ricevuto richieste.
* **Errori** Visualizza hello aggregazione del numero di errori che si sono verificati nel servizio web toohello di chiamate.
* **I costi dei servizi** hello spese per il piano di fatturazione hello associato hello servizio vengono visualizzate.

### <a name="configuring-hello-web-service"></a>Configurazione del servizio web hello
Fare clic su hello **configura** opzione di menu.

È possibile aggiornare hello le proprietà seguenti:

* **Descrizione** consente tooenter una descrizione per il servizio Web hello.
* **Titolo** consente tooenter un titolo per hello servizio Web
* **Le chiavi** consente toorotate le chiavi API primarie e secondarie.
* **Chiave dell'account di archiviazione** consente tooupdate hello chiave hello account di archiviazione associato le modifiche del servizio Web di hello. 
* **Abilita dati di esempio** consente tooprovide dati di esempio che è possibile utilizzare il servizio di richiesta-risposta hello tootest. Se si crea servizio web hello in Machine Learning Studio, i dati di esempio hello viene recuperati dal dati hello il tootrain utilizzato il modello. Se è stato creato a livello di codice servizio hello, dati hello viene eseguiti da dati di esempio hello forniti come parte del pacchetto di hello JSON.

### <a name="managing-billing-plans"></a>Gestione dei piani di fatturazione
Fare clic su hello **piani** opzione di menu dalla pagina Guida introduttiva di servizi web di hello. È anche possibile scegliere il piano di hello associato specifico toomanage servizio Web che prevede.

* **Nuovo** consente toocreate un nuovo piano.
* **Istanza del piano di installazione** consente troppo "scalabilità" una capacità di tooadd piano esistente.
* **Aggiornamento/DownGrade** consente troppo "scalabilità" una capacità di tooadd piano esistente.
* **Eliminare** consente toodelete un piano.

Fare clic su un piano tooview relativo dashboard. dashboard Hello fornisce snapshot o piano di utilizzo in un periodo di tempo selezionato. tooselect hello tooview periodo di tempo, fare clic su hello **periodo** elenco a discesa in alto a destra hello del dashboard. 

dashboard del piano Hello fornisce hello le seguenti informazioni:

* **Pianificare la descrizione** consente di visualizzare informazioni sui costi hello e sulla capacità associati hello piano.
* **Pianificare l'utilizzo** Visualizza il numero di hello delle transazioni e le ore di calcolo addebitato rispetto ai piani di hello.
* **Servizi Web** Visualizza il numero di hello di servizi Web che utilizzano questo piano.
* **Le prime da chiamate del servizio Web** Visualizza hello principali quattro servizi che stanno effettuando chiamate addebitato rispetto ai piani di hello.
* **I primi servizi Web per ore di calcolo** Visualizza hello principali quattro servizi che utilizzano risorse di calcolo addebitato rispetto ai piani di hello.

## <a name="manage-classic-web-services"></a>Gestire i servizi Web classici
> [!NOTE]
> procedure di Hello in questa sezione sono i servizi web classica toomanaging rilevanti tramite il portale di servizi Web di Azure Machine Learning hello. Per informazioni sulla gestione classico Web services tramite Machine Learning Studio hello e hello Azure classico portale, vedere [gestire un'area di lavoro di Azure Machine Learning](machine-learning-manage-workspace.md).
> 
> 

toomanage i servizi Web classico:

1. Accedi toohello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) hello di portale utilizzando l'account di Microsoft Azure - Usa account hello associato alla sottoscrizione di Azure.
2. Scegliere dal menu hello **classico servizi Web**.

Fare clic su un servizio Web classico, toomanage **classico servizi Web**. Dalla pagina di hello Classic servizi Web, è possibile:

* Fare clic su endpoint hello associata tooview del servizio web hello.
* Eliminare un servizio Web.

Quando si gestisce un servizio Web classico, gestire ognuno degli endpoint hello separatamente. Quando si fa clic su un servizio web nella pagina servizi Web hello, verrà visualizzato l'elenco di hello di endpoint associati al servizio hello. 

Nella pagina di endpoint servizio Web classico hello, è possibile aggiungere ed eliminare gli endpoint servizio hello. Per altre informazioni sull'aggiunta di endpoint, vedere [Creazione di endpoint](machine-learning-create-endpoint.md).

Fare clic su uno della pagina di avvio rapido di hello endpoint tooopen hello web del servizio. Nella pagina avvio rapido di hello, esistono due opzioni di menu che consentono di toomanage il servizio web:

* **DASHBOARD** -consente l'utilizzo di servizi Web tooview.
* **Configura** -consente un testo descrittivo tooadd, attivare la registrazione di errori e disattivare, chiave hello di aggiornamento per account di archiviazione hello associati hello al servizio Web, abilitare e disabilitare i dati di esempio.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Monitoraggio utilizzo servizio web hello
Fare clic su hello **DASHBOARD** scheda.

Dal dashboard di hello, è possibile visualizzare l'utilizzo complessivo del servizio Web in un periodo di tempo. È possibile selezionare tooview periodo hello dal menu a discesa periodo hello in alto a destra hello di grafici relativi all'utilizzo di hello. dashboard di Hello Mostra hello le seguenti informazioni:

* **Le richieste nel tempo** Visualizza un grafico di passaggio del numero di hello di richieste su hello periodo di tempo selezionato. Può aiutare a identificare se si verificano picchi di utilizzo.
* **Le richieste di richiesta-risposta** Visualizza hello il numero totale di chiamate richiesta-risposta ricevuta dal servizio hello hello periodo di tempo selezionato e quanti di essi non riusciti.
* **Tempo medio di richiesta-risposta calcolo** consente di visualizzare una media di tempo hello necessari tooexecute hello ricevuto richieste.
* **Batch di richieste** hello Visualizza il numero totale di servizio hello richieste Batch ha ricevuto tramite hello periodo di tempo selezionato e quanti di essi non riusciti.
* **Processo latenza media** consente di visualizzare una media di tempo hello necessari tooexecute hello ricevuto richieste.
* **Errori** Visualizza hello aggregazione del numero di errori che si sono verificati nel servizio web toohello di chiamate.
* **I costi dei servizi** hello spese per il piano di fatturazione hello associato hello servizio vengono visualizzate.

### <a name="configuring-hello-web-service"></a>Configurazione del servizio web hello
Fare clic su hello **configura** opzione di menu.

È possibile aggiornare hello le proprietà seguenti:

* **Descrizione** consente tooenter una descrizione per il servizio Web hello. La descrizione è un campo obbligatorio.
* **Registrazione** consente errore tooenable o disabilitare la registrazione su endpoint hello. Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).
* **Abilita dati di esempio** consente tooprovide dati di esempio che è possibile utilizzare il servizio di richiesta-risposta hello tootest. Se si crea servizio web hello in Machine Learning Studio, i dati di esempio hello viene recuperati dal dati hello il tootrain utilizzato il modello. Se è stato creato a livello di codice servizio hello, dati hello viene eseguiti da dati di esempio hello forniti come parte del pacchetto di hello JSON.

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>Concedere o sospendere l'accesso tooWeb servizi per gli utenti nel portale di hello
Utilizza hello portale di Azure classico, è possibile consentire o negare l'accesso agli utenti di toospecific.

### <a name="access-for-users-of-new-web-services"></a>Accesso per gli utenti dei nuovi servizi Web
tooenable toowork altri utenti con i servizi Web nel portale di servizi Web di Azure Machine Learning hello, è necessario aggiungerli come co-amministratori nella sottoscrizione di Azure.

Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) utilizzo di Microsoft Azure account, utilizzare account hello associato hello sottoscrizione di Azure.

1. Nel riquadro di spostamento hello, fare clic su **impostazioni**, quindi fare clic su **amministratori**.
2. Nella parte inferiore di hello della finestra hello, fare clic su **Aggiungi**. 
3. Nella finestra di dialogo ADD A CO-ADMINISTRATOR hello, hello tipo indirizzo di posta elettronica della persona hello tooadd come coamministratore, quindi selezionare sottoscrizione hello che si desidera tooaccess CO-amministratore hello.
4. Fare clic su **Salva**.

### <a name="access-for-users-of-classic-web-services"></a>Accesso per gli utenti dei servizi Web classici
toomanage un'area di lavoro:

Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) utilizzo di Microsoft Azure account, utilizzare account hello associato hello sottoscrizione di Azure.

1. Nel Pannello di servizi di Microsoft Azure hello, fare clic su **MACHINE LEARNING**.
2. Fare clic su area di lavoro hello desiderato toomanage.
3. Fare clic su hello **configura** scheda.

Dalla scheda Configurazione hello, è possibile sospendere l'area di lavoro Machine Learning toohello access facendo **DENY**. Gli utenti non saranno in grado di tooopen dell'area di lavoro hello in Machine Learning Studio. accesso toorestore, fare clic su **Consenti**.

utenti toospecific:

toomanage altri account che dispongono di accesso dell'area di lavoro toohello in Machine Learning Studio, fare clic su **Accedi tooML Studio** in hello **DASHBOARD** scheda. Verrà visualizzata l'area di lavoro hello in Machine Learning Studio. Da qui, fare clic su hello **impostazioni** scheda e quindi **utenti**. È possibile fare clic su **INVITARE utenti più** toogive utenti accedere toohello area di lavoro, oppure selezionare un utente e fare clic su **rimuovere**.

> [!NOTE]
> Hello **Accedi tooML Studio** collegamento consente di aprire Machine Learning Studio usando l'Account Microsoft è stato eseguito l'accesso in hello. Hello Account Microsoft usato toosign in toohello toocreate portale Azure classico un'area di lavoro dispone automaticamente dell'autorizzazione tooopen area di lavoro. tooopen un'area di lavoro, è necessario essere connessi con Account Microsoft che è stato definito come proprietario di hello dell'area di lavoro hello toohello oppure è necessario un invito dall'area di lavoro di hello proprietario toojoin hello tooreceive.
> 
> 

