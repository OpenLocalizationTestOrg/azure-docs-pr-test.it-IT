---
title: l'autenticazione basata su aaaHeader con PingAccess per Proxy dell'applicazione Azure AD | Documenti Microsoft
description: Pubblicare applicazioni con PingAccess e App Proxy toosupport intestazione l'autenticazione basata su.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>Autenticazione basata su intestazione per l'accesso Single Sign-On con il proxy di applicazione e PingAccess

Proxy di Active Directory dell'applicazione Azure e PingAccess hanno collaborato insieme ai clienti di Azure Active Directory tooprovide con accesso tooeven altre applicazioni. PingAccess espande hello [offerte Proxy dell'applicazione esistente](active-directory-application-proxy-get-started.md) tooinclude accesso single sign-on tooapplications che utilizzano intestazioni per l'autenticazione.

## <a name="what-is-pingaccess-for-azure-ad"></a>Che cos'è PingAccess per Azure AD?

PingAccess per Azure Active Directory è un'offerta di PingAccess che consente di toogive agli utenti di accedere e single sign-on tooapplications che utilizzano intestazioni per l'autenticazione. Proxy dell'applicazione considera queste App come qualsiasi altro utilizzando accesso tooauthenticate ad Azure AD e quindi passando il traffico attraverso il servizio connettore hello. PingAccess si trova davanti App hello e token di accesso hello da Azure AD si traduce in un'intestazione in modo che un'applicazione hello riceve autenticazione hello in formato hello che è possibile leggere.

Gli utenti non notare che, quando effettuano l'accesso toouse le app aziendale. Possono comunque lavorare da qualsiasi luogo e dispositivo. 

Poiché i connettori Proxy di applicazione hello indirizzano il traffico remoto tooall App indipendentemente dal tipo di autenticazione, verrà continuano saldo tooload automaticamente, anche.

## <a name="how-do-i-get-access"></a>Come si ottiene l'accesso?

Poiché questo scenario è il risultato di una partnership fra Azure Active Directory e PingAccess, sono necessarie le licenze per entrambi i servizi. Tuttavia, le sottoscrizioni di Azure Active Directory Premium includono una licenza di base PingAccess che riguarda le applicazioni too20. Se è necessario toopublish più di 20 applicazioni basate su intestazione, è possibile acquistare una licenza aggiuntiva da PingAccess. 

Per altre informazioni, vedere [Edizioni di Azure Active Directory](active-directory-editions.md).

## <a name="publish-your-application-in-azure"></a>Pubblicare l'applicazione in Azure

In questo articolo è destinato a utenti che pubblicano un'app con questo scenario per hello prima volta. Illustra in dettaglio come tooget iniziare con l'applicazione sia PingAccess, inoltre toohello procedura per la pubblicazione. Se si desidera che un aggiornamento su hello pubblicazione passaggi sono già state configurate entrambi i servizi, è possibile ignorare l'installazione del connettore hello e sposta troppo[aggiungere il tooAzure app Active Directory con Proxy dell'applicazione](#add-your-app-to-Azure-AD-with-Application-Proxy).

>[!NOTE]
>Poiché questo scenario è una relazione tra Azure AD e PingAccess, alcune istruzioni hello disponibile nel sito Ping identità hello.

### <a name="install-an-application-proxy-connector"></a>Installare un connettore proxy di applicazione

Se si dispone già abilitato per il Proxy dell'applicazione e dispone di un connettore installato, è possibile ignorare questa sezione e passare troppo[aggiungere il tooAzure app Active Directory con Proxy dell'applicazione](#add-your-app-to-azure-ad-with-application-proxy).

connettore Proxy dell'applicazione Hello è un Server di Windows del servizio che indirizza il traffico di hello da tooyour i dipendenti remoti App pubblicate. Per istruzioni dettagliate, vedere [abilitare i Proxy di applicazione nel portale di Azure hello](active-directory-application-proxy-enable.md).

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore globale.
2. Selezionare **Azure Active Directory** > **Proxy dell'applicazione**.
3. Selezionare **Scarica connettore** download del connettore Proxy dell'applicazione di toostart hello. Seguire le istruzioni di installazione di hello.

   ![Abilitare il Proxy di applicazione e scaricare il connettore hello](./media/application-proxy-ping-access/install-connector.png)

4. Download hello connector deve abilitare automaticamente il Proxy di applicazione per la directory, ma se non è possibile selezionare **abilitare il Proxy di applicazione**.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>Aggiungere il tooAzure app Active Directory con Proxy dell'applicazione

Esistono due azioni, è necessario tootake in hello portale di Azure. In primo luogo, è necessario toopublish l'applicazione con Proxy dell'applicazione. Quindi, è necessario toocollect alcune informazioni sull'applicazione hello che è possibile utilizzare durante la procedura PingAccess hello.

Seguire questi passaggi toopublish l'app. Per una descrizione più dettagliata dei passaggi 1-8, vedere [Pubblicare applicazioni mediante il proxy di applicazione AD Azure](application-proxy-publish-azure-portal.md).

1. Se non si è nell'ultima sezione hello, accedi toohello [portale di Azure](https://portal.azure.com) come amministratore globale.
2. Selezionare **Azure Active Directory** > **Applicazioni aziendali**.
3. Selezionare **Aggiungi** nella parte superiore di hello del pannello hello.
4. Selezionare **Applicazione locale**.
5. Compilare i campi necessario hello con informazioni sulla nuova app. Utilizzare istruzioni disponibili per le impostazioni di hello hello:
   - **URL interno**: in genere è fornire hello URL che consente di accesso dell'app toohello nella pagina quando si è nella rete aziendale hello. Per questo scenario il connettore di hello deve tootreat hello PingAccess proxy come pagina di front-hello dell'applicazione hello. Usare il formato seguente: `https://<host name of your PA server>:<port>`. porta Hello è 3000 per impostazione predefinita, ma è possibile configurarlo in PingAccess.
   - **Metodo di autenticazione preliminare**: Azure Active Directory
   - **Tradurre URL nelle intestazioni**: No

   >[!NOTE]
   >Se si tratta della prima applicazione, utilizzare la porta 3000 toostart e tornare tooupdate questa impostazione se si modifica la configurazione PingAccess. Se si tratta di app secondo o versioni successive, questo sarà necessario toomatch hello Listener configurate in PingAccess. Altre informazioni sui [listener in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).

6. Selezionare **Aggiungi** nella parte inferiore di hello del pannello hello. L'applicazione viene aggiunto e verrà visualizzato il menu di avvio rapido hello.
7. Nel menu di avvio rapido hello, selezionare **assegnare un utente per il testing**e aggiungere almeno un utente toohello applicazione. Verificare che l'account di test disponga di accesso toohello nell'applicazione locale.
8. Selezionare **assegnare** assegnazione di utente toosave hello test.
9. Nel Pannello di gestione di app hello, selezionare **Single sign-on**.
10. Scegliere **intestazione-sign-on basato su** dal menu a discesa hello. Selezionare **Salva**.

   >[!TIP]
   >Se questa è la prima volta tramite basato sulle intestazioni single sign-on, è necessario tooinstall PingAccess. toomake assicurarsi che la sottoscrizione di Azure viene associata automaticamente all'installazione di PingAccess, utilizzare hello collegamento questo toodownload pagina single sign-on PingAccess. È possibile aprire il sito di download di hello ora o tornare toothis pagina in un secondo momento. 

   ![Selezionare l'accesso basato su intestazione](./media/application-proxy-ping-access/sso-header.PNG)

11. Chiudere hello Enterprise applicazioni pannello o scorrere tutti hello modo toohello tooreturn sinistro toohello Azure Active Directory dal menu.
12. Selezionare **Registrazioni per l'app**.

   ![Selezionare Registrazioni per l'app](./media/application-proxy-ping-access/app-registrations.png)

13. Selezionare hello app appena aggiunto, quindi **gli URL di risposta**.

   ![Selezionare URL di risposta](./media/application-proxy-ping-access/reply-urls.png)

14. Controllare toosee se l'URL esterno di hello è assegnato tooyour app nel passaggio 5 è nell'elenco di URL di risposta hello. In caso contrario aggiungerlo ora.
15. Nel pannello Impostazioni applicazione di hello, selezionare **delle autorizzazioni necessarie**.

  ![Selezionare Autorizzazioni necessarie](./media/application-proxy-ping-access/required-permissions.png)

16. Selezionare **Aggiungi**. Per hello API, scegliere **Windows Azure Active Directory**, quindi **selezionare**. Per le autorizzazioni di hello, scegliere **lettura e scrittura tutte le applicazioni** e **Accedi e Leggi il profilo utente**, quindi **selezionare** e **eseguita**.  

  ![Autorizzazioni SELECT](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Raccogliere informazioni per i passaggi PingAccess hello

1. Nel pannello delle impostazioni dell'app selezionare **Proprietà**. 

  ![Selezionare Proprietà](./media/application-proxy-ping-access/properties.png)

2. Salvare hello **Id applicazione** valore. Quando si configura PingAccess viene utilizzato per l'ID client hello.
3. Nel pannello Impostazioni applicazione di hello, selezionare **chiavi**.

  ![Selezionare Chiavi](./media/application-proxy-ping-access/Keys.png)

4. Creare una chiave, immettere una descrizione della chiave e scegliere una data di scadenza dal menu a discesa hello.
5. Selezionare **Salva**. Viene visualizzato un GUID in hello **valore** campo.

  Salva questo valore a questo punto, poiché non sarà in grado di toosee nuovamente dopo averlo chiudere questa finestra.

  ![Creare una nuova chiave](./media/application-proxy-ping-access/create-keys.png)

6. Chiudere hello App registrazioni pannello o scorrere tutti hello modo toohello tooreturn sinistro toohello Azure Active Directory dal menu.
7. Selezionare **Proprietà**.
8. Salvare hello **ID Directory** GUID.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>Facoltativo: aggiornamento GraphAPI toosend i campi personalizzati

Per un elenco dei token di sicurezza che Azure AD invia per l'autenticazione, vedere [Riferimento al token di Azure AD](./develop/active-directory-token-and-claims.md). Se è necessaria un'attestazione personalizzata che invia altri token, utilizzare il campo GraphAPI tooset hello app *acceptMappedClaims* troppo**True**. È possibile utilizzare Azure AD Graph Explorer o Microsoft Graph toomake questa configurazione. 

In questo esempio viene usato Graph Explorer:

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>Scaricare PingAccess e configurare l'app

Ora che è stata completata tutti i passaggi di installazione hello Azure Active Directory, è possibile spostare in tooconfiguring PingAccess. 

Hello i passaggi dettagliati per hello PingAccess parte di questo scenario continua nella documentazione di Ping Identity, hello [configurare PingAccess per Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).

Questi passaggi consentono di eseguire il processo di hello di ottenere un account PingAccess se si dispone già di uno, installando hello PingAccess Server e creazione di una connessione Provider OIDC AD Azure con ID di Directory copiata dal portale di Azure hello hello. È quindi possibile utilizzare hello ID applicazione e la chiave valori toocreate una sessione Web su PingAccess. Successivamente è possibile impostare i mapping delle identità e creare l'host virtuale, il sito e l'applicazione.

### <a name="test-your-app"></a>Test dell'app

Dopo aver completato tutti questi passaggi, l'app dovrebbe funzionare. tootest, aprire un browser e passare l'URL esterno toohello creato quando si pubblica l'applicazione hello in Azure. Accedere con l'account di prova hello è assegnato toohello app.

## <a name="next-steps"></a>Passaggi successivi

- [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html) (Configurare PingAccess per Azure AD)
- [Come viene offerto l'accesso Single Sign-On dal proxy di applicazione di Azure AD?](application-proxy-sso-overview.md)
- [Risolvere i problemi del Proxy applicazione](active-directory-application-proxy-troubleshoot.md)
