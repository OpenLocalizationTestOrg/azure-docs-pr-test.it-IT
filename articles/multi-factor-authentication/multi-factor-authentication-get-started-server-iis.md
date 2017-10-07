---
title: "aaaIIS l'autenticazione e Server di autenticazione a più fattori di Azure | Documenti Microsoft"
description: Si tratta hello Azure multi-factor authentication pagina di supporto nella distribuzione dell'autenticazione IIS e il Server Azure multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>Configurazione di Azure Multi-Factor Authentication per le App Web IIS

Utilizzare sezione autenticazione IIS hello di hello Server Azure multi-Factor Authentication (MFA) tooenable e configurare l'autenticazione IIS per l'integrazione con applicazioni web IIS Microsoft. Hello Azure MFA Server viene installato un plug-in che è possibile filtrare le richieste inoltrate toohello IIS web server tooadd Azure multi-Factor Authentication. Hello plug-in IIS fornisce supporto per l'autenticazione basata su Form e l'autenticazione HTTP integrata di Windows. Attendibili che gli indirizzi IP possono anche essere tooexempt configurato gli indirizzi IP interni dall'autenticazione a due fattori.

![Autenticazione IIS](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>Uso dell'autenticazione IIS basata su form con il server Azure Multi-Factor Authentication
toosecure IIS web dell'applicazione che utilizza l'autenticazione basata su form, installare hello del Server Azure multi-Factor Authentication nel server web IIS di hello e configurare hello Server per ogni procedura hello:

1. In hello del Server Azure multi-Factor Authentication, fare clic sull'icona autenticazione IIS hello nel menu a sinistra di hello.
2. Fare clic su hello **basata su Form** scheda.
3. Fare clic su **Aggiungi**.
4. le variabili nome utente, password e dominio toodetect automaticamente, immettere hello URL di accesso (ad esempio, https://localhost/contoso/auth/login.aspx) nella finestra di dialogo Configura automaticamente sito Web di hello e fare clic su **OK**.
5. Controllare hello **corrispondenza utente di multi-Factor Authentication richiedono** se tutti gli utenti sono stati o verranno importati nel Server hello e soggetto toomulti-factor authentication. Se un numero significativo di utenti non è ancora stato importato nel Server hello e/o esenti dall'autenticazione a più fattori, lasciare deselezionata la casella hello.
6. Se le variabili di pagina hello non possono essere rilevate automaticamente, fare clic su **specificare manualmente** nella finestra di dialogo Configura automaticamente sito Web di hello.
7. Nella finestra di dialogo Aggiungi sito Web di hello, immettere nella pagina account di accesso URL toohello hello nel campo URL di invio hello e immettere un nome di applicazione (facoltativo). nome dell'applicazione Hello viene visualizzato nei report di Azure multi-Factor Authentication e potrebbe essere visualizzato all'interno di messaggi di autenticazione SMS o App per dispositivi mobili.
8. Selezionare il formato di richiesta corretto hello. Questa proprietà è impostata troppo**POST o GET** per la maggior parte delle applicazioni web.
9. Immettere variabile nome utente hello, la variabile Password e variabili di dominio (se è presente nella pagina di accesso hello). nomi hello toofind di hello caselle di input, passare toohello pagina di accesso in un web browser, fare clic su pagina hello e selezionare **Visualizza origine**.
10. Controllare hello **corrispondenza utente richiedono Azure multi-Factor Authentication** se tutti gli utenti sono stati o verranno importati nel Server hello e soggetto toomulti-factor authentication. Se un numero significativo di utenti non è ancora stato importato nel Server hello e/o esenti dall'autenticazione a più fattori, lasciare deselezionata la casella hello.
11. Fare clic su **avanzate** tooreview le impostazioni avanzate, tra cui:

  - Selezionare un file di paging di rifiuto personalizzato
  - Sito Web toohello di cache le autenticazioni riuscite per un periodo di tempo utilizzando cookie
  - Selezionare se credenziali tooauthenticate hello primario in un dominio di Windows, la directory LDAP. o in un server RADIUS.

12. Fare clic su **OK** finestra di dialogo Aggiungi sito Web toohello tooreturn.
13. Fare clic su **OK**.
14. Una volta hello URL e rilevate o immesse le variabili di pagina, vengono visualizzati dati del sito Web hello in hello pannello basata su Form.

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>Uso dell'autenticazione integrata di Windows con il server Azure Multi-Factor Authentication
toosecure IIS web dell'applicazione che utilizza l'autenticazione HTTP integrata di Windows, installare hello Azure MFA Server nel server web IIS di hello, quindi configurare hello Server con hello alla procedura seguente:

1. In hello del Server Azure multi-Factor Authentication, fare clic sull'icona autenticazione IIS hello nel menu a sinistra di hello.
2. Fare clic su hello **HTTP** scheda.
3. Fare clic su **Aggiungi**.
4. Nella finestra di dialogo Aggiungi URL di Base di hello, immettere l'URL di hello per il sito Web di hello in cui viene eseguita l'autenticazione HTTP (ad esempio, http://localhost/owa) e specificare un nome di applicazione (facoltativo). nome dell'applicazione Hello viene visualizzato nei report di Azure multi-Factor Authentication e potrebbe essere visualizzato all'interno di messaggi di autenticazione SMS o App per dispositivi mobili.
5. Se i timeout di inattività hello e massimo sessione predefinita hello non è sufficiente.
6. Controllare hello **corrispondenza utente di multi-Factor Authentication richiedono** se tutti gli utenti sono stati o verranno importati nel Server hello e soggetto toomulti-factor authentication. Se un numero significativo di utenti non è ancora stato importato nel Server hello e/o esenti dall'autenticazione a più fattori, lasciare deselezionata la casella hello.
7. Controllare hello **cache dei Cookie** casella se si desidera.
8. Fare clic su **OK**.

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>Abilitare i plug-in di IIS per il server Azure Multi-Factor Authentication
Dopo aver configurato hello basata su Form o URL dell'autenticazione HTTP e impostazioni, selezionare hello posizioni in cui hello plug-in IIS di Azure multi-Factor Authentication deve essere caricato e abilitato in IIS. Utilizzare hello seguente procedura:

1. Se in esecuzione in IIS 6, fare clic su hello **ISAPI** scheda. Sito Web selezionare hello hello applicazione web è in esecuzione in (ad esempio, sito Web predefinito) tooenable hello Azure multi-Factor Authentication filtro ISAPI plug-in per il sito.
2. Se in esecuzione in IIS 7 o versione successiva, fare clic su hello **modulo nativo** scheda. Selezionare server hello, siti Web o applicazioni tooenable hello plug-in IIS livelli hello desiderato.
3. Fare clic su hello **autenticazione IIS abilitare** casella in alto hello hello. Applicazione di IIS hello selezionata è ora protetta da Azure multi-Factor Authentication. Verificare che gli utenti siano stati importati nel Server hello.

## <a name="trusted-ips"></a>IP attendibili
Hello gli indirizzi IP attendibili consente agli utenti toobypass Azure multi-Factor Authentication per le richieste del sito Web provenienti da specifici indirizzi IP o subnet. Ad esempio, è consigliabile tooexempt utenti da Azure multi-Factor Authentication durante l'accesso dall'ufficio hello. A tale scopo, è necessario specificare subnet dell'ufficio hello come una voce di indirizzi IP attendibili. tooconfigure indirizzi IP attendibili, utilizzare hello seguente procedura:

1. Nella sezione autenticazione IIS hello, fare clic su hello **gli indirizzi IP attendibili** scheda.
2. Fare clic su **Aggiungi**.
3. Quando viene visualizzata la finestra di dialogo di hello aggiungere gli indirizzi IP attendibili, selezionare hello **IP singolo**, **intervallo IP**, o **Subnet** pulsante di opzione.
4. Immettere l'indirizzo IP hello, intervallo di indirizzi IP o subnet che deve essere abilitata. Se l'immissione di una subnet, hello seleziona la Netmask appropriata e fare clic su **OK**. ora è stata aggiunta Hello whitelist.
