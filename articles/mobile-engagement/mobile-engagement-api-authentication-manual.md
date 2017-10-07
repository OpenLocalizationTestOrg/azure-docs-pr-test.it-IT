---
title: aaaAuthenticate con l'API REST di Engagement Mobile - installazione manuale
description: Viene descritto come toomanually impostare l'autenticazione per le API REST di Engagement Mobile
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Eseguire l'autenticazione con le API REST di Mobile Engagement - installazione manuale
Questa è troppo documentazione un'appendice[eseguire l'autenticazione con le API REST di Engagement Mobile](mobile-engagement-api-authentication.md). Assicurarsi di che leggere il primo contesto di hello tooget. Descrive un modo alternativo toodo hello iniziali di configurazione per configurare l'autenticazione per utilizzando le API REST di Engagement Mobile hello hello portale di Azure. 

> [!NOTE]
> istruzioni di Hello seguenti si basano su questo [Guida di Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) e personalizzato per ciò che è richiesto per l'autenticazione per le API di Mobile Engagement. Se si desidera toounderstand hello procedura in modo dettagliato, fare riferimento tooit. 
> 
> 

1. Account di accesso tooyour Account Azure tramite hello [portale classico](https://manage.windowsazure.com/).
2. Selezionare **Active Directory** hello nel riquadro di sinistra.
   
     ![selezionare Active Directory][1]
3. Scegliere hello **predefinita Active Directory** nel portale di Azure. 
   
     ![scegliere la directory][2]
   
   > [!IMPORTANT]
   > Questo approccio funziona solo quando si utilizza predefinito hello Active Directory del proprio account e non funzionerà se si esegue questo in Active Directory creati nell'account. 
   > 
   > 
4. applicazioni di hello tooview nella directory, fare clic su **applicazioni**.
   
     ![visualizzare le applicazioni][3]
5. Fare clic su **AGGIUNGI**. 
   
     ![aggiungere un'applicazione][4]
6. Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**
   
     ![nuova applicazione][5]
7. Nome dell'applicazione hello e tipo hello selezionare applicazione come **applicazione WEB, e/o API WEB** e fare clic sul pulsante Avanti hello.
   
     ![assegnare un nome all'applicazione][6]
8. È possibile fornire un URL fittizio come **URL ACCESSO** e **URI ID APP**. Non vengono usati per questo scenario e gli URL di hello stessi non vengono convalidati.  
   
     ![proprietà dell'applicazione][7]
9. Alla fine di hello di questo, si avrà un'app di Azure ad con nome hello che seguente hello fornite in precedenza. Questo è il nome **AD\_APP\_NAME** ed è necessario prenderne nota.  
   
     ![Nome dell'applicazione][8]
10. Fare clic sul nome dell'applicazione hello e fare clic su **configura**.
    
      ![configurare l'applicazione][9]
11. Prendere nota dell'ID CLIENT che verrà utilizzato come hello **CLIENT\_ID** per l'API chiamate. 
    
     ![configurare l'applicazione][10]
12. Scorrere verso il basso toohello **chiavi** sezione e aggiungere una chiave con preferibilmente la durata di 2 anni (scadenza) e fare clic su **salvare**. 
    
     ![configurare l'applicazione][11]
13. Copiare immediatamente valore hello mostrato per la chiave di hello poiché viene visualizzata solo ora e non verrà archiviato in modo non verranno mai più visualizzati. In caso di smarrimento sarà necessario toogenerate una nuova chiave. Si tratterà hello **CLIENT_SECRET** per l'API chiamate. 
    
     ![configurare l'applicazione][12]
    
    > [!IMPORTANT]
    > Questa chiave scadrà alla fine di hello della durata di hello specificato toorenew Assicurarsi pertanto di verificare al momento di hello in caso contrario l'autenticazione di API non funzionerà più. È possibile anche eliminare e ricreare la chiave se si ritiene che sia stata compromessa.
    > 
    > 
14. Fare clic su **Visualizza endpoint** pulsante che viene ora visualizzato hello **endpoint dell'App** la finestra di dialogo. 
    
    ![][13]
15. Nella finestra di dialogo endpoint dell'App hello copiare hello **ENDPOINT TOKEN OAUTH 2.0**. 
    
    ![][14]
16. Questo endpoint sarà nel seguente formato in cui hello GUID nell'URL hello è hello il **TENANT_ID** quindi prendere nota di esso: 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. Si procederà ora le autorizzazioni di hello tooconfigure per questa app. Per questo oggetto è tooopen backup hello [portale di Azure](https://portal.azure.com). 
18. Fare clic su **gruppi di risorse** e trovare hello **Mobile Engagement** gruppo di risorse.  
    
    ![][15]
19. Fare clic su hello **Mobile Engagement** risorse di gruppo e passare toohello **impostazioni** pannello qui. 
    
    ![][16]
20. Fare clic su **utenti** in hello pannello impostazioni e quindi fare clic su **Aggiungi** tooadd un utente. 
    
    ![][17]
21. Fare clic su **Selezionare un ruolo**
    
    ![][18]
22. Fare clic su **Proprietario**
    
    ![][19]
23. Ricerca per nome dell'applicazione hello **AD\_APP\_nome** nella casella di ricerca hello. Qui non verrà visualizzato per impostazione predefinita. Se si trova il, selezionarla e fare clic su **selezionare** nella parte inferiore di hello del pannello hello. 
    
    ![][20]
24. In hello **aggiungere accesso** pannello viene visualizzato come **1 utente, 0 gruppi**. Fare clic su **OK** su questa modifica hello tooconfirm di blade. 
    
    ![][21]

Configurazione di AAD hello necessario sono stati completati ed è hello toocall di tutti i set di API. 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



