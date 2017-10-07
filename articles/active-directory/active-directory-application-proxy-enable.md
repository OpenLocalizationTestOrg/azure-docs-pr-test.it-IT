---
title: Introduzione AD App Proxy - aaaAzure installare connettore | Documenti Microsoft
description: Attivare il Proxy di applicazione nel portale di Azure hello e installare i connettori hello di proxy inverso hello.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a>Iniziare con Proxy dell'applicazione e installare il connettore hello
In questo articolo illustra hello passaggi tooenable Proxy di applicazione di Microsoft Azure AD per la directory cloud in Azure AD.

Se non si è ancora visualizzata Proxy dell'applicazione considerare i vantaggi di produttività e sicurezza hello tooyour organizzazione, altre informazioni, vedere [come tooprovide proteggere l'accesso remoto applicazioni locali tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Prerequisiti del proxy dell'applicazione
Prima di poter abilitare e utilizzare servizi Proxy dell'applicazione, è necessario toohave:

* Una [sottoscrizione di Microsoft Azure AD Basic o Premium](active-directory-editions.md) e una directory di Azure AD di cui si è un amministratore globale.
* Un server che esegue Windows Server 2012 R2 o 2016, in cui è possibile installare hello connettore Proxy dell'applicazione. Hello server necessita di servizi di toobe tooconnect in grado di toohello Proxy dell'applicazione nel cloud hello e hello applicazioni locali che si desidera pubblicare.
  * Per single sign-on tooyour applicazioni pubblicate mediante la delega vincolata Kerberos, la macchina deve essere dominio nel dominio hello stesso Active Directory come applicazioni hello che si desidera pubblicare. Per informazioni, vedere [KCD for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md) (KDC per l'Accesso Single Sign-On con il proxy di applicazione).

Se l'organizzazione utilizza proxy toohello tooconnect server internet, leggere [lavoro con esistente proxy server locali](application-proxy-working-with-proxy-servers.md) per informazioni dettagliate su come tooconfigure li prima di ottenere avviato con Proxy dell'applicazione.

## <a name="open-your-ports"></a>Aprire le porte

tooprepare l'ambiente per il Proxy di applicazione di Azure Active Directory, è innanzitutto necessario tooenable comunicazione tooAzure data center. Se nel percorso di hello è presente un firewall, assicurarsi che sia aperta in modo che hello che connettore può rendere HTTPS (TCP) richiede toohello Proxy dell'applicazione.

1. Le porte seguenti hello aperto troppo**in uscita** traffico:

   | Numero della porta | Uso |
   | --- | --- |
   | 80 | Download di revoca dei certificati elenchi (CRL) durante la convalida del certificato SSL hello |
   | 443 | Tutte le comunicazioni in uscita con il servizio Proxy di applicazione hello |

   Se il firewall impone il traffico in base agli utenti di toooriginating, aprire le porte per il traffico da servizi di Windows che vengono eseguiti come un servizio di rete.

   > [!IMPORTANT]
   > tabella Hello riflette i requisiti delle porte per le versioni connettore 1.5.132.0 hello e più recenti. Se si dispone ancora di una versione precedente di connettore, è necessario anche hello tooenable seguendo le porte in aggiunta too80 e 443:5671, 8080, 9090-9091, 9350, 9352, 10100 – 10120.
   >
   >Per informazioni sull'aggiornamento di versione più recente toohello connettori, vedere [connettori Proxy di applicazione AD Azure comprendere](application-proxy-understand-connectors.md#automatic-updates).

2. Se il firewall o proxy consente whitelist DNS, è possibile n e t e toomsappproxy.net connessioni whitelist. Se non è necessario tooallow accesso toohello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653), che vengono aggiornati ogni settimana.

3. Microsoft utilizza i certificati di tooverify quattro indirizzi. Consenti accesso toohello URL seguenti se è ancora fatto per altri prodotti:
   * mscrl.microsoft.com:80
   * crl.microsoft.com:80
   * ocsp.msocsp.com:80
   * www.microsoft.com:80

4. Il connettore richiede accesso toologin.windows.net e login.microsoftonline.net per il processo di registrazione hello.

5. Hello utilizzare [Azure AD applicazione Proxy porte Test strumento connettore](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify che il connettore può raggiungere il servizio di Proxy applicazione hello. Come minimo, assicurarsi che area Stati Uniti centro hello e hello area più vicina tooyou hanno tutti i segni di spunta verde. La presenza di più segni di spunta verdi indica una maggiore resilienza.

## <a name="install-and-register-a-connector"></a>Installare e registrare un connettore
1. Accedere come amministratore in hello [portale di Azure](https://portal.azure.com/).
2. La directory corrente viene visualizzata sotto il nome utente nell'angolo superiore destro di hello. Se è necessario toochange directory, selezionare l'icona.
3. Andare troppo**Azure Active Directory** > **Proxy dell'applicazione**.

   ![Passare tooApplication Proxy](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. Selezionare **Scarica connettore**.

   ![Scaricare il connettore](./media/active-directory-application-proxy-enable/download_connector.png)

5. Eseguire **AADApplicationProxyConnectorInstaller.exe** sul server hello preparato secondo toohello prerequisiti.
6. Seguire le istruzioni hello tooinstall guidata hello. Durante l'installazione, verrà richiesta tooregister hello connettore con hello Proxy applicazione del tenant di Azure AD.

   * Fornire le credenziali di amministratore globale di Azure AD. Il tenant di amministratore globale può essere diverso dalle credenziali di Microsoft Azure.
   * Assicurarsi che il servizio Proxy di applicazione di hello salve che hello di registri hello connettore si trova nella stessa directory in cui è abilitato. Ad esempio, se hello tenant è contoso.com, deve essere salve admin@contoso.com o qualsiasi altro alias su tale dominio.
   * Se **sicurezza avanzata di Internet Explorer** è troppo**su** nel server in cui si sta installando il connettore hello hello potrebbe non essere visualizzata la schermata di registrazione hello. accesso tooget, seguire le istruzioni di hello nel messaggio di errore hello. Verificare che Internet Explorer Enhanced Security Context sia disabilitato.

Per ottenere una disponibilità elevata, è consigliabile distribuire almeno due connettori. Ogni connettore deve essere registrato separatamente.

## <a name="test-that-hello-connector-installed-correctly"></a>Test di tale connettore hello installato correttamente

È possibile confermare che un nuovo connettore installato correttamente controllando che in entrambi hello portale di Azure o nel server. 

In hello portale di Azure, accedere tooyour tenant e passare troppo**Azure Active Directory** > **Proxy dell'applicazione**. Tutti i connettori e i gruppi di connettori vengono visualizzati in questa pagina. Selezionare i dettagli di un connettore toosee o inserirlo in un gruppo di connettori diversi. 

Nel server, controllare l'elenco di hello dei servizi attivi per il connettore di hello e aggiornamento del connettore hello. due servizi Hello devono avviare immediatamente l'esecuzione, ma in caso contrario, attivarli: 

   * **Microsoft AAD Application Proxy Connector** abilita la connettività.

   * **Microsoft AAD Application Proxy Connector Updater** è un servizio di aggiornamento automatico. Verifica aggiornamento Hello per le nuove versioni del connettore hello e aggiornamenti hello connettore in base alle esigenze.

   ![Servizi del connettore proxy di applicazione - Screenshot](./media/active-directory-application-proxy-enable/app_proxy_services.png)

Per informazioni sui connettori e come rimanere backup toodate, vedere [connettori Proxy di applicazione AD Azure comprendere](application-proxy-understand-connectors.md).


## <a name="next-steps"></a>Passaggi successivi
Si è pronti a questo punto troppo[pubblicare applicazioni con Proxy dell'applicazione](application-proxy-publish-azure-portal.md).

Se si hanno applicazioni che si trovano in reti o posizioni diverse, è possibile utilizzare connettore gruppi tooorganize hello diversi connettori in unità logiche. Per altre informazioni, vedere [Pubblicare applicazioni in reti e posizioni separate tramite i gruppi di connettori](active-directory-application-proxy-connectors-azure-portal.md).
