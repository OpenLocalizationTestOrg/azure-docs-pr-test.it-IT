---
title: i domini aaaCustom Proxy dell'applicazione Azure AD | Documenti Microsoft
description: "Gestire i domini personalizzati in Azure AD applicazione Proxy in modo tale URL hello per app hello è hello uguali indipendentemente dal fatto in cui gli utenti diritti di accesso."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Utilizzo di domini personalizzati nel Proxy di applicazione AD Azure

Quando si pubblica un'applicazione tramite il Proxy di applicazione Azure Active Directory, si crea un URL esterno per il toowhen toogo utenti che lavorano in remoto. Questo URL Ottiene dominio predefinito hello *yourtenant.msappproxy.net*. Ad esempio, se è stato pubblicato un'app denominata spese per il tenant è denominato Contoso, quindi URL esterno hello sarebbe https://expenses-contoso.msappproxy.net. Se si desidera toouse il nome di dominio, configurare un dominio personalizzato per l'applicazione. 

È consigliabile configurare domini personalizzati per le applicazioni ogni volta che è possibile. Alcuni dei vantaggi di hello di domini personalizzati:

- Gli utenti possono usare l'applicazione toohello con hello stesso URL, se si lavora all'interno o all'esterno della rete.
- Se tutte le applicazioni hanno hello stesso URL interni ed esterni, i collegamenti in un'applicazione che puntano tooanother continuano toowork anche all'esterno delle rete aziendale hello. 
- Si controllano la personalizzazione e creare URL hello desiderato. 


## <a name="configure-a-custom-domain"></a>Configurare un dominio personalizzato

### <a name="prerequisites"></a>Prerequisiti

Prima di configurare un dominio personalizzato, assicurarsi di aver hello preparati requisiti seguenti: 
- Oggetto [tooAzure Active Directory di aggiunta dominio verificato](active-directory-domains-add-azure-portal.md).
- Un certificato personalizzato per il dominio di hello, sotto forma di hello di un file PFX. 
- Un'app locale [pubblicata tramite il proxy di applicazione](application-proxy-publish-azure-portal.md).

### <a name="configure-your-custom-domain"></a>Configurare il dominio personalizzato

Quando si dispone di questi tre requisiti pronti, seguire questi passaggi tooset il dominio personalizzato:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Passare troppo**Azure Active Directory** > **applicazioni aziendali** > **tutte le applicazioni** e scegliere l'applicazione hello desiderato toomanage.
3. Selezionare **Proxy dell'applicazione**. 
4. Nel campo URL esterno hello, utilizzare tooselect elenco a discesa di hello del dominio personalizzato. Se non viene visualizzato il dominio nell'elenco di hello, quindi non è stata verificata ancora. 
5. Selezionare **Salva**
5. Hello **certificato** risulta abilitata campo che è stata disabilitata. Selezionare questo campo. 

   ![Fare clic su un certificato tooupload](./media/active-directory-application-proxy-custom-domains/certificate.png)

   Se è già caricato un certificato per questo dominio, il campo certificato hello Visualizza informazioni sul certificato di hello. 

6. Caricare un certificato PFX hello e immettere la password di hello per certificato hello. 
7. Selezionare **salvare** toosave le modifiche. 
8. Aggiungere un [record DNS](../dns/dns-operations-recordsets-portal.md) che reindirizzamenti hello nuovo msappproxy.net dominio toohello URL esterno. 

>[!TIP] 
>È sufficiente un certificato di tooupload per ogni dominio personalizzato. Dopo aver caricato un certificato, è possibile scegliere dominio personalizzato hello quando si pubblica una nuova app e dispone di configurazione aggiuntive di toodo ad eccezione dei record DNS hello. 

## <a name="manage-certificates"></a>Gestire i certificati

### <a name="certificate-format"></a>Formato del certificato
Non vi è alcuna restrizione sui metodi di firma certificato hello. Sono supportati certificati ECC (Curve Cryptography), SAN (Subject Alternative Name) e altri tipi comuni di certificato. 

È possibile utilizzare un certificato con caratteri jolly come carattere jolly hello corrisponde hello desiderato di URL esterno. 

È anche possibile usare certificati autofirmati. Se si utilizza un'autorità di certificazione privata, hello CDP (punto di distribuzione punto revoca di certificato) per il certificato di hello debba essere pubblico.

### <a name="changing-hello-domain"></a>Modificare il dominio hello
Tutti i domini verificati vengono visualizzati nell'elenco a discesa URL esterno di hello per l'applicazione. toochange hello dominio solo aggiornamento tale campo per un'applicazione hello. Se non è il dominio hello desiderato nell'elenco di hello, [aggiungerlo come un dominio verificato](active-directory-domains-add-azure-portal.md). Se si seleziona un dominio che non dispone ancora di un certificato associato, seguire i certificati di hello tooadd passaggi da 5 a 7. Quindi, assicurarsi di aggiornare hello tooredirect di record DNS da hello nuovo URL esterno. 

### <a name="certificate-management"></a>Gestione dei certificati
È possibile utilizzare hello che stesso certificato per più applicazioni, a meno che le applicazioni di hello condividono un host esterno. 

Viene visualizzato un avviso quando un certificato scade, indicante che tooupload un altro certificato tramite il portale di hello. Se hello certificato revocato, gli utenti possono vedere un avviso di sicurezza quando si accede a un'applicazione hello. Non vengono eseguiti controlli delle revoche dei certificati.  certificato hello tooupdate per una determinata applicazione, passare toohello applicazione e seguire i passaggi da 5 a 7 per la configurazione di domini personalizzati in tooupload applicazioni pubblicate un nuovo certificato. Se il certificato precedente hello non utilizzato da altre applicazioni, viene eliminato automaticamente. 

Tutta la gestione dei certificati è attualmente attraverso pagine dell'applicazione singoli è sono necessari i certificati toomanage nel contesto di hello di applicazioni pertinente hello. 

## <a name="next-steps"></a>Passaggi successivi
* [Abilita single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour pubblicati App con autenticazione di Azure AD.
* [Abilitare l'accesso condizionale](active-directory-application-proxy-conditional-access.md) tooyour App pubblicate.
* [Aggiungere il tooAzure nome di dominio personalizzato AD](active-directory-domains-add-azure-portal.md)


