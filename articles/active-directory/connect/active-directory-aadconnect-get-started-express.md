---
title: 'Azure AD Connect: introduzione alle impostazioni rapide | Documentazione Microsoft'
description: Informazioni su come toodownload, installazione e l'esecuzione di hello installazione guidata di Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Introduzione alle impostazioni rapide per Azure AD Connect
La funzione **Impostazioni rapide** di Azure AD Connect viene usata quando è presente una topologia a singola foresta e si usa la [sincronizzazione password](active-directory-aadconnectsync-implement-password-synchronization.md) per l'autenticazione. **Impostazioni Express** è l'opzione predefinita hello e viene utilizzata per scenario hello distribuita più di frequente. Si sono solo pochi clic breve e stoccaggio tooextend cloud toohello directory locale.

Prima di iniziare l'installazione di Azure AD Connect, verificare che sia troppo[scaricare Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) e prerequisito hello completato i passaggi [Azure AD Connect: prerequisiti Hardware e](active-directory-aadconnect-prerequisites.md).

Se le impostazioni rapide non corrispondono alla topologia, vedere la [documentazione correlata](#related-documentation) per altri scenari.

## <a name="express-installation-of-azure-ad-connect"></a>Installazione rapida di Azure AD Connect
È possibile visualizzare i seguenti passaggi nell'azione di hello [video](#videos) sezione.

1. Accedere come si desidera tooinstall Azure AD Connect in un server di toohello amministratore locale. Eseguire questa operazione nel server di hello desiderato di server di sincronizzazione toobe hello.
2. Fare doppio clic su tooand passare **AzureADConnect.msi**.
3. Nella schermata iniziale hello selezionare hello casella accettano toohello alle condizioni di licenza e fare clic su **continua**.  
4. Nella schermata di impostazioni di hello Express, fare clic su **Usa impostazioni rapide**.  
   ![Benvenuti tooAzure Active Directory Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. Nella schermata di tooAzure AD Connect hello, immettere hello username e password di un amministratore globale per Azure AD. Fare clic su **Avanti**.  
   ![Connettersi AD tooAzure](./media/active-directory-aadconnect-get-started-express/connectaad.png) se si riceve un errore e problemi di connettività, vedere [dei problemi di connettività](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Nella schermata di dominio Active Directory tooAD Connetti hello, immettere hello username e password per un account di amministratore dell'organizzazione. È possibile immettere parte del dominio hello in formato FQDN o NetBios, vale a dire FABRIKAM\administrator o fabrikam.com\administrator. Fare clic su **Avanti**.  
   ![Connettersi tooAD di dominio Active Directory](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. Hello [ **configurazione di accesso AD Azure** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) pagina vengono visualizzati solo se non è stato completato [verificare i domini](../active-directory-add-domain.md) in hello [prerequisiti](active-directory-aadconnect-prerequisites.md).
   ![Domini non verificati](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Se viene visualizzata questa pagina, verificare ogni dominio contrassegnato come **Non aggiunto** e **Non verificato**. Assicurarsi che i domini usati siano stati verificati in Azure AD. Dopo avere verificato i domini, fare clic su simboli aggiornamento hello.
8. Nella schermata di hello tooconfigure pronti, fare clic su **installare**.
   * Nella pagina Pronto tooconfigure hello, facoltativamente, è possibile deselezionare hello **avviare il processo di sincronizzazione di hello non appena viene completato configurazione** casella di controllo. È necessario deselezionare questa casella di controllo se si desidera toodo di configurazione aggiuntive, ad esempio [filtro](active-directory-aadconnectsync-configure-filtering.md). Se si deseleziona questa opzione, la procedura guidata hello Configura sincronizzazione, ma lascia dell'utilità di pianificazione di hello disabilitato. Non può essere eseguito finché non si abilita manualmente da [rieseguire l'installazione guidata di hello](active-directory-aadconnectsync-installation-wizard.md).
   * Se si dispone di Exchange in Active Directory locale, quindi è anche un'opzione tooenable [ **distribuzione ibrida di Exchange**](https://technet.microsoft.com/library/jj200581.aspx). Abilitare questa opzione se si prevede di toohave cassette postali di Exchange sia nel cloud hello e on-premise nel hello stesso tempo.
     ![Pronto tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Al termine dell'installazione di hello, fare clic su **uscita**.
10. Una volta completata l'installazione di hello, disconnettersi e accedere di nuovo prima di usare Synchronization Service Manager o l'Editor delle regole di sincronizzazione.

## <a name="videos"></a>Video
Per un video sull'utilizzo per l'installazione rapida hello, vedere:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Dopo avere installato di Azure AD Connect è possibile [verificare l'installazione di hello e assegnare licenze](active-directory-aadconnect-whats-next.md).

Altre informazioni su queste funzionalità, che sono state abilitate con installazione hello: [l'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md), [impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), e [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Altre informazioni su questi argomenti comuni: [dell'utilità di pianificazione e la modalità di sincronizzazione tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

## <a name="related-documentation"></a>documentazione correlata
| Argomento |
| --- | --- |
| Panoramica di Azure AD Connect |
| Eseguire l'installazione con le impostazioni personalizzate |
| Aggiornamento da DirSync |
| Account usati per l'installazione |

