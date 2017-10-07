---
title: aaaHow toocreate una raccolta di cloud di Azure RemoteApp | Documenti Microsoft
description: Informazioni su come toocreate una distribuzione di Azure RemoteApp che salva i dati in hello cloud di Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>Come toocreate una raccolta di cloud di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Sono disponibili due tipi di [raccolte di Azure RemoteApp](remoteapp-collections.md): 

* Cloud: risiede completamente in Azure. È possibile scegliere toosave tutti i dati nel cloud hello (in modo una raccolta di tipo solo cloud) o tooconnect la rete virtuale di tooa raccolta e salvare i dati non esiste.   
* Ibrida: include una rete virtuale per l'accesso locale, è necessario utilizzare hello di Azure AD e un ambiente Active Directory locale.

In questa esercitazione viene illustrato il processo di hello di creazione di una raccolta nel cloud. i quattro passaggi della creazione di una distribuzione cloud. 

1. Creare una raccolta di Azure RemoteApp.
2. Facoltativamente, configurare la sincronizzazione della directory. Se si utilizza AD Azure + Active Directory, si dispone toosynchronize utenti, contatti e le password dal tenant tooyour AD Azure Active Directory locale.
3. Pubblicare le app.
4. Configurare l'accesso utente.

**Prima di iniziare**

È necessario seguente hello toodo prima di creare una raccolta di hello:

* [Accedere](https://azure.microsoft.com/services/remoteapp/) ad Azure RemoteApp. 
* Raccogliere informazioni sugli utenti hello che si desidera accedere toogrant a. Le informazioni possono essere relative all'account Microsoft o all'account di lavoro Active Directory per gli utenti.
* Si presuppone che sono entrambi toouse passare una delle immagini modello hello fornito come parte della sottoscrizione o che sia già caricato hello modello immagine toouse. Se è necessario tooupload un'immagine di modello diverso, è possibile farlo dalla pagina di hello immagini modello. Fare clic su **caricare un'immagine modello** e seguire i passaggi hello nella procedura guidata hello. 
* Desidera toouse immagine di Office 365 ProPlus hello? consultare le informazioni in [questo articolo](remoteapp-officesubscription.md).
* Desidera App personalizzate tooprovide o applicazioni LOB. Creare una nuova [immagine](remoteapp-imageoptions.md) e usarla nella raccolta nel cloud.
* Determinare se è necessario tooconnect tooa rete virtuale. Se si sceglie tooconnect tooa rete virtuale, assicurarsi che vengano soddisfatti hello [ridimensionamento delle linee guida](remoteapp-vnetsizing.md) e [possono connettersi tooRemoteApp](remoteapp-vnet.md). Estrarre hello [articolo pianificazione di rete virtuale ](remoteapp-planvnet.md)per ulteriori informazioni.
* Se si utilizza una rete virtuale, decidere se toojoin è tooyour dominio di Active Directory locale.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>Passaggio 1: Creare una raccolta cloud con o senza una rete virtuale
Utilizzare hello seguenti passaggi viene troppo**creare una raccolta di tipo solo cloud**:

1. Nel portale di gestione hello passare toohello RemoteApp pagina.
2. Fare clic su **Nuovo > Creazione rapida**.
3. Immettere un nome per la raccolta e selezionare l'area.
4. Scegliere il piano di hello che si desidera toouse - standard o basic.
5. Scegliere hello modello toouse per questa raccolta. 
   
    **Suggerimento:** prevede la sottoscrizione a RemoteApp [immagini modello](remoteapp-images.md) contenenti Office 365 o programmi Office 2013 (per l'utilizzo di valutazione), alcune pubblicato (ad esempio Word) e altri pronto toopublish. È anche possibile creare una nuova [immagine](remoteapp-imageoptions.md) e usarla nella raccolta nel cloud.
6. Fare clic su **Crea raccolta RemoteApp**.
   
    **Importante:** può richiedere fino a too30 minuti tooprovision la raccolta.

Dopo aver creata la raccolta di Azure RemoteApp, fare doppio clic sul nome hello dell'insieme di hello. Verrà visualizzata hello **avvio rapido** pagina - si tratta in cui sarà terminata la configurazione raccolta hello.

Utilizzare hello seguenti passaggi viene toocreate un **cloud + raccolta rete virtuale**:

1. Nel portale di gestione hello passare toohello Azure RemoteApp pagina.
2. Fare clic su **Nuovo** > **Crea con rete virtuale**.
3. Immettere un nome per la raccolta.
4. Scegliere il piano di hello che si desidera toouse - standard o basic.
5. Scegliere hello rete virtuale già stato creato. Sapere come toodo che? Per il momento, hello passaggi sono descritti nella hello [ibrida](remoteapp-create-hybrid-deployment.md) argomento.
6. Se si decide toojoin dominio tooyour insieme. In caso affermativo, è necessario toointegrate Connetti toouse AD Azure AD e l'ambiente Active Directory. Questa procedura è descritta nel **passaggio 2**riportato di seguito.
7. Fare clic su **Crea raccolta RemoteApp**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>Passaggio 2: Configurare la sincronizzazione della directory di Active Directory (facoltativo)
Se si desidera toouse Active Directory, Azure RemoteApp richiede la sincronizzazione delle directory tra Azure Active Directory e gli utenti toosynchronize di Active Directory locale, contatti e tenant di Azure Active Directory tooyour le password. Per informazioni sulla pianificazione, vedere [Configurare Active Directory per Azure RemoteApp](remoteapp-ad.md) . È inoltre possibile passare direttamente troppo[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) per informazioni.

## <a name="step-3-publish-apps"></a>Passaggio 3: Pubblicare le app
Un'app di Azure RemoteApp è l'applicazione hello o un programma che è fornire agli utenti di tooyour. Si trova nell'immagine modello hello caricato per la raccolta di hello. Quando un utente accede a un'app, l'applicazione hello sembra toorun nell'ambiente locale, ma è effettivamente in esecuzione in una macchina virtuale in Azure. 

Prima che gli utenti possono accedere le applicazioni, è necessario toopublish li: la pubblicazione consente le app agli utenti di accedere alle App hello tramite hello client Desktop remoto.

È possibile pubblicare più applicazioni tooyour raccolta di Azure RemoteApp. Pagina pubblicazione hello fare clic su **pubblica** tooadd un programma. È possibile pubblicare da hello **avviare** menu dell'immagine modello hello o specificando il percorso di hello all'immagine modello hello per app hello. Se si sceglie tooadd da hello **avviare** menu, scegliere toopublish app hello. Se si sceglie tooprovide hello percorso toohello app, specificare un nome per l'applicazione hello e hello percorso toowhere che immagine modello hello è installato.

## <a name="step-4-configure-user-access"></a>Passaggio 4: Configurare l'accesso utente
Dopo aver creato la raccolta, è necessario agli utenti di hello tooadd che si desidera toouse in grado di toobe risorse remote. Se si utilizza Active Directory, gli utenti di hello è fornire accesso tooneed tooexist nel tenant di Active Directory hello associati hello sottoscrizione è usato toocreate questa raccolta.

1. Dalla pagina avvio rapido hello, fare clic su **configurare l'accesso utente**. 
2. Immettere l'account Microsoft o account aziendale hello (da Active Directory) che si desidera accedere toogrant per.
   
   **Note:** 
   
   Assicurarsi di utilizzare hello  *user@domain.com*  formato.
   
   Se si utilizza Office 365 ProPlus nella raccolta, è necessario utilizzare le identità di Active Directory hello per gli utenti. Ciò consente di convalidare la licenza. 
3. Una volta convalidati gli utenti di hello, fare clic su **salvare**.

## <a name="next-steps"></a>Passaggi successivi
La procedura è stata completata e la raccolta di Azure RemoteApp nel cloud è stata creata e distribuita. passaggio successivo Hello è toohave gli utenti, scaricare e installare il client di Desktop remoto di hello. È possibile trovare l'URL di hello del client hello nella pagina avvio rapido di Azure RemoteApp hello. Quindi, avere agli utenti l'accesso nel client hello e accedere alle App hello che è stato pubblicato.

### <a name="help-us-help-you"></a>Come contribuire al miglioramento
Non tutti sanno che in toorating aggiunta in questo articolo e aggiunta di commenti verso il basso, è possibile rendere articolo toohello di modifiche se stesso. Mancano informazioni? Alcune informazioni non sono corrette? Qualcosa non è abbastanza chiaro? Scorrere verso l'alto e fare clic su **modifica su GitHub** modifiche toomake - provengono quelli toous per la revisione e quindi, al termine è disconnettersi su di essi, si noterà delle modifiche e miglioramenti a destra.

