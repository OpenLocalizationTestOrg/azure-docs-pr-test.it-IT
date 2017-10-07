---
title: aaaHow toouse l'abbonamento a Office 365 con Azure RemoteApp | Documenti Microsoft
description: Informazioni su come usare la sottoscrizione a Office 365 in Azure RemoteApp tooshare Office app.
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: f82b6e23-2b71-47be-846d-fd93f2652f3c
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2648868dd28cbcd93e38461ae6dce25eaa5d5e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-your-office-365-subscription-with-azure-remoteapp"></a>Come toouse l'abbonamento a Office 365 con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Non tutti sanno che è possibile utilizzare la sottoscrizione di Office 365 esistente in Azure RemoteApp tooshare Office App cloud hello. Continuare a leggere per informazioni sull'Office 365 + opzioni di Azure RemoteApp, inclusi collegamenti tooarticles su Office 365 che consentono di rendere più hello della sottoscrizione.

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>Utilizzo di account di Office 365 per Azure RemoteApp
Estrarre nuovo articolo di Peter per tutte le informazioni di hello: [come toouse Azure RemoteApp con gli account utente di Office 365](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-toorun-office-applications-in-azure-remoteapp"></a>È possibile utilizzare le applicazioni di Office toorun sottoscrizione Office 365 in Azure RemoteApp?
È possibile usarlo. Infatti, tramite l'abbonamento a Office 365 è hello solo modo toobring il tooAzure di applicazioni di Office RemoteApp.

(Nota: se la distribuzione di Azure RemoteApp è fornita un partner di hosting, questi possono essere in grado di tooprovide con licenze di Office in base a un [contratto di licenza per Provider del servizio](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx))

cosa più interessante l'abbonamento a Office 365 Hello è che consente di utilizzare hello stesso licenza utente per le diverse piattaforme e ambienti, tra cui hello cloud di Azure. Quando si usano applicazioni di Office in Azure RemoteApp non necessario toopurchase ulteriori licenze o configurare le licenze esistenti in alcun modo particolare. È sufficiente disporre di una sottoscrizione di Office 365 che includa [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx).

Office 365 ProPlus consente l'[attivazione di computer condivisi](https://technet.microsoft.com/library/Dn782860.aspx). Questa funzionalità consente l'attivazione temporanea basata sugli utenti per Office in ambienti cloud e virtuali quali Azure RemoteApp e Servizi Desktop remoto.

Piani di Office 365 che includono Office 365 ProPlus Estrarre hello [disponibilità all'interno di ogni piano di servizio](https://technet.microsoft.com/library/office-365-plan-options.aspx) tabella. Si noti che non tutti i piani dispongono di Office 365 ProPlus (ad esempio, piano di Office 365 Business hello). Se il piano, non è consigliabile effettuare l'aggiornamento piano tooa che esegue (ad esempio, Office 365 Education E3).

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>Uso delle licenze di Office 365 ProPlus con Azure RemoteApp
Ogni licenza utente per Office 365 ProPlus consente a un singolo utente di attivare applicazioni di Office nel computer too5 plus Tablet e telefoni. Ogni attivazione è registrato con utente hello fino a quando non si disattiva Office sul dispositivo hello. (Gli utenti possono gestire i dispositivi in hello [portale di Office 365](https://portal.office365.com/).)

Con Azure RemoteApp un singolo utente può accedere a diversi computer hello stesso giorno inavvertitamente. Ciò avviene perché il servizio hello ridimensiona le risorse nel cloud hello, mentre l'utente di hello Visualizza solo le app di hello e programmi che è stato condiviso e gestisce automaticamente. Per questo scenario di Office 365 ProPlus offre una modalità di attivazione di un computer condiviso, questo significa che l'utente non deve necessariamente toodo qualsiasi tooaccess gestione licenze tali risorse e che i singoli computer hello non vengono conteggiate nel limite di attivazione di hello 5 computer.

Come è (salve) assegnare licenze di Office 365 ProPlus tooyour gli utenti, può usano Office dai propri dispositivi personali, nonché tramite la raccolta di Azure RemoteApp.

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>Applicazioni di Office che possono essere usate con Office 365 e Azure RemoteApp
È possibile utilizzare il tooactivate sottoscrizione Office 365 e condivisione di Office 2013 in distribuzioni di Azure RemoteApp. È attualmente non supportano hello utilizzo di altre versioni di Office con Azure RemoteApp. Le versioni non supportate sono quindi Office 2003, Office 2007, Office 2010 e Office 2016.

## <a name="what-about-visio-pro-or-project-pro"></a>Informazioni su Visio Pro o Project Pro
immagine di Office 365 ProPlus Hello inclusi nella sottoscrizione di RemoteApp include Visio Pro e progetto Pro. Ma è possibile usare il tooactivate sottoscrizione Office 365 ProPlus tali programmi, hanno la propria licenza. È possibile attivarli in hello [portale di Office 365](https://portal.office365.com/). 

Non è toolicense questi programmi se non si desidera toouse li. Attivare solo i programmi di hello toouse - desiderato e ignorare hello altri. Verrà comunque visualizzato nell'immagine di hello, ma non possono essere utilizzati. 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>Informazioni introduttive su Office 365 e Azure RemoteApp
Ora che si conoscono i dettagli di hello delle licenze di Office 365, è possibile iniziare a utilizzarlo in Azure RemoteApp - è molto semplice:

Quando si crea la raccolta RemoteApp di Azure, utilizzare hello **Office 365 ProPlus (è necessaria la sottoscrizione)** immagine.

![Immagine di Azure RemoteApp con Office 365 Pro Plus](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

Questa immagine contiene più recente di Windows Server e Office 365 ProPlus hello. Dopo la configurazione della raccolta (incluse le app di pubblicazione), gli utenti dovranno semplicemente accedere ad Azure RemoteApp usando il proprio client RemoteApp e specificare le proprie credenziali di Office 365 per le app di Office. Le licenze vengono recapitate automaticamente, senza necessità di configurazione o gestione.

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>Possibilità di creare un'immagine personalizzata con Office 365 ProPlus
È possibile creare un'immagine personalizzata per la raccolta che contiene Office 365 ProPlus. Sono disponibili 2 opzioni: utilizzare hello Azure galleria che forniamo oppure è possibile creare un'immagine personalizzata e installare Office 365 ProPlus non esiste.

### <a name="use-hello-azure-gallery-image"></a>Utilizzare l'immagine della raccolta di Azure hello
toodeploy modo più semplice di Hello raccolta tooa Office 365 ProPlus è troppo[iniziare con una delle immagini della raccolta di Azure hello](remoteapp-image-on-azurevm.md) incluso nella sottoscrizione Azure RemoteApp. Assicurarsi di scegliere hello **Windows Server Host sessione Desktop remoto con Office 365 ProPlus pre-installato** immagine. Quindi, installare le app da tale immagine e l'ora è toogo.

### <a name="use-a-custom-image"></a>Usare un'immagine personalizzata
È sempre possibile creare un'immagine personalizzata, è possibile creare un [macchina virtuale di Azure](remoteapp-image-on-azurevm.md) o [creare hello immagine localmente](remoteapp-create-custom-image.md) e caricarlo tooAzure. In entrambi i casi, assicurarsi di installare Office 365 ProPlus tramite hello computer condiviso attivazione del nodo. Hello utilizzare [strumento di distribuzione di Office](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx) e seguire hello [istruzioni](https://technet.microsoft.com/library/Dn782858.aspx) per l'installazione.  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>Disabilitare gli aggiornamenti automatici per Office 365 ProPlus nell'immagine personalizzata. IMPORTANTE
L'immagine personalizzata viene utilizzato come modello per l'aggiunta di risorse aggiuntive come richiesta hello dall'aumento di utenti da Azure RemoteApp. tooprevent ritardi e i problemi di connessione, disabilitare gli aggiornamenti automatici per Office nell'immagine di hello. In caso contrario, ogni risorsa creata con tale modello verrà aggiornata automaticamente all'avvio. Utilizzare invece il processo di Azure RemoteApp standard hello per l'aggiornamento di un'immagine personalizzata. In questo modo si aggiorna le applicazioni di Office hello su immagine modello hello e quindi fare in modo che Azure RemoteApp ottenere gli aggiornamenti di hello tooyour utenti.

toodisable aggiornamenti automatici, aggiungere i seguenti file di configurazione dello strumento di distribuzione di Office toohello hello:

        <Updates Enabled="FALSE" />

Il file di configurazione dovrebbe ora includere le righe seguenti:

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>Modalità di aggiornamento di un'immagine con Office 365 ProPlus
Sono disponibili immagini di molti motivi tooupdate hello nella raccolta. tra cui i seguenti:

* Ottenere gli aggiornamenti Windows più recenti di hello 
* Ottenere hello aggiornamenti più recenti dell'applicazione di Office 365 ProPlus
* Aggiornare l'app personalizzata
* Modificare altre impostazioni di configurazione per l'immagine di hello stessa

Per passaggi di hello end-to-end per l'aggiornamento dell'immagine di hello toouse raccolta è stato aggiornato, visitare [qui](remoteapp-update.md). Ma per informazioni su come tooupdate hello immagine e Office 365 ProPlus, consultare le seguenti informazioni hello.

È possibile aggiornare l'immagine in due modi, ovvero sostituendo l'immagine con un'immagine completamente nuova oppure aggiornando l'immagine esistente.

### <a name="replace-your-image-with-hello-latest-azure-gallery-image--add-customizations"></a>Sostituire l'immagine con l'immagine della raccolta di Azure più recenti hello + Aggiungi personalizzazioni
Con questa opzione fare in modo che Microsoft degli aggiornamenti di Windows Server e Office 365 ProPlus hello. Anziché aggiornare l'immagine esistente, si creerà un'immagine completamente nuova basata su immagine della raccolta hello più recente. Ripetere i passi in precedenza un'immagine di hello toocustomize: installare App personalizzate, modificare Configurazione immagine hello e così via.

le immagini della Galleria Hello vengano regolarmente aggiornate, pertanto è possibile posizionare facile e sapere che le app di Windows Server e Office 365 ProPlus sono backup toodate. Naturalmente, compromesso hello è che è necessario tooapply le personalizzazioni ogni volta che si ottiene una nuova immagine. È possibile creare script tooautomate impostando le personalizzazioni.

### <a name="manually-update-your-existing-image"></a>Aggiornare manualmente l'immagine esistente
Con questa opzione, si utilizza immagine toohello standard Windows strumenti tooapply gli aggiornamenti. Per Office 365 ProPlus, utilizzare toodownload strumento di distribuzione di Office hello e installare gli aggiornamenti più recenti di hello o le versioni di Office 365 ProPlus.

> [!IMPORTANT]
> Nota: disabilitare gli aggiornamenti automatici di Office 365 ProPlus hello.
> 
> 

Per ulteriori informazioni sull'utilizzo di hello strumento di distribuzione di Office per gli aggiornamenti,

* [Distribuire a portata di clic per i prodotti Office 365 tramite hello strumento di distribuzione di Office](https://technet.microsoft.com/library/JJ219423.aspx)
* [Distribuzione e l'aggiornamento di Office 365 ProPlus tramite lo strumento di distribuzione di Office di hello](https://channel9.msdn.com/Events/Ignite/2015/BRK3168) (video)
* [Configurare le impostazioni di aggiornamento di Office 365 ProPlus](https://technet.microsoft.com/library/dn761708.aspx)

