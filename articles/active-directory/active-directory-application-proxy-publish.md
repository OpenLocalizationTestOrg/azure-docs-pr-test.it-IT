---
title: App aaaPublish con Proxy dell'applicazione Azure AD | Documenti Microsoft
description: Pubblicare cloud toohello di applicazioni on-premise con Proxy dell'applicazione Azure Active Directory nel portale classico hello.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Pubblicare applicazioni mediante il proxy di applicazione AD Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](application-proxy-publish-azure-portal.md)
> * [portale di Azure classico](active-directory-application-proxy-publish.md)

Proxy dell'applicazione Azure Active Directory consente di supportare gli utenti remoti mediante la pubblicazione toobe applicazioni locale accessibili tramite hello internet. A questo punto si dovrebbe già disporre [abilitato Proxy dell'applicazione nel portale di Azure classico hello](active-directory-application-proxy-enable.md). In questo articolo illustra hello passaggi toopublish le applicazioni in esecuzione nella rete locale e fornire l'accesso remoto sicuro dall'esterno della rete. Dopo aver completato questo articolo, sarà un'applicazione hello tooconfigure pronto con informazioni personalizzate o requisiti di sicurezza.

> [!NOTE]
> Proxy dell'applicazione è una funzionalità che è disponibile solo se è stato aggiornato toohello Premium o Edizione Basic di Azure Active Directory. Per altre informazioni, vedere [Edizioni di Azure Active Directory](active-directory-editions.md). Se si desidera toouse Proxy dell'applicazione, è possibile [pubblicare applicazioni nel portale di Azure hello](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Pubblicare un'app usando la procedura guidata hello
1. Accedere come amministratore in hello [portale di Azure classico](https://manage.windowsazure.com/).
2. TooActive Directory scegliere directory hello in cui è abilitato il Proxy di applicazione.
   
    ![Active Directory - Icona](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Fare clic su hello **applicazioni** scheda e quindi fare clic su hello **Aggiungi** pulsante in basso hello hello
   
    ![Aggiungi applicazione](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Selezionare **Pubblica un'applicazione che sarà accessibile dall'esterno della rete**.
   
    ![Pubblica un'applicazione che sarà accessibile dall'esterno della rete](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Fornire le seguenti informazioni sull'applicazione hello:
   
   * **Nome**: nome descrittivo di hello per l'applicazione. Deve essere univoco all'interno della directory.
   * **URL interno**: indirizzo hello hello connettore Proxy dell'applicazione utilizza un'applicazione hello tooaccess dall'interno della rete privata. È possibile fornire un percorso specifico in hello toopublish di server back-end, mentre il resto di hello del server hello è pubblicato. In questo modo, è possibile pubblicare i siti diversi hello nello stesso server e assegnare a ognuno di essi proprie regole di accesso e nome.
     
     > [!TIP]
     > Se si pubblica un percorso, assicurarsi che includa tutte le immagini necessarie hello, script e fogli di stile per l'applicazione. Ad esempio, se l'app in https://yourapp/app e Usa le immagini che si trova in https://yourapp/media, è necessario pubblicare https://yourapp/ come percorso di hello.
     > 
     > 
   * **Metodo di preautenticazione**: come Proxy di applicazione verifica gli utenti prima di concedere loro accesso tooyour applicazione. Scegliere una delle opzioni di hello dal menu a discesa hello.
     
     * Azure Active Directory: Proxy applicazione reindirizza toosign gli utenti con Azure AD, che autentica le autorizzazioni per directory hello e applicazione.
     * Pass-through: Gli utenti non sono un'applicazione hello tooaccess tooauthenticate.
     
     ![Proprietà dell'applicazione](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. procedura guidata hello toofinish, fare clic su hello segno di spunta in basso hello hello. un'applicazione Hello è ora definita in Azure AD.

## <a name="assign-users-and-groups-toohello-application"></a>Assegnare gli utenti e gruppi toohello applicazione
In ordine per gli utenti tooaccess l'applicazione pubblicata, è necessario tooassign li singolarmente o in gruppi. (Tenere presente tooassign manualmente, accesso troppo accedere.) Ogni utente assegnato deve avere una licenza Azure Basic o superiore. È possibile assegnare licenze singolarmente o toogroups. Per ulteriori informazioni, vedere [l'assegnazione di utenti applicazione tooan](active-directory-applications-guiding-developers-assigning-users.md). 

Per le applicazioni che richiedono la preautenticazione, assegnazione di un utente concede un'applicazione hello toouse autorizzazione. Per le app che non richiedono la preautenticazione, assegnazione di un utente significa che tale utente di hello può accedere a un'applicazione hello tramite il pannello di accesso di hello.

1. Dopo il completamento procedura guidata Aggiungi App di hello, vedrai hello pagina per l'applicazione di avvio rapido. toomanage che dispone di accesso toohello app, selezionare **utenti e gruppi**.
   
    ![Assegnazione degli utenti nella pagina Avvio rapido per il proxy di applicazione - Screenshot](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Cercare gruppi specifici nella propria directory oppure visualizzare tutti gli utenti. risultati della ricerca hello toodisplay, fare clic su hello segno di spunta.
   
      ![Ricerca di gruppi o utenti - Screenshot](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Selezionare ogni utente o gruppo tooassign toothis app desiderata, quindi scegliere **assegnare**. Si è richiesto tooconfirm questa azione.

> [!NOTE]
> Per le app con autenticazione integrata di Windows, è possibile assegnare solo utenti e gruppi sincronizzati da Active Directory locale. Non è possibile assegnare utenti che accedono con account Microsoft e guest per le app pubblicate con il proxy di applicazione di Azure Active Directory. Assicurarsi che gli utenti l'accesso con credenziali che fanno parte di hello nello stesso dominio applicazione hello si esegue la pubblicazione.
> 
> 

## <a name="test-your-published-application"></a>Testare l'applicazione pubblicata
Dopo aver pubblicato l'applicazione, è possibile eseguirne il test out passando toohello URL che è stato pubblicato. Verificare che sia possibile accedervi, che il rendering venga eseguito correttamente e che tutto funzioni come previsto. Se si riscontrano problemi o ottiene un messaggio di errore, provare a hello [risoluzione dei problemi guida](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Configurare l'applicazione
È possibile modificare le app pubblicate o impostare le opzioni avanzate nella pagina Configurazione hello. In questa pagina, è possibile personalizzare l'applicazione modifica nome hello oppure caricare un logo. È inoltre possibile gestire le regole di accesso come hello metodo di preautenticazione o multi-factor authentication.

![Configurazione avanzata](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Dopo la pubblicazione di applicazioni mediante il Proxy applicazione di Azure Active Directory, vengono visualizzati nell'elenco delle applicazioni hello in Azure AD ed è possibile gestirle.

Se si disabilitino servizi Proxy dell'applicazione dopo la pubblicazione delle applicazioni, applicazioni hello non sono più accessibili dall'esterno della rete privata. Gli utenti possono accesso hello applicazioni locale come di consueto.

Fare doppio clic sul nome di hello dell'applicazione hello tooview un'applicazione e apportare garantire che sia accessibile. Se il servizio Proxy di applicazione hello è disabilitato e applicazione hello non è disponibile, viene visualizzato un messaggio di avviso in alto hello hello.

toodelete un'applicazione, selezionare un'applicazione nell'elenco di hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi
* [Pubblicare applicazioni mediante il proprio nome di dominio](active-directory-application-proxy-custom-domains.md)
* [Abilitare l'accesso Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)
* [Abilitare l'accesso condizionale](active-directory-application-proxy-conditional-access.md)
* [Lavorare con applicazioni grado di riconoscere attestazioni](active-directory-application-proxy-claims-aware-apps.md)

Per informazioni più recenti hello e gli aggiornamenti, consultare hello [blog del Proxy dell'applicazione](http://blogs.technet.com/b/applicationproxyblog/)

