---
title: Come usare la sottoscrizione di Office 365 con Azure RemoteApp | Documentazione Microsoft
description: Informazioni su come usare la sottoscrizione di Office 365 in Azure RemoteApp per condividere app di Office.
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
ms.openlocfilehash: e58ee0444517074d6b756652d03fc79c2370e69e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-your-office-365-subscription-with-azure-remoteapp"></a>Come usare la sottoscrizione di Office 365 con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Non tutti sanno che è possibile usare la sottoscrizione di Office 365 in Azure RemoteApp per condividere le app di Office dal cloud. Di seguito sono disponibili informazioni sulle opzioni per Office 365 con Azure RemoteApp, inclusi collegamenti ad articoli relativi a Office 365 che consentono di sfruttare al meglio la sottoscrizione.

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>Utilizzo di account di Office 365 per Azure RemoteApp
Leggere il nuovo articolo di Peter per tutte le informazioni: [Come usare Azure RemoteApp con gli account utente di Office 365](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-to-run-office-applications-in-azure-remoteapp"></a>Posso usare la sottoscrizione di Office 365 per eseguire applicazioni di Office in Azure RemoteApp?
È possibile usarlo. L'uso della sottoscrizione di Office 365, in effetti, è l'unico modo per eseguire le applicazioni di Office in Azure RemoteApp.

Nota: se la distribuzione Azure RemoteApp viene eseguita da un partner di hosting, quest'ultimo potrebbe essere in grado di fornire licenze di Office in base a un programma [SPLA (Service Provider Licensing Agreement)](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx)

Uno dei vantaggi della sottoscrizione di Office 365 consiste nel fatto che consente di usare la stessa licenza utente su molte piattaforme diverse e molti ambienti diversi, incluso il cloud di Azure. Quando si usano le applicazioni di Office in Azure RemoteApp, non è necessario acquistare licenze aggiuntive o configurare le licenze esistenti in modo particolare. È sufficiente disporre di una sottoscrizione di Office 365 che includa [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx).

Office 365 ProPlus consente l'[attivazione di computer condivisi](https://technet.microsoft.com/library/Dn782860.aspx). Questa funzionalità consente l'attivazione temporanea basata sugli utenti per Office in ambienti cloud e virtuali quali Azure RemoteApp e Servizi Desktop remoto.

Piani di Office 365 che includono Office 365 ProPlus Verificare la tabella della [disponibilità dei servizi per ogni piano](https://technet.microsoft.com/library/office-365-plan-options.aspx). Si noti che non tutti i piani includono Office 365 ProPlus (ad esempio, il piano Office 365 Business). Se il piano non lo include, valutare l'aggiornamento a un piano che lo include, ad esempio Office 365 Education E3.

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>Uso delle licenze di Office 365 ProPlus con Azure RemoteApp
Ogni licenza utente per Office 365 ProPlus consente a un singolo utente di attivare le applicazioni di Office in un massimo di 5 computer, oltre a tablet e telefoni. Ogni attivazione viene registrata con l'utente fino alla disattivazione di Office nel dispositivo. Gli utenti possono gestire i propri dispositivi nel [portale di Office 365](https://portal.office365.com/).

Con RemoteApp di Azure un singolo utente può accedere in diversi computer nello stesso giorno inavvertitamente. Ciò avviene perché il servizio gestisce automaticamente e scala le risorse nel cloud, mentre l'utente visualizza solo le applicazioni e i programmi che sono stati condivisi. Per questo scenario Office 365 ProPlus offre una modalità di attivazione del computer condiviso - questo significa che l'utente non deve eseguire qualsiasi gestione della licenza per accedere a tali risorse e che i singoli computer non vengono conteggiati rispetto al limite di attivazione di 5 computer.

Se, in qualità di amministratore, si assegnano agli utenti licenze di Office 365 ProPlus, gli utenti potranno usare Office nei propri dispositivi personali, nonché tramite la raccolta di Azure RemoteApp.

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>Applicazioni di Office che possono essere usate con Office 365 e Azure RemoteApp
È possibile usare la sottoscrizione a Office 365 per attivare e condividere Office 2013 nelle distribuzioni di Azure RemoteApp. L'uso di altre versioni di Office con Azure RemoteApp non è attualmente supportato. Le versioni non supportate sono quindi Office 2003, Office 2007, Office 2010 e Office 2016.

## <a name="what-about-visio-pro-or-project-pro"></a>Informazioni su Visio Pro o Project Pro
L'immagine di Office 365 ProPlus inclusa nella sottoscrizione di RemoteApp offre sia Visio Pro che Project Pro. Non è tuttavia possibile usare la sottoscrizione di Office 365 ProPlus per attivare questi programmi. Per ogni programma è prevista una licenza specifica. È possibile attivare questi programmi nel [portale di Office 365](https://portal.office365.com/). 

Se non si prevede di usarli, non è necessario ottenere la licenza per questi programmi. È sufficiente attivare i programmi da usare e ignorare gli altri. I programmi verranno visualizzati comunque nell'immagine, ma non potranno essere usati. 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>Informazioni introduttive su Office 365 e Azure RemoteApp
Dopo avere ottenuto informazioni dettagliate sulle licenze per Office 365, è possibile iniziare a usarlo con facilità in Azure RemoteApp:

Quando si crea la raccolta di Azure RemoteApp, usare l'immagine di **Office 365 ProPlus (sottoscrizione necessaria)** .

![Immagine di Azure RemoteApp con Office 365 Pro Plus](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

Questa immagine contiene la versione più recente di Windows Server e Office 365 ProPlus. Dopo la configurazione della raccolta (incluse le app di pubblicazione), gli utenti dovranno semplicemente accedere ad Azure RemoteApp usando il proprio client RemoteApp e specificare le proprie credenziali di Office 365 per le app di Office. Le licenze vengono recapitate automaticamente, senza necessità di configurazione o gestione.

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>Possibilità di creare un'immagine personalizzata con Office 365 ProPlus
È possibile creare un'immagine personalizzata per la raccolta che contiene Office 365 ProPlus. Sono disponibili due opzioni, ovvero l'uso dell'immagine della raccolta di Azure fornita o la creazione di un'immagine predefinita e l'installazione di Office 365 ProPlus in tale immagine.

### <a name="use-the-azure-gallery-image"></a>Usare l'immagine della raccolta di Azure
Il modo più semplice per distribuire Office 365 ProPlus in una raccolta consiste nell' [iniziare con una delle immagini della raccolta di Azure](remoteapp-image-on-azurevm.md) incluse nella sottoscrizione di Azure RemoteApp. Assicurarsi di scegliere l'immagine relativa all' **host della sessione di Desktop remoto in Windows Server con Office 365 ProPlus preinstallato** . È quindi sufficiente installare eventuali altre app da includere nell'immagine.

### <a name="use-a-custom-image"></a>Usare un'immagine personalizzata
È sempre possibile creare un'immagine personalizzata, ovvero creare una [macchina virtuale di Azure](remoteapp-image-on-azurevm.md) o [creare l'immagine localmente](remoteapp-create-custom-image.md) e caricarla in Azure. In entrambi i casi, assicurarsi di installare Office 365 ProPlus usando il nodo di attivazione dei computer condivisi. Usare lo [Strumento di distribuzione di Office](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx) e seguire le [istruzioni](https://technet.microsoft.com/library/Dn782858.aspx) per l'installazione.  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>Disabilitare gli aggiornamenti automatici per Office 365 ProPlus nell'immagine personalizzata. IMPORTANTE
L'immagine personalizzata viene usata da Azure RemoteApp come modello per l'aggiunta di altre risorse per soddisfare l'incremento della domanda da parte degli utenti. Per evitare ritardi e problemi di connessione, disabilitare gli aggiornamenti automatici per Office nell'immagine. In caso contrario, ogni risorsa creata con tale modello verrà aggiornata automaticamente all'avvio. Usare invece il processo standard di Azure RemoteApp per l'aggiornamento dell'immagine personalizzata. Le applicazioni di Office verranno quindi aggiornate una volta nell'immagine del modello e gli aggiornamenti successivi verranno forniti automaticamente agli utenti da Azure RemoteApp.

Per disabilitare gli aggiornamenti automatici, aggiungere il file di configurazione seguente allo Strumento di distribuzione di Office:

        <Updates Enabled="FALSE" />

Il file di configurazione dovrebbe ora includere le righe seguenti:

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>Modalità di aggiornamento di un'immagine con Office 365 ProPlus
L'aggiornamento dell'immagine nella raccolta è necessario per molti motivi, tra cui i seguenti:

* Ottenere gli aggiornamenti Windows più recenti 
* Ottenere gli aggiornamenti più recenti per le applicazioni di Office 365 ProPlus
* Aggiornare l'app personalizzata
* Modificare altre impostazioni di configurazione per l'immagine stessa

Per le procedure end-to-end per l'aggiornamento della raccolta in modo che venga usata l'immagine aggiornata, vedere [questa pagina](remoteapp-update.md). Per informazioni su come aggiornare l'immagine e Office 365 ProPlus, vedere di seguito.

È possibile aggiornare l'immagine in due modi, ovvero sostituendo l'immagine con un'immagine completamente nuova oppure aggiornando l'immagine esistente.

### <a name="replace-your-image-with-the-latest-azure-gallery-image--add-customizations"></a>Sostituire l'immagine con l'immagine più recente della raccolta di Azure e aggiungere personalizzazioni
Questa opzione consente a Microsoft di eseguire automaticamente gli aggiornamenti di Windows Server e Office 365 ProPlus. Invece di aggiornare l'immagine esistente, verrà creata un'immagine completamente nuova basata sull'immagine più recente della raccolta. Sarà quindi necessario ripetere tutti i passaggi eseguiti in precedenza per personalizzare l'immagine, ovvero installare app personalizzate, modificare la configurazione dell'immagine e così via.

Le immagini della raccolta vengono aggiornate regolarmente, quindi si ha sempre la certezza che le app di Windows Server e Office 365 ProPlus siano sempre aggiornate. Ovviamente, lo svantaggio consiste nel fatto che sarà necessario applicare le personalizzazioni ogni volta che si ottiene una nuova immagine. È possibile creare script per automatizzare l'applicazione delle personalizzazioni.

### <a name="manually-update-your-existing-image"></a>Aggiornare manualmente l'immagine esistente
Questa opzione prevede l'uso degli strumenti standard di Windows per applicare aggiornamenti all'immagine. Per Office 365 ProPlus, usare lo Strumento di distribuzione di Office per scaricare e installare gli aggiornamenti o le versioni più recenti di Office 365 ProPlus.

> [!IMPORTANT]
> Occorre ricordare di disabilitare gli aggiornamenti automatici di Office 365 ProPlus.
> 
> 

Altre informazioni sull'uso dello Strumento di distribuzione di Office per gli aggiornamenti

* [Distribuire prodotti Office 365 a portata di clic tramite lo Strumento di distribuzione di Office](https://technet.microsoft.com/library/JJ219423.aspx)
* [Distribuzione e aggiornamento di Office 365 ProPlus mediante lo Strumento di distribuzione di Office](https://channel9.msdn.com/Events/Ignite/2015/BRK3168) (video)
* [Configurare le impostazioni di aggiornamento di Office 365 ProPlus](https://technet.microsoft.com/library/dn761708.aspx)

