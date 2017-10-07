---
title: Proxy dell'applicazione AD Azure nel portale classico hello aaaEnable | Documenti Microsoft
description: Accendere il Proxy di applicazione nel portale di Azure classico hello e installare i connettori di hello per il proxy inverso hello.
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
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Abilitare il Proxy di applicazione nel portale classico hello e scaricare i connettori
In questo articolo illustra hello passaggi tooenable Proxy di applicazione di Microsoft Azure AD per la directory cloud in Azure AD.

Se si ha familiarità con le quali il Proxy di applicazione consente di eseguire, altre informazioni, vedere [come tooprovide proteggere l'accesso remoto applicazioni locali tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Prerequisiti del proxy dell'applicazione
Prima di poter abilitare e utilizzare servizi Proxy dell'applicazione, è necessario toohave:

* Una [sottoscrizione di Microsoft Azure AD Basic o Premium](active-directory-editions.md) e una directory di Azure AD di cui si è un amministratore globale.
* Un server che esegue Windows Server 2012 R2 o 2016, in cui è possibile installare hello connettore Proxy dell'applicazione. Hello server invia le richieste di servizi Proxy dell'applicazione toohello nel cloud hello e richiede un HTTP o HTTPS connessione toohello le applicazioni che si desidera pubblicare.
  * Per single sign-on tooyour pubblicazione delle applicazioni, la macchina deve essere dominio nel dominio hello stesso Active Directory come applicazioni hello che si desidera pubblicare. Per altre informazioni, vedere [Accesso Single Sign-On con il proxy di applicazione](active-directory-application-proxy-sso-using-kcd.md)
* Se l'organizzazione utilizza proxy toohello tooconnect server internet, leggere [lavoro con esistente proxy server locali](application-proxy-working-with-proxy-servers.md) per informazioni dettagliate su come tooconfigure li.

## <a name="open-your-ports"></a>Aprire le porte

tooprepare l'ambiente per il Proxy di applicazione di Azure Active Directory, è innanzitutto necessario tooenable comunicazione tooAzure data center. Se nel percorso di hello è presente un firewall, assicurarsi che sia aperta in modo che hello che connettore può rendere HTTPS (TCP) richiede toohello Proxy dell'applicazione.

1. Le porte seguenti hello aperto troppo**in uscita** traffico:

   | Numero della porta | Uso |
   | --- | --- |
   | 80 | Download di revoca dei certificati elenchi (CRL) durante la convalida del certificato SSL hello |
   | 443 | Tutte le comunicazioni in uscita con il servizio Proxy di applicazione hello |

   Se il firewall impone il traffico in base agli utenti di toooriginating, aprire le porte per il traffico proveniente da servizi di Windows in esecuzione come servizio di rete.

   > [!IMPORTANT]
   > tabella Hello riflette i requisiti delle porte per le versioni connettore 1.5.132.0 hello e più recenti. Se si dispone ancora di una versione precedente di connettore, è necessario anche hello tooenable seguenti porte: 5671, 8080, 9090, 9091, 9350, 9352 e 10100 – 10120.
   >
   >Per informazioni sull'aggiornamento di versione più recente toohello connettori, vedere [connettori Proxy di applicazione AD Azure comprendere](application-proxy-understand-connectors.md#automatic-updates).

2. Se il firewall o proxy consente whitelist DNS, è possibile n e t e toomsappproxy.net connessioni whitelist. Se non è necessario tooallow accesso toohello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653), che vengono aggiornati ogni settimana.

3. Hello utilizzare [Azure AD applicazione Proxy porte Test strumento connettore](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify che il connettore può raggiungere il servizio di Proxy applicazione hello. Come minimo, assicurarsi che area Stati Uniti centro hello e hello area più vicina tooyou hanno tutti i segni di spunta verde. La presenza di più segni di spunta verdi indica una maggiore resilienza.

## <a name="enable-application-proxy-in-azure-ad"></a>Abilitare il proxy di applicazione in Azure AD
1. Accedere come amministratore in hello [portale di Azure classico](https://manage.windowsazure.com/).
2. TooActive Directory scegliere hello directory in cui si desidera tooenable Proxy dell'applicazione.

    ![Active Directory - Icona](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Selezionare **configura** nella pagina directory hello e scorrere verso il basso troppo**Proxy dell'applicazione**.
4. Attiva/disattiva **Abilita servizi Proxy dell'applicazione per questa Directory** troppo**abilitato**.

    ![Abilitare il proxy dell’applicazione](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. Selezionare **Scarica ora**. Hello **Azure Active Directory Application Proxy Connector Download** apre. Leggere e accettare hello condizioni di licenza e fare clic su **scaricare** toosave file di programma di installazione di Windows hello (.exe) per il connettore hello.

## <a name="install-and-register-hello-connector"></a>Installare e registrare hello connettore
1. Eseguire **AADApplicationProxyConnectorInstaller.exe** sul server hello preparato secondo toohello prerequisiti.
2. Seguire le istruzioni hello tooinstall guidata hello.
3. Durante l'installazione, verrà richiesta tooregister hello connettore con hello Proxy applicazione del tenant di Azure AD.

   * Fornire le credenziali di amministratore globale di Azure AD. Il tenant di amministratore globale può essere diverso dalle credenziali di Microsoft Azure.
   * Assicurarsi che il servizio Proxy di applicazione di hello salve che hello di registri hello connettore si trova nella stessa directory in cui è abilitato. Ad esempio, se hello tenant è contoso.com, deve essere salve admin@contoso.com o qualsiasi altro alias su tale dominio.
   * Se **sicurezza avanzata di Internet Explorer** è troppo**su** nel server hello hello schermata di registrazione sia bloccata. accesso tooallow, seguire le istruzioni di hello nel messaggio di errore hello. Verificare che Internet Explorer Enhanced Security Context sia disabilitato.
   * Se la registrazione del connettore non riesce, vedere [Risolvere i problemi del Proxy applicazione](active-directory-application-proxy-troubleshoot.md).  
4. Al termine dell'installazione di hello, due nuovi servizi vengono aggiunti tooyour server:

   * **Microsoft AAD Application Proxy Connector** abilita la connettività.

     * **Microsoft AAD Application Proxy Connector Updater** è un servizio di aggiornamento automatico. Periodicamente per le nuove versioni del connettore hello e aggiorna il connettore hello in base alle esigenze.

     ![Servizi del connettore proxy di applicazione - Screenshot](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Fare clic su **fine** nella finestra di installazione di hello.

Per informazioni sui connettori, vedere [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md) (Informazioni sui connettori proxy di applicazione di Azure AD).

Per ottenere una disponibilità elevata, è consigliabile distribuire almeno due connettori. toodeploy più connettori, ripetere i passaggi 2 e 3. Ogni connettore deve essere registrato separatamente.

Se si desidera toouninstall hello connettore, disinstallare il servizio connettore hello e servizio di aggiornamento hello. Riavviare il servizio di hello remove toofully computer.

## <a name="next-steps"></a>Passaggi successivi
Si è pronti a questo punto troppo[pubblicare applicazioni con Proxy dell'applicazione](active-directory-application-proxy-publish.md).

Se si hanno applicazioni che si trovano in reti o posizioni diverse, è possibile utilizzare connettore gruppi tooorganize hello diversi connettori in unità logiche. Per altre informazioni, vedere [Pubblicare applicazioni in reti e posizioni separate tramite i gruppi di connettori](active-directory-application-proxy-connectors.md).
