---
title: domande frequenti su RemoteApp aaaAzure | Documenti Microsoft
description: "Altre risposte toohello più domande frequenti su Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Domande frequenti su Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Abbiamo saputo hello seguenti domande su Azure RemoteApp. Ve ne sono altre? Visitare hello [forum RemoteApp](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) e far conoscere cosa è necessario tooknow o di un commento verso il basso sotto.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>Le informazioni cercate non sono disponibili? Non è possibile trovare la risposta a una domanda?
Se non è possibile trovare informazioni hello è necessario o si dispone di una domanda aggiuntiva che si sta non copre qui, visitare toohello [forum di Azure RemoteApp](http://aka.ms/araforum) e porre la domanda non esiste. dove verranno aggiunte altre risposte.

## <a name="what-is-azure-remoteapp"></a>Informazioni su Azure RemoteApp
* **Informazioni su Azure RemoteApp** RemoteApp è che un servizio di Azure consente di fornire l'accesso remoto sicuro tooapplications da molti dispositivi utente diversi. Altre informazioni su [Azure RemoteApp](remoteapp-whatis.md).
* **Quali sono le opzioni di distribuzione hello?** Sono disponibili due tipi di distribuzioni di RemoteApp: ibrida e nel cloud. Quale è necessario dipende da numerosi fattori, ad esempio la necessità di aggiunta a un dominio. Tutte queste decisioni sono discusse [qui](remoteapp-collections.md).

## <a name="quick-tips-on-using-azure-remoteapp"></a>Suggerimenti rapidi sull'uso di Azure RemoteApp
* **Dopo quanto tempo si viene disconnessi? Quanto tempo è possibile essere inattivo prima di eseguire l'avvio di hello?** 4 ore. Se un utente rimane inattivo per 4 ore, viene disconnesso automaticamente da Azure RemoteApp. Check-out hello altre impostazioni predefinite in [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md).
* **È possibile provare il servizio gratuitamente?** Sì. È disponibile una versione di valutazione gratuita della durata di 30 giorni. Al termine del processo di valutazione di hello, è possibile passare a pagamento di account (che è possibile utilizzare nell'ambiente di produzione) o smettere di usare il servizio hello tooa. Avviare la versione di valutazione gratuito visitando troppo[portal.azure.com](http://portal.azure.com) -creare una nuova istanza di RemoteApp. Versione di valutazione gratuita hello, è possibile compilare 2 istanze di RemoteApp con 10 utenti per ogni istanza. Si noti che la versione di valutazione è valida soltanto per 30 giorni.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Dettagli della sottoscrizione Azure RemoteApp
* **Quali sono i limiti dei servizi hello?** Per informazioni sulle impostazioni predefinite di hello e limiti di Azure RemoteApp nel servizio [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md). Per altre domande contattare Microsoft.
* **Il numero di utenti eseguire ho toohave?** È necessario un numero minimo di 20 utenti. È possibile ripetere che toobe deselezionare super - hello minimo è pari a 20. Verrà emessa una fattura per 20. 
* **Quanto costa RemoteApp?** Consultare i [dettagli dei prezzi di Azure RemoteApp ](https://azure.microsoft.com/pricing/details/remoteapp/).
* **Un tipo di raccolta costa più di un altro?** Sì, è possibile, a seconda delle esigenze di raccolta. Una raccolta ibrida richiede una connessione di rete di Azure RemoteApp tooyour locale. Se si utilizza una Route di rete virtuale/Express esistente, non esiste alcun costo aggiuntivo. Ma se si utilizza una nuova rete virtuale di Azure e un gateway o Expressroute, verrà addebitata per hello [gateway VPN](https://azure.microsoft.com/pricing/details/vpn-gateway) o [Express Route](https://azure.microsoft.com/pricing/details/expressroute/). Questo costo (descritti in dettaglio in collegamenti hello) è all'inizio del mese di Azure RemoteApp dei costi.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>Raccolte - cos'è supportato, cosa è opportuno utilizzare e altro
* **Le applicazioni personalizzate LOB (line-of-business) sono supportate?** Sì. creare un'applicazione personalizzata in Azure RemoteApp, toouse un [immagine modello personalizzato](remoteapp-create-custom-image.md)e quindi caricarla raccolta RemoteApp toohello.
* **L'applicazione LOB personalizzato funzioneranno in Azure RemoteApp?**  hello toofigure modo migliore di out tootest è. Estrarre hello [Centro compatibilità](http://www.rdcompatibility.com/compatibility/default.aspx).
* **Quale metodo di distribuzione (cloud o ibrido) è più adatto per la propria organizzazione?** Le raccolte di ibrida forniscono un'esperienza più completa di hello se si desidera l'integrazione completa con single sign-on (SSO) e la connettività di rete protetto in locale. Le raccolte di cloud forniscono tooisolate un modo semplice e agile la distribuzione con più metodi di autenticazione. Altre informazioni su hello [opzioni di distribuzione](remoteapp-whatis.md).
* **Al momento si usa SQL o un altro database, in locale o in Azure. Che tipo di distribuzione è consigliabile usare?** Questo dipende dal luogo in cui risiede il database SQL o back-end. Se il database di hello in una rete privata, è possibile utilizzare raccolta ibrida hello. Se il database di hello viene esposto toohello Internet e consente ai client di connessioni tooconnect tooit, è possibile utilizzare raccolta hello nel cloud.
* **E per quanto riguarda il mapping delle unità, le porte USB e seriali, la condivisione degli Appunti e il reindirizzamento della stampante?** Tutte queste funzionalità sono supportate in Azure RemoteApp. Il reindirizzamento della stampante e la condivisione degli Appunti sono abilitati per impostazione predefinita. Altre informazioni sul reindirizzamento sono disponibili [qui](remoteapp-redirection.md). 

## <a name="template-images"></a>Immagini modello
* **È possibile utilizzare un cloud o macchina virtuale esistente come modello hello per la raccolta RemoteApp?** È possibile usarlo. È possibile creare un'immagine basata su una macchina virtuale di Azure, utilizzare una delle immagini hello incluse con la sottoscrizione o creare un'immagine personalizzata. Estrarre hello [Opzioni immagine RemoteApp](remoteapp-imageoptions.md).

## <a name="network-options"></a>Opzioni di rete
* **raccolta ibrida Hello richiede una rete virtuale. È possibile usare la rete virtuale esistente?** È possibile se rete virtuale esistente hello è una rete virtuale di Azure. Vedere "passaggio 1: configurare la rete virtuale" in hello [istruzioni raccolta ibrida](remoteapp-create-hybrid-deployment.md) per ulteriori informazioni.
* **È possibile utilizzare una rete virtuale con una raccolta di cloud?** È possibile. Per altre informazioni, vedere [Creare una raccolta cloud](remoteapp-create-cloud-deployment.md), in particolare il passaggio 1.

## <a name="authentication-options"></a>Opzioni di autenticazione
* **Per quanto riguarda l'autenticazione, I metodi sono supportati?**  raccolta cloud hello supporta gli account Microsoft e account di Azure Active Directory, che sono anche gli account di Office 365. raccolta ibrida Hello supporta solo gli account di Azure Active Directory che sono stati sincronizzati (usando uno strumento come [Azure Active Directory Sync](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) da una distribuzione di Windows Server Active Directory; in particolare, una sincronizzazione con hello Opzione di sincronizzazione password o sincronizzato con federazione di Active Directory Federation Services (ADFS) configurata. È anche possibile configurare la [Multi-Factor Authentication (MFA)](https://azure.microsoft.com/services/multi-factor-authentication/).

> [!NOTE]
> gli utenti di Azure Active Directory Hello devono essere di tenant hello è associato alla sottoscrizione. (È possibile visualizzare e modificare la sottoscrizione hello **impostazioni** scheda nel portale di hello. Vedere [tenant di Azure Active Directory hello modifica usata da RemoteApp](remoteapp-changetenant.md) per ulteriori informazioni.)
> 
> 

* **Motivo per cui è possibile fornire l'account di accesso di Azure Active Directory?**  gli utenti di Azure Active Directory hello devono essere dalla directory di hello in cui è associato alla sottoscrizione. È possibile visualizzare o modificare la directory nella scheda Impostazioni hello nel portale di hello. Vedere [tenant di Azure Active Directory hello modifica usata da RemoteApp](remoteapp-changetenant.md) per ulteriori informazioni.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>Client - il dispositivo può usare tooaccess Azure RemoteApp?
È possibile trovare informazioni client valido, inclusi i passaggi per l'installazione dei client diversi hello in [l'accesso delle App in Azure RemoteApp](remoteapp-clients.md).

* **Quali dispositivi e i sistemi operativi supportano da applicazioni client hello?**
  Primo, il computer di hello e Tablet: 
  
  * Windows 10 (anteprima client)
  * Windows 8.1 e Windows 8
  * Windows 7 Service Pack 1
  * Mac OS X
  * Windows RT
  * Tablet Android
  * iPad

    E i telefoni hello:
  * iPhone
  * Telefono Android
  * Windows Phone
    
    [Scaricare](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) ora un client di RemoteApp.
* **Azure RemoteApp supporta i thin client?** Sì, hello seguenti con Windows Embedded thin client sono supportate:
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **La versione di Windows Server è supportata per la sessione Desktop remoto Host () hello?** Windows Server 2012 R2.

## <a name="support-and-feedback"></a>Supporto, commenti e suggerimenti
* **Che cos'è il piano di supporto hello per RemoteApp?** Il supporto per la fatturazione e la gestione delle sottoscrizioni viene fornito gratuitamente. Il supporto tecnico è disponibile tramite hello [i piani di servizio Azure](https://azure.microsoft.com/support/plans/). È anche possibile ottenere supporto gratuito dalla community tramite il [forum di discussione di Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp). 
* **Come è possibile inviare commenti?** Visitare hello [forum sul feedback su](https://feedback.azure.com/forums/247748-azure-remoteapp/).
* **Che è possibile comunicare toolearn informazioni su Azure RemoteApp?** In aggiunta tooour [forum di discussione](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp), vale a dire domande di toopost un ottimo punto, è possibile unire hello settimanale [chiedere hello esperti webinar](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html), in cui si parlerà tutto RemoteApp.
* **Qual è la documentazione disponibile per RemoteApp?** È un'ottima domanda. È inoltre contenuto nel cassetto della Guida del portale hello della Guida per toohello (fare clic su hello **?** in una pagina di portale hello), hello gli articoli seguenti è disponibili tooteach tutte su RemoteApp:
  
  * **Per iniziare:**
    * [Che cos'è RemoteApp?](remoteapp-whatis.md)
    * [Che cos'è immagini modello RemoteApp di hello?](remoteapp-images.md)
    * [Come funzionano le licenze?](remoteapp-licensing.md)
    * [Come funzionano RemoteApp e Office insieme?](remoteapp-o365.md)
    * [Come funziona il reindirizzamento in RemoteApp](remoteapp-redirection.md)?
  * **Distribuzione:**
    * [Creare un'immagine modello personalizzata](remoteapp-create-custom-image.md)
    * [Creare una raccolta ibrida](remoteapp-create-hybrid-deployment.md)
    * [Creare una raccolta nel cloud](remoteapp-create-cloud-deployment.md)
    * [Configurare Azure Active Directory per RemoteApp](remoteapp-ad.md)
    * [Pubblicare un'app in RemoteApp](remoteapp-publish.md)
  * **Gestione:**
    
    * [Aggiungere utenti](remoteapp-user.md)
    * [Procedure consigliate per la configurazione e l'uso di RemoteApp](remoteapp-bestpractices.md)    
    
    Video Sono anche disponibili diversi video su RemoteApp. Alcuni forniscono informazioni di base ([tooAzure introduzione RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) mentre altri consentono di eseguire la distribuzione ([distribuzione Cloud](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) e [distribuzione ibrida](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). Si raccomanda di accedere a queste utili risorse.

### <a name="help-us-help-you"></a>Come contribuire al miglioramento
Non tutti sanno che in toorating aggiunta in questo articolo e aggiunta di commenti verso il basso, è possibile rendere articolo toohello di modifiche se stesso. Mancano informazioni? Alcune informazioni non sono corrette? Qualcosa non è abbastanza chiaro? Scorrere verso l'alto e fare clic su **modifica su GitHub** modifiche toomake - provengono quelli toous per la revisione e quindi, al termine è disconnettersi su di essi, si noterà delle modifiche e miglioramenti a destra.

