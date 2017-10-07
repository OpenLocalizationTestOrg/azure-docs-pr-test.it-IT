---
title: "aaaMonitor l'infrastruttura di identità locali in hello cloud."
description: "Si tratta hello Azure AD Connect Health pagina in cui viene descritto che cos'è e il motivo per cui si utilizzerebbe."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>Monitorare l'identità dell'infrastruttura e sincronizzazione servizi locali nel cloud hello
Azure Active Directory (Azure AD) Connect Health consente di monitorare e ottenere informazioni approfondite la tua identità locale hello e l'infrastruttura servizi di sincronizzazione. Permette toomaintain tooOffice una connessione affidabile 365 e Microsoft Online Services, fornendo funzionalità di monitoraggio per i componenti chiave di identità, ad esempio server di Active Directory Federation Services (ADFS), il server di Azure AD Connect (anche noto come il motore di sincronizzazione), i controller di dominio Active Directory e così via. Rende inoltre hello principali punti dati su questi componenti facilmente accessibile in modo che è possibile ottenere l'utilizzo e altri importanti decisioni informate toomake insights.

Hello informazioni vengono visualizzate in hello [portale di Azure AD Connect Health](https://aka.ms/aadconnecthealth). Nel portale di Azure AD Connect Health hello, è possibile visualizzare gli avvisi, monitoraggio delle prestazioni, analitica di utilizzo e altre informazioni. Azure AD Connect Health consente a un unico strumento hello di integrità per i componenti chiave di identità in un'unica posizione.

![Cos’è Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

Come aumentare la funzionalità di hello in Azure AD Connect Health, portale hello fornisce un singolo dashboard attraverso obiettivo hello dell'identità. Si dispone di un ambiente ancora più potente, integro e integrato per il tooincrease agli utenti il possibilità tooget cose.

## <a name="why-use-azure-ad-connect-health"></a>Perché usare Azure AD Connect Health
Quando si integrano le directory locali con Azure AD, gli utenti sono più produttivi perché è un'identità comune tooaccess sia cloud e risorse locali. Tuttavia, questa integrazione Crea richiesta di hello per garantire che l'ambiente sia integro, in modo che gli utenti possono accedere in modo affidabile le risorse locali e in hello cloud da qualsiasi dispositivo. Azure AD Connect Health consente di monitorare e ottenere informazioni approfondite l'infrastruttura di identità locale utilizzato tooaccess Office 365 o di altre applicazioni di Azure AD. È semplice come installare un agente in ogni server di identità locale in uso.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[Azure AD Connect Health per AD FS](active-directory-aadconnect-health-adfs.md)
Azure AD Connect Health per AD FS supporta AD FS 2.0 su Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2. Supporta inoltre il monitoraggio del proxy ADFS hello AD o server proxy di applicazione web che forniscono l'autenticazione di supporto per l'accesso extranet. Con un'installazione semplice e a basso costo di hello integrità agente, Azure AD Connect Health per AD FS fornisce hello seguente insieme di funzionalità principali:

* Monitoraggio con gli avvisi tooknow quando ADFS e server proxy ADFS non sono integri
* Notifiche tramite posta elettronica per gli avvisi critici
* Tendenze nei dati delle prestazioni, utili per la pianificazione delle capacità di AD FS.
* Analitica di utilizzo per accessi AD FS con pivot (App, gli utenti, il percorso di rete e così via), che sono toounderstand utili come guida usata AD FS
* Report per AD FS, relativi ad esempio ai primi 50 utenti che hanno tentativi di nome utente/password non riusciti e l'ultimo indirizzo IP.

Hello video seguente viene fornita una panoramica di Azure AD Connect Health per AD FS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md)
Azure AD Connect Health per la sincronizzazione consente di monitorare e vengono fornite informazioni delle sincronizzazioni hello che si verificano tra Active Directory locale e Azure AD. Azure AD Connect Health per la sincronizzazione fornisce hello seguente insieme di funzionalità principali:

* Monitoraggio con tooknow avvisi quando un server di Azure AD Connect, noto anche come hello motore di sincronizzazione, non è integro
* Notifiche tramite posta elettronica per gli avvisi critici
* Informazioni operative approfondite sulla sincronizzazione, che includono grafici della latenza per le operazioni di sincronizzazione e tendenze relative a varie operazioni, come aggiunta, aggiornamento o eliminazione
* Riepilogo rapido le informazioni sulle proprietà di sincronizzazione e l'ultimo corretta esportare tooAzure AD
* Report sugli errori di sincronizzazione a livello di oggetto \(non è necessario Azure AD Premium\).

Hello video seguente viene fornita una panoramica di Azure AD Connect Health per la sincronizzazione.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[Azure AD Connect Health per Active Directory Domain Services](active-directory-aadconnect-health-adds.md)
Azure AD Connect Health per Active Directory Domain Services consente il monitoraggio dei controller di dominio installati in Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016. installazione dell'agente di integrità Hello consente si toomonitor locale ambiente di dominio Active Directory dal cloud hello. Azure AD Connect Health di dominio Active Directory fornisce hello seguente insieme di funzionalità principali:

* Monitoraggio toodetect avvisi quando i controller di dominio non sono integri e le notifiche per gli avvisi critici di posta elettronica
* dashboard di controller di dominio Hello, che offre una visualizzazione rapida dello stato di hello e lo stato operativo dei controller di dominio
* dashboard di stato di replica Hello che dispone di informazioni di replica più recente di hello e collega le guide tootroubleshooting quando vengono rilevati errori
* Accesso rapido ovunque tooperformance grafici di dati dei contatori delle prestazioni comuni che sono necessari per la risoluzione dei problemi e monitoraggio

Hello video seguente viene fornita una panoramica di Azure AD Connect Health per AD DS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Introduzione ad Azure AD Connect Health
tooget avviato con Azure AD Connect Health, utilizzare hello alla procedura seguente:

1. [Ottenere Azure AD Premium](../active-directory-get-started-premium.md) o [avviare una versione di valutazione](https://azure.microsoft.com/trial/get-started-active-directory/).
2. [Scaricare e installare gli agenti di Azure AD Connect Health](#download-and-install-azure-ad-connect-health-agent) nei server di identità.
3. Dashboard di View hello Azure AD Connect Health alla [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth).

> [!NOTE]
> Tenere presente che prima di poter visualizzare i dati nel dashboard di Azure AD Connect Health, è necessario tooinstall hello gli agenti di Azure AD Connect Health nei server di destinazione.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>Scaricare e installare l'agente di Azure AD Connect Health
* Assicurarsi che si [soddisfare i requisiti di hello](active-directory-aadconnect-health-agent-install.md#requirements) per Azure AD Connect Health.
* Introduzione ad Azure AD Connect Health per AD FS
    * [Scaricare l'agente di Azure AD Connect Health per AD FS.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [Vedere le istruzioni di installazione di hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs).
* Introduzione ad Azure AD Connect Health per la sincronizzazione
    * [Scaricare e installare hello la versione più recente di Azure AD Connect](http://go.microsoft.com/fwlink/?linkid=615771). Hello integrità agente per la sincronizzazione verrà installato come parte dell'installazione di hello Azure AD Connect (versione 1.0.9125.0 o versione successiva).
* Introduzione ad Azure AD Connect Health per Active Directory Domain Services
    * <seg>
  [Scaricare l'agente di Azure AD Connect Health per Active Directory Domain Services](http://go.microsoft.com/fwlink/?LinkID=820540).</seg>
    * [Vedere le istruzioni di installazione di hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds).

## <a name="azure-ad-connect-health-portal"></a>Portale di Azure AD Connect Health
portale di Azure AD Connect Health Hello Mostra viste degli avvisi, monitoraggio delle prestazioni e analitica di utilizzo. Hello https://aka.ms/aadconnecthealth URL viene toohello pannello principale di Azure AD Connect Health. Un pannello è paragonabile a una finestra. Nel pannello principale hello, vedrai **avvio rapido**, i servizi in Azure AD Connect Health e opzioni di configurazione aggiuntive. Vedere hello seguente schermata e una breve spiegazione che seguono la schermata di hello. Dopo aver distribuito gli agenti di hello, il servizio di integrità hello identifica automaticamente i servizi hello che Azure AD Connect Health esegue il monitoraggio.

> [!NOTE]
> Per informazioni sulle licenze, vedere hello [domande sulla connessione AD Azure](active-directory-aadconnect-health-faq.md) o hello [pagina dei prezzi di Azure AD](https://aka.ms/aadpricing).
    
![portale di Azure AD Connect Health](./media/active-directory-aadconnect-health/portal4.png)

* **Guida introduttiva**: quando si seleziona questa opzione, hello **avvio rapido** apre blade. È possibile scaricare Azure AD Connect Health Agent hello selezionando **Scarica strumenti e**. È anche possibile accedere alla documentazione e fornire commenti e suggerimenti.
* **Active Directory Federation Services**: questa opzione Visualizza tutti i servizi ADFS hello che Azure AD Connect Health attualmente monitorati. Quando si seleziona un'istanza, pannello hello visualizzato Mostra informazioni su tale istanza del servizio. Queste informazioni includono una panoramica, le proprietà, gli avvisi, informazioni di monitoraggio e analisi di utilizzo. Altre informazioni sulle nuove funzionalità hello [tramite Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md).
* **Azure Active Directory Connect (Sincronizzazione)**: questa opzione visualizza i server di Azure AD Connect attualmente monitorati da Azure AD Connect Health. Quando si seleziona la voce hello, pannello hello visualizzato Mostra informazioni su server di Azure AD Connect. Altre informazioni sulle nuove funzionalità hello [tramite Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md).
* **Servizi di dominio Active Directory**: questa opzione Visualizza tutte le foreste di Active Directory hello che Azure AD Connect Health attualmente monitorati. Quando si seleziona un insieme di strutture, pannello hello visualizzato Mostra informazioni su tale foresta. Queste informazioni includono una panoramica di informazioni essenziali, hello i controller di dominio il dashboard, il dashboard di stato di replica hello, avvisi e monitoraggio. Altre informazioni sulle nuove funzionalità hello [tramite Azure AD Connect Health con AD DS](active-directory-aadconnect-health-adds.md).
* **Configurare**: in questa sezione include le opzioni tooturn hello segue disattivazione:

  - L'aggiornamento automatico tooautomatically aggiornamento hello Azure AD Connect Health agent toohello versione più recente: sarà aggiornato automaticamente toohello versioni più recenti di hello Azure AD Connect Health Agent quando diventano disponibili. Questa opzione è abilitata per impostazione predefinita.
  - Risoluzione dei problemi relativi a solo scopo di consentire i dati di integrità della directory di Microsoft access tooyour Azure AD: se questa opzione è abilitata, è possibile visualizzare Microsoft hello stessi dati visualizzati. Queste informazioni possono essere utili per la risoluzione dei problemi e per fornire l'assistenza necessaria. Questa opzione è disabilitata per impostazione predefinita.

## <a name="related-links"></a>Collegamenti correlati
* [Installazione dell'agente di Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operazioni di Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso di Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso di Azure AD Connect Health per la sincronizzazione](active-directory-aadconnect-health-sync.md)
* [Uso di Azure AD Connect Health con Servizi di dominio Active Directory](active-directory-aadconnect-health-adds.md)
* [Domande frequenti su Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Cronologia delle versioni di Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
