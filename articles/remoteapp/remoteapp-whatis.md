---
title: "aaaWhat è Azure RemoteApp? | Microsoft Docs"
description: Informazioni su come tooshare App e risorse tooany dispositivo tramite Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>Informazioni su Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

RemoteApp di Azure offre funzionalità di hello del programma di RemoteApp Microsoft locale hello, supportato da Servizi Desktop remoto, tooAzure. Azure RemoteApp consente di fornire l'accesso remoto sicuro tooapplications da molti dispositivi utente diversi. Azure RemoteApp fondamentalmente ospita le sessioni di Terminal Server non permanenti nel cloud hello e ottenere toouse li e condividerli con gli utenti.

Con RemoteApp di Azure è possibile condividere app e risorse con utenti su quasi tutti i dispositivi. È di ospitare le app cloud hello, vale a dire che si occuperà di hardware hello e ridimensionamento toomeet utente richieste. Toodo è caricare le app hello tooshare desiderato e quindi ottenere il toouse utenti tali app. [Gli utenti ottengono tookeep i propri dispositivi](remoteapp-clients.md), durante la gestione di tutti gli elementi tramite hello portale di Azure. È anche possibile hello utilizzando le credenziali aziendali, consentendo di garantire sicurezza hello delle App e dati.

Continuare a leggere l'articolo per altre informazioni su Azure RemoteApp oppure, se si è già convinti, [provarlo subito](https://azure.microsoft.com/services/remoteapp/).

Domande su Azure RemoteApp? Vedere le [Domande frequenti](remoteapp-faq.md).

Azure RemoteApp fa parte di hello [Microsoft Virtual Desktop Infrastructure](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**Novità** Desidera toolearn informazioni su Azure RemoteApp? O pronta toovalidate RemoteApp di Azure su larga scala? Aggiungere il nostro settimanale [chiedere hello esperti webinar](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Raccolte di Azure RemoteApp
Sono disponibili due tipi di [raccolte di Azure RemoteApp](remoteapp-collections.md):

* Oggetto **cloud raccolta** è ospitato in e archivia i dati per programmi nel cloud hello. Gli utenti possono accedere alle app effettuando l'accesso con l'account Microsoft o con le credenziali aziendali sincronizzate o federate con Azure Active Directory.
  
    Scegliere una raccolta di cloud quando l'applicazione hello da tooshare non richiede una risorsa di connessione tooany rete privata dell'azienda (ad esempio, tramite un dispositivo VPN). Se un'applicazione hello utilizza risorse di hello Internet, OneDrive o in Azure, una raccolta di cloud è più adatto. È inoltre toocreate più rapido hello.
* Oggetto **raccolta ibrida** è ospitato in e archivia i dati in hello cloud di Azure, ma consente agli utenti accedere ai dati e le risorse memorizzate nella rete locale. Gli utenti possono accedere alle app effettuando l'accesso con le credenziali aziendali sincronizzate o federate con Azure Active Directory.
  
    Scegliere una raccolta ibrida se occorre tooresources una connessione di rete privata dell'azienda. Ad esempio, se hello applicazione deve accedere tooone seguenti hello:
  
  * Server di file sulla rete intranet
  * Quicken
  * Database protetti da firewall
    
    Si tratta in genere più utile per le grandi aziende con un numero elevato di risorse nella rete private in cui non possono essere spostato toohello cloud.

sono disponibili opzioni diverse, tra cui reti Hello raccolte diverse, pertanto scoprire [quale raccolta](remoteapp-collections.md) adatta alle tue esigenze. 

### <a name="updating-your-collection"></a>Aggiornamento della raccolta
Uno dei hello le principali differenze tra le raccolte di hello ibrido e cloud è la modalità di gestione degli aggiornamenti software. Un insieme di cloud che usa l'immagine di Office 365 ProPlus o Office 2013 preinstallata hello, non si dispone tooworry su tutti gli aggiornamenti. servizio Hello gestisce se stesso e rilascia gli aggiornamenti su base continuativa, alle App tooboth e sistema operativo hello.

Per le raccolte ibrido, nonché le raccolte di cloud che usano un'immagine modello personalizzato, si è responsabile della gestione di App e l'immagine di hello. Per le immagini appartenenti a un dominio, è possibile controllare gli aggiornamenti usando strumenti quali Windows Update, Criteri di gruppo o System Center.

Dopo l'aggiornamento dell'immagine modello personalizzato, caricare hello nuova immagine toohello cloud di Azure e quindi aggiornare hello raccolta toouse hello nuova immagine. (È possibile farlo da hello Azure RemoteApp **avvio rapido** pagina o Dashboard hello.)

Per altre informazioni vedere [Aggiornare la raccolta](remoteapp-update.md) .

## <a name="supported-remoteapp-clients"></a>Client supportati di RemoteApp
Azure RemoteApp è supportata in hello RemoteApp client App per Windows e Windows RT, nonché App Desktop remoto Microsoft hello per Mac, iOS e Android. Gli utenti possono usare queste app nel loro mobile o calcolo tooaccess dispositivi hello nuovi programmi RemoteApp di Azure.

Vedere [l'accesso delle App in Azure RemoteApp](remoteapp-clients.md) per ulteriori informazioni sui client hello.

## <a name="next-steps"></a>Passaggi successivi
Per provarlo, vedere gli articoli seguenti che descrivono come iniziare a usare Azure RemoteApp:

* [Tipo di raccolta necessario per RemoteApp di Azure](remoteapp-collections.md)
* [Creare un'immagine di Azure RemoteApp](remoteapp-imageoptions.md)
* [Come toocreate una raccolta di cloud di Azure RemoteApp](remoteapp-create-cloud-deployment.md)
* [Come toocreate una raccolta ibrida di Azure RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Funzionamento delle licenze in Azure RemoteApp](remoteapp-licensing.md)
* [Procedure consigliate per l'uso di Azure RemoteApp](remoteapp-bestpractices.md)
* [Domande frequenti su Azure RemoteApp](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Come contribuire al miglioramento
Non tutti sanno che in toorating aggiunta in questo articolo e aggiunta di commenti verso il basso, è possibile rendere articolo toohello di modifiche se stesso. Mancano informazioni? Alcune informazioni non sono corrette? Qualcosa non è abbastanza chiaro? Scorrere verso l'alto e fare clic su **modifica su GitHub** o **modifica** modifiche toomake - provengono quelli toous per la revisione e quindi, al termine è disconnettersi su di essi, si noterà delle modifiche e miglioramenti a destra.

