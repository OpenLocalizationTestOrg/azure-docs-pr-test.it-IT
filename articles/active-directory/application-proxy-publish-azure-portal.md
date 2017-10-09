---
title: App aaaPublish con Proxy dell'applicazione Azure AD | Documenti Microsoft
description: Pubblicare cloud toohello di applicazioni on-premise con Proxy dell'applicazione Azure Active Directory nel portale di Azure hello.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Pubblicare applicazioni mediante il proxy di applicazione AD Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](application-proxy-publish-azure-portal.md)
> * [portale di Azure classico](active-directory-application-proxy-publish.md)

Proxy dell'applicazione Azure Active Directory (AD) consente di supportare gli utenti remoti mediante la pubblicazione toobe applicazioni locale accessibili tramite hello internet. È possibile pubblicare queste applicazioni tramite hello tooprovide portale Azure l'accesso remoto sicuro dall'esterno della rete.

In questo articolo illustra hello passaggi toopublish un'app locale con Proxy dell'applicazione. Dopo aver completato questo articolo, gli utenti verranno essere in grado di tooaccess l'app in modalità remota. E sarà pronto tooconfigure caratteristiche aggiuntive per un'applicazione hello come single sign-on, informazioni personalizzate e requisiti di sicurezza.

Se si tooApplication nuovo Proxy, ulteriori informazioni su questa funzionalità con articolo hello [come tooprovide proteggere l'accesso remoto applicazioni locali tooon](active-directory-application-proxy-get-started.md).


## <a name="publish-an-on-premises-app-for-remote-access"></a>Pubblicare un'applicazione locale per l'accesso remoto

Seguire questi toopublish passaggi le applicazioni con Proxy dell'applicazione. Se ancora stato già scaricato e configurato un connettore per l'organizzazione, andare troppo[iniziare con Proxy dell'applicazione e installare il connettore hello](active-directory-application-proxy-enable.md) primo e quindi pubblicare l'app.

> [!TIP]
> Se si sta testando il Proxy dell'applicazione per hello prima volta, scegliere un'applicazione che è configurata per l'autenticazione basata su password. Proxy dell'applicazione supporta altri tipi di autenticazione, ma le app basate su password sono hello tooget più semplice backup ed eseguire rapidamente. 

1. Accedere come amministratore in hello [portale di Azure](https://portal.azure.com/).
2. Selezionare **Azure Active Directory** > **Applicazioni aziendali** > **Nuova applicazione**.

  ![Aggiungere un'applicazione aziendale](./media/application-proxy-publish-azure-portal/add-app.png)

3. Selezionare **Tutte** quindi scegliere **Applicazione locale**.  

  ![Aggiungere una propria applicazione](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Fornire le seguenti informazioni sull'applicazione hello:

   - **Nome**: nome hello dell'applicazione hello che verrà visualizzato nel Pannello di accesso hello e nel portale di Azure hello. 

   - **URL interno**: hello URL utilizzato da un'applicazione hello tooaccess all'interno della rete privata. È possibile fornire un percorso specifico in hello toopublish di server back-end, mentre il resto di hello del server hello è pubblicato. In questo modo, è possibile pubblicare i siti diversi hello nello stesso server applicazioni diversi e assegnare a ognuno di essi proprie regole di accesso e nome.

     > [!TIP]
     > Se si pubblica un percorso, assicurarsi che includa tutte le immagini necessarie hello, script e fogli di stile per l'applicazione. Ad esempio, se l'app in https://yourapp/app e Usa le immagini che si trova in https://yourapp/media, è necessario pubblicare https://yourapp/ come percorso di hello. Pagina di destinazione hello toobe che agli utenti di vedere non dispone di questo URL interno. Per altre informazioni, vedere [Impostare una home page personalizzata per le app pubblicate tramite il proxy applicazione di Azure AD](application-proxy-office365-app-launcher.md).

   - **URL esterno**: hello indirizzo agli utenti verranno inviata tooin ordine tooaccess app hello dall'esterno della rete. Se non si desidera dominio Proxy di applicazione predefinito di hello toouse, conoscenza [domini personalizzati in Azure AD applicazione Proxy](active-directory-application-proxy-custom-domains.md).
   - **Pre-autenticazione**: come Proxy di applicazione verifica gli utenti prima di concedere loro accesso tooyour applicazione. 

     - Azure Active Directory: Proxy applicazione reindirizza toosign gli utenti con Azure AD, che autentica le autorizzazioni per directory hello e applicazione. È consigliabile lasciare questa opzione come impostazione predefinita di hello, in modo che è possibile usufruire delle funzionalità di sicurezza di Azure AD come accesso condizionale e multi-Factor Authentication.
     - Pass-through: Gli utenti non hanno tooauthenticate rispetto a un'applicazione hello tooaccess Azure Active Directory. È comunque possibile impostare i requisiti di autenticazione nel back-end hello.
   - **Gruppo di connettori**: un'applicazione tooyour connettori processo hello accesso remoto e i gruppi di connettori consentono di organizzare i connettori e le App per area, rete o scopo. Se non si dispone di tutti i gruppi connettore ancora creati, l'app viene assegnato troppo**predefinito**.

   ![Configurare l'applicazione](./media/application-proxy-publish-azure-portal/configure-app.png)
5. Se necessario, configurare le impostazioni aggiuntive. Per la maggior parte delle applicazioni, è consigliabile mantenere queste impostazioni nei rispettivi stati predefiniti. 
   - **Timeout applicazione back-end**: impostare questo valore troppo**lungo** solo se l'applicazione è lento tooauthenticate e connettersi. 
   - **Convertire gli URL nelle intestazioni**: mantenere il valore come **Sì** , a meno che l'applicazione necessaria l'intestazione dell'host nella richiesta di autenticazione hello originale hello.
   - **Convertire gli URL nel corpo di applicazione**: mantenere il valore come **n** a meno che non si dispone di applicazioni di on-premise tooother collegamenti HTML hardcoded e non usare i domini personalizzati. Per altre informazioni, vedere [Reindirizzare i collegamenti hardcoded per le app pubblicate con il proxy di app di Azure AD](application-proxy-link-translation.md).
   
   ![Configurare l'applicazione](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. Selezionare **Aggiungi**.


## <a name="add-a-test-user"></a>Aggiungere un utente di test 

tootest che l'app è stato pubblicato correttamente, aggiungere un account utente di prova. Verificare che l'account disponga già di autorizzazioni tooaccess hello dell'applicazione all'interno di hello alla rete aziendale.

1. Nel pannello avvio rapido hello selezionare **assegnare un utente per il testing**.

  ![Assegna utente per il test](./media/application-proxy-publish-azure-portal/assign-user.png)

2. Gli utenti di hello e blade gruppi, selezionare **Aggiungi**.

  ![Aggiungere un utente o gruppo](./media/application-proxy-publish-azure-portal/add-user.png)

3. Nel Pannello di assegnazione di hello Aggiungi, selezionare **utenti e gruppi** scegliere account hello da tooadd. 
4. Selezionare **Assegna**.

## <a name="test-your-published-app"></a>Testare l'app pubblicata

Nel browser passare toohello URL esterno configurato hello durante la fase di pubblicazione. Dovrebbe essere schermata start hello ed essere in grado di toosign con account di prova hello impostati.

![Testare l'app pubblicata](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>Passaggi successivi
- [Scaricare i connettori](active-directory-application-proxy-enable.md) e [creare gruppi di connettori](active-directory-application-proxy-connectors-azure-portal.md) toopublish applicazioni su reti separate e percorsi.

- [Configurare l'accesso Single Sign-On](application-proxy-sso-azure-portal.md) per l'app appena pubblicata
