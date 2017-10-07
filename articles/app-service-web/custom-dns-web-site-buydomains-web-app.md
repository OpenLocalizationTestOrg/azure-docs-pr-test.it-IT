---
title: aaaBuy un nome di dominio personalizzato per le app Web di Azure
description: Informazioni su come assegnare un nome toobuy un dominio personalizzato con un'app web nel servizio App di Azure.
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Acquistare un nome di dominio personalizzato per app Web Azure

I domini del servizio app (anteprima) sono i domini di primo livello che sono gestiti direttamente in Azure. Rendono i domini personalizzati toomanage semplice [App Web di Azure](app-service-web-overview.md). Questa esercitazione viene illustrato come un dominio di servizio App toobuy e assegnare DNS nomi tooAzure Web App.

Questo articolo è per il Servizio app di Azure (app Web, app per le API, app per dispositivi mobili, app per la logica). Per una macchina virtuale di Azure o archiviazione di Azure, vedere [tooAzure dominio assegnare App servizio macchina virtuale o archiviazione di Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/). Per i servizi cloud, vedere [Configurazione di un nome di dominio personalizzato per un servizio cloud di Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

* [Creare un'app del servizio app](/azure/app-service/) oppure usare un'app creata per un'altra esercitazione.

## <a name="prepare-hello-app"></a>Preparare l'applicazione hello

i domini personalizzati toouse in App Web di Azure, l'app web [piano di servizio App](https://azure.microsoft.com/pricing/details/app-service/) deve essere un livello a pagamento (**Shared**, **base**, **Standard**, o **Premium**). In questo passaggio è assicurarsi che Hello web app è in hello supportato piano tariffario.

### <a name="sign-in-tooazure"></a>Accedi tooAzure

Aprire hello [portale di Azure](https://portal.azure.com) e accedere con l'account di Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Passare toohello app nel portale di Azure hello

Scegliere dal menu a sinistra hello **servizi App**e quindi selezionare il nome di hello di app hello.

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

Verrà visualizzata hello pagina di gestione di app del servizio App hello.  

### <a name="check-hello-pricing-tier"></a>Controllo hello piano tariffario

Hello navigazione della pagina dell'app hello a sinistra, scorrere toohello **impostazioni** sezione e selezionare **scalabilità verticale (piano di servizio App)**.

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

livello corrente dell'applicazione Hello è evidenziato da un bordo blu. Verificare che tale applicazione hello non hello toomake **libero** livello. DNS personalizzato non è supportato in hello **libero** livello. 

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Se hello piano di servizio App non è **libero**, chiudere hello **scegliere il piano tariffario** pagina e andare troppo[dominio hello acquistare](#buy-the-domain).

### <a name="scale-up-hello-app-service-plan"></a>Applicare la scalabilità verticale hello piano di servizio App

Selezionare uno dei livelli di hello non disponibili (**Shared**, **base**, **Standard**, o **Premium**). 

Fare clic su **Seleziona**.

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Quando viene visualizzata hello previa notifica, l'operazione di ridimensionamento hello è stata completata.

![Conferma operazione di scalabilità](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Acquisto di hello dominio

### <a name="sign-in-tooazure"></a>Accedi tooAzure
Aprire hello [portale di Azure](https://portal.azure.com/) e accedere con l'account di Azure.

### <a name="launch-buy-domains"></a>Avvio di Acquistare un dominio
In hello **App Web** scheda, fare clic sul nome dell'app web, selezionare hello **impostazioni**, quindi selezionare **i domini personalizzati**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

In hello **i domini personalizzati** pagina, fare clic su **acquistare domini**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Configurare l'acquisto di dominio hello

In hello **dominio del servizio App** pagina hello **Cerca dominio** casella, si desidera toobuy e tipo di nome di dominio di tipo hello `Enter`. Hello suggeriti i domini disponibili vengono visualizzati sotto la casella di testo hello. Selezionare uno o più domini che si desidera toobuy. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Fare clic su hello **informazioni di contatto** e compilare il modulo di informazioni di contatto del dominio hello. Al termine, fare clic su **OK** pagina di tooreturn toohello dominio del servizio App.
   
È molto importante compilare tutti i campi obbligatori con la massima correttezza possibile. Domini di errore toopurchase possono generare dati non corretti per le informazioni di contatto. 

Successivamente, selezionare le opzioni di hello desiderato per il dominio. Vedere hello spiegazioni nella tabella seguente:

| Impostazione | Valore consigliato | Descrizione |
|-|-|-|
|Rinnovo automatico | **Abilitazione** | Rinnova il dominio del servizio App automaticamente ogni anno. Viene addebitata sulla carta di credito hello stesso prezzo di acquisto in fase di hello del rinnovo. |
|Protezione della privacy | Abilita | Consente di partecipare troppo "Protezione", che è incluso nel prezzo di acquisto hello _gratuitamente_ (ad eccezione di domini di primo livello cui Registro di sistema non supporta la protezione della privacy, ad esempio _. co.in_, _. Co.uk_e così via). |
| Assegnare i nomi host predefiniti | **www** e **@** | Seleziona hello desiderato le associazioni nome host, se necessario. Una volta completata l'operazione di acquisto hello dominio, l'app web accessibili in nomi host hello selezionato. Se l'applicazione web hello è protetto da [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), non viene visualizzato il dominio radice hello di hello opzione tooassign (@), perché Gestione traffico non non supporto un record. È possibile apportare modifiche toohello hostname assegnazioni al termine dell'acquisto dominio hello. |

### <a name="accept-terms-and-purchase"></a>Accettare i termini di acquisto

Fare clic su **legali** termini hello tooreview hello spese e, quindi fare clic su **acquistare**.

> [!NOTE]
> I domini del servizio App utilizzano domini di hello toohost di DNS di Azure. Inoltre toohello tassa di registrazione di dominio, si applicano gli addebiti di utilizzo per DNS di Azure. Per altre informazioni, vedere la pagina relativa ai [prezzi del DNS di Azure](https://azure.microsoft.com/pricing/details/dns/).
>
>

In hello **dominio del servizio App** pagina, fare clic su **OK**. Durante l'operazione di hello è in corso, vedrai hello seguendo le notifiche:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>Nomi host hello di test

Se è stato assegnato l'impostazione predefinita i nomi host tooyour web app, è inoltre possibile visualizzare una notifica di esito positivo per ogni nome di host selezionati. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

È inoltre visualizzare i nomi host hello selezionato in hello **i domini personalizzati** pagina hello **i nomi host** sezione. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

i nomi host hello tootest, passare i nomi host toohello elencato nel browser hello. Nell'esempio hello in hello precedente schermata, tenta di spostarsi too_kontoso.net_ e _www.kontoso.net_.

## <a name="assign-hostnames-tooweb-app"></a>Assegnare i nomi host tooweb app

Se si sceglie di non tooassign uno o più nomi host tooyour web app predefinita hello durante il processo di acquisto, o se è necessario un nome host tooassign non elencati, è possibile assegnare un nome host in qualsiasi momento.

È inoltre possibile assegnare i nomi host negli hello dominio del servizio App tooany altre app web. Hello passaggi variano a seconda se hello dominio del servizio App e app web hello appartengono toohello stessa sottoscrizione.

- Sottoscrizione diversa: eseguire il mapping di record DNS personalizzati dall'app web di hello dominio del servizio App toohello Analogamente a un dominio esternamente acquistato. Per informazioni sull'aggiunta di DNS personalizzato dei nomi di dominio del servizio App tooan, vedere [gestire i record DNS personalizzati](#custom). toomap un'app web tooa dominio acquistate esterno, vedere [mappare un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md). 
- Stessa sottoscrizione: hello utilizzare alla procedura seguente.

### <a name="launch-add-hostname"></a>Avviare Aggiungi nome host
In hello **servizi App** pagina, il nome di hello selezionare dell'app web che si desidera tooassign nomi host, selezionare **impostazioni**, quindi selezionare **i domini personalizzati**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Assicurarsi che il dominio acquistato sia elencato in hello **domini del servizio App** sezione senza selezionarla. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Tutti i domini di servizio App hello nella stessa sottoscrizione dell'app web hello **i domini personalizzati** pagina. Se il dominio è nella sottoscrizione dell'app web hello, ma non è possibile visualizzare in app web hello **i domini personalizzati** pagina, provare a riaprire hello **i domini personalizzati** pagina o aggiornare la pagina Web hello. Controllare inoltre a campana hello notifica nella parte superiore di hello di hello portale di Azure per gli errori di creazione o lo stato di avanzamento.
>
>

Selezionare **Aggiungi il nome host**.

### <a name="configure-hostname"></a>Configurare il nome host
In hello **aggiungere hostname** finestra di dialogo, hello dominio completo del tipo il dominio del servizio App o un sottodominio. ad esempio:

- kontoso.net
- www.kontoso.net
- abc.kontoso.net

Al termine, selezionare **Convalida**. tipo di record hostname Hello viene selezionato automaticamente.

Selezionare **Aggiungi il nome host**.

Quando l'operazione di hello è stata completata, viene visualizzata una notifica di esito positivo per hello assegnato il nome host.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Chiudere Aggiungi il nome host
In hello **aggiungere hostname** pagina, assegnare a qualsiasi altra nome host tooyour app web, in base alle esigenze. Al termine, chiudere hello **aggiungere hostname** pagina.

Dovrebbe essere hostname(s) hello appena assegnato dell'app **i domini personalizzati** pagina.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>Nomi host hello di test

Passare i nomi host toohello elencato nel browser hello. Nell'esempio hello nella precedente schermata hello, provare a passare too_abc.kontoso.net_.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Gestire i record DNS personalizzati

In Azure, i record DNS per un dominio del servizio app vengono gestiti tramite [DNS di Azure](https://azure.microsoft.com/services/dns/). È possibile aggiungere, rimuovere e aggiornare i record DNS, esattamente come per un dominio acquistato esternamente.

### <a name="open-app-service-domain"></a>Aprire Dominio del servizio app

Nel portale di Azure, dal menu a sinistra di hello, hello selezionare **più servizi** > **domini del servizio App**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Selezionare toomanage dominio hello. 

### <a name="access-dns-zone"></a>Accesso alla Zona DNS

Nel menu a sinistra del dominio hello, selezionare **zona DNS**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Questa azione apre hello [zona DNS](../dns/dns-zones-records.md) pagina del servizio App dominio in DNS di Azure. Per informazioni su come i record DNS tooedit, vedere [come zone DNS toomanage hello Azure portal](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>Annullare l'acquisto (elimina dominio)

Dopo aver acquistato hello dominio dell'applicazione del servizio, è necessario toocancel cinque giorni l'acquisto per un rimborso completo. Dopo cinque giorni, è possibile eliminare hello dominio del servizio App, ma non è possibile ricevere un rimborso.

### <a name="open-app-service-domain"></a>Aprire Dominio del servizio app

Nel portale di Azure, dal menu a sinistra di hello, hello selezionare **più servizi** > **domini del servizio App**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Selezionare hello dominio tooyou desidera toocancel o eliminare. 

### <a name="delete-hostname-bindings"></a>Eliminare associazioni nome host

Nel menu a sinistra del dominio hello, selezionare **le associazioni nome host**. le associazioni nome host Hello da tutti i servizi Azure sono elencate di seguito.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

È possibile eliminare hello dominio dell'applicazione del servizio vengono eliminate tutte le associazioni nome host.

Eliminare le associazioni nome host selezionando **...** > **Elimina**. Dopo l'eliminazione di tutte le associazioni hello, selezionare **salvare**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>Annullare o eliminare

Nel menu a sinistra del dominio hello, selezionare **Panoramica**. 

Se il periodo di annullamento hello sul dominio hello acquistato non è trascorso, selezionare **annullare acquisto**. In caso contrario, viene visualizzato il pulsante **Elimina**. dominio hello toodelete senza restituzione, seleziona **eliminare**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Selezionare **OK** operazione hello tooconfirm. Se non si desidera tooproceed, fare clic all'esterno di finestra di dialogo Conferma hello.

Una volta completata l'operazione di hello, dominio hello è stato rilasciato dalla sottoscrizione e disponibile per tutti gli utenti toopurchase nuovamente. 
