---
title: 'Azure Active Directory Domain Services: distribuire il proxy di applicazione di Azure Active Directory | Documentazione Microsoft'
description: Usare il proxy di applicazione di Azure AD nei domini gestiti di Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Distribuire il proxy di applicazione di Azure AD in un dominio gestito di Azure AD Domain Services
Proxy dell'applicazione Azure Active Directory (AD) consente di supportare gli utenti remoti mediante la pubblicazione toobe applicazioni locale accessibili tramite hello internet. Con i servizi di dominio Active Directory di Azure, è possibile ora accuratezza di spostamento e le applicazioni legacy che esegue servizi di infrastruttura tooAzure locale. È quindi possibile pubblicare queste applicazioni utilizzano hello Proxy dell'applicazione AD Azure, tooprovide toousers di accesso remoto sicuro all'interno dell'organizzazione.

Se si toohello nuovo Proxy dell'applicazione Azure AD, ulteriori informazioni su questa funzionalità con hello articolo seguente: [come tooprovide proteggere l'accesso remoto applicazioni locali tooon](../active-directory/active-directory-application-proxy-get-started.md).


## <a name="before-you-begin"></a>Prima di iniziare
attività di hello tooperform elencate in questo articolo, è necessario:

1. Una **sottoscrizione di Azure**valida.
2. Una **directory di Azure AD** sincronizzata con una directory locale o con una directory solo cloud.
3. Un **licenza Azure AD Basic o Premium** è obbligatorio toouse hello Proxy dell'applicazione AD Azure.
4. **Servizi di dominio AD Azure** deve essere abilitato per la directory hello Azure AD. Se non è ancora fatto, seguire tutte le attività descritte nella hello hello [Guida introduttiva](active-directory-ds-getting-started.md).

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>Attività 1: Abilitare il proxy di applicazione di Azure AD per la directory di Azure AD
Eseguire hello seguendo i passaggi tooenable hello Proxy dell'applicazione AD Azure per la directory di Azure AD.

1. Accedere come amministratore in hello [portale di Azure](http://portal.azure.com).

2. Fare clic su **Azure Active Directory** toobring i cenni preliminari sulla directory hello. Fare clic su **Applicazioni aziendali**.

    ![Selezionare la directory di Azure AD](./media/app-proxy/app-proxy-enable-start.png)
3. Fare clic su **Proxy di applicazione**. Se non si dispone di una sottoscrizione di Azure AD Basic o Azure AD Premium, viene visualizzato un tooenable opzione una versione di valutazione. Attiva/disattiva **abilitare il Proxy di applicazione?** troppo**abilitare** e fare clic su **salvare**.

    ![Abilitare il proxy di applicazione](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload hello connettore, fare clic su hello **connettore** pulsante.

    ![Scaricare il connettore](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. Nella pagina di download di hello, accettare l'informativa sulla privacy e condizioni di licenza di hello e fare clic su hello **scaricare** pulsante.

    ![Confermare il download](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>Attività 2: provisioning appartenenti a un dominio Windows Server toodeploy hello Azure AD applicazione connettore del Proxy
È necessario appartenenti a un dominio di macchine virtuali Windows Server in cui è possibile installare connettore Proxy dell'applicazione AD Azure hello. A seconda delle applicazioni di hello in corso di pubblicazione, è possibile scegliere più server in cui è installato il connettore hello tooprovision. Questa opzione di distribuzione offre maggiore disponibilità e permette di gestire carichi di lavoro di autenticazione più gravosi.

Eseguire il provisioning di server del connettore hello in hello stessa rete virtuale (o una rete virtuale connessa peering), in cui è stato abilitato il dominio gestito di servizi di dominio Active Directory di Azure. Analogamente, hello che ospitano applicazioni hello è pubblicare tramite Proxy applicazione hello necessario toobe installato hello stessa rete virtuale di Azure.

server del connettore tooprovision, eseguire attività di hello descritta nell'articolo hello intitolata [aggiunta a un dominio gestito di macchina virtuale tooa Windows](active-directory-ds-admin-guide-join-windows-vm.md).


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>Attività 3: installare e registrare hello connettore del Proxy dell'applicazione AD Azure
In precedenza, è stato effettuato il provisioning di una macchina virtuale di Windows Server e di partecipare al programma dominio gestito toohello. In questa attività, installare connettore Proxy dell'applicazione AD Azure hello in questa macchina virtuale.

1. Copia hello connettore installazione pacchetto toohello macchina virtuale in cui si installa connettore Proxy applicazione Web di Azure AD hello.

2. Eseguire **AADApplicationProxyConnectorInstaller.exe** sulla macchina virtuale hello. Accettazione delle condizioni di licenza software hello.

    ![Accettare le condizione per l'installazione](./media/app-proxy/app-proxy-install-connector-terms.png)
3. Durante l'installazione, verrà richiesta tooregister hello connettore con hello Proxy di applicazione della directory di Azure AD.
    * Specificare le **credenziali di amministratore globale di Azure AD**. Il tenant di amministratore globale può essere diverso dalle credenziali di Microsoft Azure.
    * Hello amministratore account utilizzato tooregister hello connettore deve appartenere toohello stessa directory in cui è abilitato il servizio di Proxy applicazione hello. Ad esempio, se hello tenant è contoso.com, deve essere salve admin@contoso.com o qualsiasi altro alias valido in quel dominio.
    * Se sicurezza avanzata di Internet Explorer è attivata per il server di hello in cui si sta installando il connettore di hello, schermata di registrazione hello potrebbe essere bloccato. accesso tooallow, seguire le istruzioni di hello nel messaggio di errore hello. Verificare che Internet Explorer Enhanced Security Context sia disabilitato.
    * Se la registrazione del connettore non riesce, vedere [Risolvere i problemi del Proxy applicazione](../active-directory/active-directory-application-proxy-troubleshoot.md).

    ![Connettore installato](./media/app-proxy/app-proxy-connector-installed.png)
4. connettore hello tooensure funziona correttamente, hello esecuzione dei problemi di connettore Proxy di applicazione di Azure Active Directory. Dopo la risoluzione dei problemi di hello in esecuzione, verrà visualizzato un report ha esito positivo.

    ![Esito positivo dello strumento di risoluzione dei problemi](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. Dovrebbe essere elencato nella pagina di proxy applicazione hello nella directory di Azure AD connettore di hello appena installato.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> È possibile scegliere i connettori tooinstall su più server tooguarantee la disponibilità elevata per l'autenticazione delle applicazioni pubblicate mediante hello Proxy dell'applicazione AD Azure. Eseguire hello stessi passaggi elencati in precedenza connettore hello tooinstall altro dominio gestito di tooyour aggiunti a un server.
>
>

## <a name="next-steps"></a>Passaggi successivi
È impostato hello Proxy dell'applicazione Azure Active Directory e si è integrato con il dominio gestito di servizi di dominio Active Directory di Azure.

* **Eseguire la migrazione delle macchine virtuali di applicazioni tooAzure:** è possibile accuratezza di spostamento e le applicazioni dal locale server tooAzure tooyour unita in join le macchine virtuali gestite dominio. In questo modo consente di eliminare i costi di infrastruttura hello dell'esecuzione di server locali.

* **Pubblicare applicazioni mediante il Proxy di applicazione AD Azure:** pubblicare applicazioni in esecuzione in macchine virtuali di Azure utilizzando hello Proxy dell'applicazione AD Azure. Per altre informazioni, vedere l'articolo relativo alla [pubblicazione di applicazioni con il proxy di applicazione di Azure AD](../active-directory/application-proxy-publish-azure-portal.md).


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>Nota di distribuzione: pubblicare applicazioni con l'autenticazione integrata di Windows usando il proxy di applicazione di Azure AD
Consentire alle applicazioni single sign-on tooyour utilizzando l'autenticazione integrata di Windows (IWA) tramite la concessione dell'autorizzazione di connettori Proxy di applicazione tooimpersonate utenti e inviare e ricevere i token per loro conto. Configurare la delega vincolata kerberos (KCD) per hello connettore toogrant hello necessarie autorizzazioni tooaccess le risorse nel dominio gestito hello. Per una maggiore sicurezza, utilizzare il meccanismo di delega vincolata Kerberos basata sulle risorse di hello in domini gestiti.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Abilitare la delega vincolata kerberos basata sulle risorse per il connettore Proxy dell'applicazione hello Azure AD
Hello Proxy dell'applicazione Azure connector deve essere configurato per la delega vincolata kerberos (KCD), in modo che può rappresentare gli utenti nel dominio gestito hello. In un dominio gestito di Azure AD Domain Services non si hanno privilegi di amministratore di dominio. Di conseguenza, **non è possibile configurare la delega vincolata Kerberos tradizionale a livello di account in un dominio gestito**.

Usare la delega vincolata Kerberos basata su risorse, come illustrato in [questo articolo](active-directory-ds-enable-kcd.md).

> [!NOTE]
> È necessario toobe un membro del gruppo 'Administrators di controller di dominio di AAD' hello, hello tooadminister gestiti dominio utilizzando i cmdlet PowerShell di Active Directory.
>
>

Impostazioni hello PowerShell Get-ADComputer cmdlet tooretrieve hello per computer hello in cui hello Proxy dell'applicazione Azure Active Directory è installato connettore.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

Successivamente, usare tooset cmdlet Set-ADComputer hello backup basata sulle risorse delega vincolata Kerberos per server di risorse hello.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

Se sono stati distribuiti più connettori Proxy di applicazione nel dominio gestito, è necessario tooconfigure la delega vincolata Kerberos basata sulle risorse per ogni istanza di tale connettore.


## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Configurare la delega vincolata Kerberos in un dominio gestito](active-directory-ds-enable-kcd.md)
* [Panoramica della delega vincolata Kerberos](https://technet.microsoft.com/library/jj553400.aspx)
