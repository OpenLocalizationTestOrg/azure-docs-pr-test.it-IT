---
title: aaaHow toocreate una raccolta ibrida per Azure RemoteApp | Documenti Microsoft
description: Informazioni su come toocreate una distribuzione di RemoteApp che si connette la rete interna tooyour.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>Come toocreate una raccolta ibrida per Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Sono disponibili due tipi di raccolte Azure RemoteApp:

* Cloud: risiede completamente in Azure. È possibile scegliere toosave tutti i dati nel cloud hello (in modo una raccolta di tipo solo cloud) o tooconnect la rete virtuale di tooa raccolta e salvare i dati non esiste.   
* Ibrida: include una rete virtuale per l'accesso locale, è necessario utilizzare hello di Azure AD e un ambiente Active Directory locale.

Non si sa cosa è necessario? Vedere [Tipo di raccolta necessario per RemoteApp di Azure](remoteapp-collections.md).

In questa esercitazione viene illustrato il processo di hello di creazione di una raccolta ibrida. Sono previsti otto passaggi:

1. Decidere quali [immagine](remoteapp-imageoptions.md) toouse per la raccolta. È possibile creare un'immagine personalizzata o utilizzare una delle immagini di Microsoft hello incluse con la sottoscrizione.
2. Configurare la rete virtuale. Estrarre hello [pianificazione della rete virtuale](remoteapp-planvnet.md) e [ridimensionamento](remoteapp-vnetsizing.md) informazioni.
3. Creare una raccolta.
4. Aggiungere il dominio locale tooyour di raccolta.
5. Aggiungere una raccolta di tooyour immagine modello.
6. Configurare la sincronizzazione della directory. RemoteApp di Azure richiede che si integra con Azure Active Directory da entrambi 1) configurare Azure Active Directory Sync con opzione di sincronizzazione Password hello o 2) Configurazione sincronizzazione Azure Active Directory senza l'opzione di sincronizzazione Password hello ma usa un dominio che è tooAD federati ADFS. Estrarre hello [le informazioni di configurazione di Active Directory con RemoteApp](remoteapp-ad.md).
7. Pubblicare app di RemoteApp.
8. Configurare l'accesso utente.

**Prima di iniziare**

È necessario seguente hello toodo prima di creare una raccolta di hello:

* [Accedere](https://azure.microsoft.com/services/remoteapp/) ad Azure RemoteApp.
* Creare un account utente in Active Directory toouse come account del servizio Azure RemoteApp hello. Limitare le autorizzazioni di hello per questo account in modo che questo può associarsi solo dominio toohello macchine.
* Raccogliere informazioni sulla rete locale: informazioni sull'indirizzo IP e dettagli sul dispositivo VPN.
* Installare hello [Azure PowerShell](/powershell/azure/overview) modulo.
* Raccogliere informazioni sugli utenti hello che si desidera accedere toogrant a. Si sarà necessario hello nome dell'entità utente di Azure Active Directory (ad esempio, name@contoso.com) per ogni utente. Verificare che tale hello UPN corrispondente tra Azure AD e Active Directory.
* Scegliere un'immagine modello. Un'immagine modello RemoteApp di Azure contiene hello App e i programmi che si desidera toopublish per gli utenti. Per altre informazioni, vedere [Opzioni immagine di RemoteApp di Azure](remoteapp-imageoptions.md) .
* Desidera toouse immagine di Office 365 ProPlus hello? consultare le informazioni in [questo articolo](remoteapp-officesubscription.md).
* [Configurare Active Directory per RemoteApp](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>Passaggio 1: configurare la rete virtuale
È possibile distribuire una raccolta ibrida che utilizza una rete virtuale di Azure esistente oppure è possibile creare una nuova rete virtuale. Una rete virtuale consente agli utenti di accedere ai dati nella rete locale mediante le risorse remote di RemoteApp. Usa una rete virtuale di Azure offre il tooother di accesso di rete diretta raccolta servizi di Azure e le macchine virtuali distribuite toothat di rete virtuale.

Verificare hello [pianificazione della rete virtuale](remoteapp-planvnet.md) e [dimensioni tra reti VIRTUALI](remoteapp-vnetsizing.md) informazioni prima di creare una rete virtuale.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Creare una rete virtuale di Azure e creare un join tooyour distribuzione di Active Directory
Per iniziare, creare una [rete virtuale](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), Questa operazione viene eseguita su hello **rete** scheda hello portale di Azure. È necessario tooconnect il toohello di rete virtuale distribuzione di Active Directory che viene sincronizzata tooyour tenant di Azure Active Directory.

Vedere [creare una rete virtuale usando il portale di Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) per ulteriori informazioni.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Assicurarsi che la rete virtuale sia pronta per RemoteApp di Azure
Prima di creare la raccolta, verificare che la nuova rete virtuale sia pronta. È possibile convalidarlo eseguendo hello seguenti:

1. Creare una macchina virtuale di Azure all'interno di hello subnet della rete virtuale di hello che appena creata per RemoteApp.
2. Utilizzare una macchina virtuale toohello tooconnect di Desktop remoto. (facendo clic su **Connetti**).
3. Creare un join toohello stessa distribuzione di Active Directory che si desidera toouse per RemoteApp.

Ha funzionato? La rete e la subnet virtuali sono pronte per RemoteApp di Azure!

È possibile trovare ulteriori informazioni sulla creazione di macchine virtuali di Azure e connessione Desktop remoto toothem [qui](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Passaggio 2: Creare una raccolta di RemoteApp di Azure.
1. In hello [portale di Azure](http://manage.windowsazure.com), visitare toohello Azure RemoteApp pagina.
2. Fare clic su **Nuovo > Crea con rete virtuale**.
3. Immettere un nome per la raccolta.
4. Scegliere il piano di hello che si desidera toouse - standard o basic.
5. Scegliere la rete virtuale dall'elenco e quindi la subnet hello discesa.
6. Scegliere toojoin è tooyour dominio.
7. Fare clic su **Crea raccolta RemoteApp**.

Dopo aver creata la raccolta di Azure RemoteApp, fare doppio clic sul nome hello dell'insieme di hello. Verrà visualizzata hello **avvio rapido** pagina - si tratta in cui sarà terminata la configurazione raccolta hello.

Nel caso in cui si siano verificati problemi Estrarre hello [raccolta ibrida informazioni sulla risoluzione dei](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-toohello-local-domain"></a>Passaggio 3: Collegare il dominio locale toohello di raccolta
1. In hello **avvio rapido** pagina, fare clic su **aggiunta a un dominio locale**.
2. Aggiungere hello Azure RemoteApp dominio account del servizio tooyour locale Active Directory. È necessario il nome di dominio di hello, unità organizzativa, nome utente dell'account di servizio e la password.
   
    Si tratta di informazioni hello raccolte se sono stati seguiti i passaggi di hello in [Configura Active Directory per Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>Passaggio 4: Immagine collegamento tooan Azure RemoteApp
Un'immagine modello RemoteApp di Azure contiene i programmi di hello che si desidera tooshare con gli utenti. È possibile creare un nuovo [immagine modello](remoteapp-imageoptions.md) o collegamento tooan esistente image (uno già importati o caricati tooAzure RemoteApp). È anche possibile collegare tooone di hello Azure RemoteApp [immagini modello](remoteapp-images.md) che contengono i programmi di Office 2013 (per l'utilizzo di valutazione) o di Office 365.

Se si sta caricando una nuova immagine hello, è necessario tooenter hello nome e scegliere il percorso di hello per immagine hello. Nella pagina successiva di hello della procedura guidata hello, si verrà vedere un set di cmdlet di PowerShell - copia ed eseguire questi cmdlet da un'elevata immagine specificata di Windows PowerShell tooupload prompt dei comandi hello.

Se ci si collega l'immagine modello esistente tooan, è sufficiente specificare il nome di immagine hello, la posizione e la sottoscrizione Azure associata.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Passaggio 5: Configurare la sincronizzazione della directory di Active Directory
RemoteApp di Azure richiede che si integra con Azure Active Directory da entrambi 1) configurare Azure Active Directory Sync con opzione di sincronizzazione Password hello o 2) Configurazione sincronizzazione Azure Active Directory senza l'opzione di sincronizzazione Password hello ma usa un dominio che è tooAD federati ADFS.

Consultare [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) - questo articolo consente di impostare l'integrazione di directory in 4 passaggi.

Per informazioni sulla pianificazione e le procedure dettagliate, vedere [Roadmap sulla sincronizzazione della directory](http://msdn.microsoft.com//library/azure/hh967642.aspx) .

## <a name="step-6-publish-apps"></a>Passaggio 6: Pubblicare le app
Un'app di Azure RemoteApp è l'applicazione hello o un programma che è fornire agli utenti di tooyour. Si trova nell'immagine modello hello caricato per la raccolta di hello. Quando un utente accede a un'app, viene visualizzato toorun nell'ambiente locale, ma è effettivamente in esecuzione in Azure.

Prima che gli utenti possono accedere le applicazioni, è necessario toopublish loro – in questo modo gli utenti accesso hello App tramite il client Desktop remoto di hello.

È possibile pubblicare più raccolta tooyour di App. Pagina pubblicazione hello fare clic su **pubblica** tooadd un'app. È possibile pubblicare da hello **avviare** menu dell'immagine modello hello o specificando il percorso di hello all'immagine modello hello per app hello. Se si sceglie tooadd da hello **avviare** menu, scegliere tooadd programma hello. Se si sceglie tooprovide hello percorso toohello app, specificare un nome per l'applicazione hello e hello percorso toowhere che immagine modello hello è installato.

## <a name="step-7-configure-user-access"></a>Passaggio 7: Configurare l'accesso utente
Dopo aver creato la raccolta, è necessario agli utenti di hello tooadd che si desidera toouse in grado di toobe risorse remote. gli utenti di Hello è fornire accesso tooneed tooexist nel tenant di Active Directory hello associati hello sottoscrizione è utilizzato toocreate questa raccolta RemoteApp di Azure.

1. Dalla pagina avvio rapido hello, fare clic su **configurare l'accesso utente**.
2. Immettere l'account Microsoft o account aziendale hello (da Active Directory) che si desidera accedere toogrant per.
   
   **Note:**
   
   Assicurarsi di utilizzare hello  *user@domain.com*  formato.
   
   Se si utilizza Office 365 ProPlus nella raccolta, è necessario utilizzare le identità di Active Directory hello per gli utenti. Ciò consente di convalidare la licenza.
3. Quando gli utenti di hello vengono convalidati, fare clic su **salvare**.

## <a name="next-steps"></a>Passaggi successivi
La procedura è stata completata e la raccolta ibrida RemoteApp di Azure è stata creata e distribuita. passaggio successivo Hello è toohave gli utenti, scaricare e installare il client di Desktop remoto di hello. È possibile trovare l'URL di hello del client hello nella pagina avvio rapido di Azure RemoteApp hello. Quindi, avere agli utenti l'accesso nel client hello e accedere alle App hello che è stato pubblicato.

### <a name="help-us-help-you"></a>Come contribuire al miglioramento
Non tutti sanno che in toorating aggiunta in questo articolo e aggiunta di commenti verso il basso, è possibile rendere articolo toohello di modifiche se stesso. Mancano informazioni? Alcune informazioni non sono corrette? Qualcosa non è abbastanza chiaro? Scorrere verso l'alto e fare clic su **modifica su GitHub** modifiche toomake - provengono quelli toous per la revisione e quindi, al termine è disconnettersi su di essi, si noterà delle modifiche e miglioramenti a destra.

