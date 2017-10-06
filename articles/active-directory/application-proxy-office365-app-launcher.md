---
title: una home page personalizzata per le app pubblicate usando il Proxy di applicazione AD Azure aaaSet | Documenti Microsoft
description: Nozioni fondamentali di hello include informazioni sui connettori Proxy di applicazione di Azure AD
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
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Impostare una home page personalizzata per le app pubblicate tramite il proxy applicazione di Azure AD

Questo articolo illustra come tooconfigure App toodirect utenti tooa home page personalizzata. Quando si pubblica un'applicazione con Proxy dell'applicazione, si imposta un URL interno, ma che viene visualizzata agli utenti dovrebbe essere prima pagina di hello. Impostare una home page personalizzata in modo che gli utenti Vai a pagina destra toohello quando accedono alle App hello da hello Pannello di accesso di Azure Active Directory o l'utilità di avvio applicazione hello Office 365.

Quando gli utenti avviano l'applicazione hello, gli si indirizzati dall'URL di dominio radice toohello predefinito per l'app pubblicata hello. pagina di destinazione Hello viene in genere impostato come URL della home page hello. Utilizzare gli URL home page personalizzata di hello Azure AD PowerShell modulo toodefine quando si desidera tooland agli utenti di app in una pagina specifica all'interno di app hello. 

ad esempio:
- All'interno della rete azienda, gli utenti andare troppo*https://ExpenseApp/login/login.aspx* toosign in e accedere all'app.
- Poiché si dispone di altre risorse come le immagini che il Proxy di applicazione deve tooaccess hello primo livello della struttura di cartelle hello, si pubblica l'applicazione hello con *https://ExpenseApp* come hello URL interno.
- URL esterno predefinito è Hello *https://ExpenseApp-contoso.msappproxy.net*, che non accetta le credenziali di utenti toohello nella pagina.  
- Impostare *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* toogive URL pagina iniziale come hello agli utenti un'esperienza senza problemi. 

>[!NOTE]
>Quando si concedono l'accesso agli utenti le app toopublished, hello App vengono visualizzate in hello [Pannello di accesso AD Azure](active-directory-saas-access-panel-introduction.md) hello e [avvio app di Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Prima di iniziare

Prima di impostare l'URL della home page di hello, tenere hello presente i requisiti seguenti:

* Verificare che si specifica il percorso di hello è un percorso di sottodominio di hello URL radice del dominio.

  Se l'URL del dominio radice hello è, ad esempio, https://apps.contoso.com/app1/, URL della home page hello configurate deve iniziare con https://apps.contoso.com/app1/.

* Se si apporta una modifica toohello pubblicare app, modifica hello potrebbe reimpostare il valore di hello dell'URL della home page hello. Quando si aggiorna l'applicazione hello in hello future, si deve ricontrollare e, se necessario, aggiornare l'URL della home page hello.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Modifica hello home page di hello portale di Azure

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.
2. Passare troppo**Azure Active Directory** > **registrazioni di App** e selezionare l'applicazione hello elenco. 
3. Selezionare **proprietà** dalle impostazioni di hello.
4. Hello aggiornamento **URL della Home page** campo con il nuovo percorso. 

   ![Fornire nuovi URL della home page](./media/application-proxy-office365-app-launcher/homepage.png)

5. Selezionare **Salva**

## <a name="change-hello-home-page-with-powershell"></a>Modificare hello home page con PowerShell

### <a name="install-hello-azure-ad-powershell-module"></a>Installare il modulo di Azure AD PowerShell hello

Prima di definire un URL della home page personalizzata tramite PowerShell, è possibile installare il modulo di Azure AD PowerShell hello. È possibile scaricare i pacchetti hello da hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), che utilizza hello endpoint dell'API Graph. 

tooinstall hello del pacchetto, seguire questi passaggi:

1. Aprire una finestra di PowerShell di standard e quindi eseguire hello comando seguente:

    ```
     Install-Module -Name AzureAD
    ```
    Se si esegue il comando hello come un utente non amministratore, utilizzare hello `-scope currentuser` opzione.
2. Durante l'installazione di hello, selezionare **Y** tooinstall due pacchetti da Nuget.org. Sono necessari entrambi i pacchetti. 

### <a name="find-hello-objectid-of-hello-app"></a>Trovare hello ObjectID dell'applicazione hello

Ottenere hello ObjectID dell'applicazione hello e quindi eseguire la ricerca per l'applicazione hello relativa home page.

1. Aprire PowerShell e importare il modulo di hello Azure AD.

    ```
    Import-Module AzureAD
    ```

2. Accedi toohello modulo di Azure AD come amministratore tenant hello.

    ```
    Connect-AzureAD
    ```
3. Trovare l'applicazione hello in base all'URL della pagina iniziale. È possibile trovare hello URL nel portale di hello passando troppo**Azure Active Directory** > **applicazioni aziendali** > **tutte le applicazioni**. Questo esempio usa *sharepoint-iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. È necessario ottenere un risultato simile toohello uno qui. Copiare hello toouse ObjectID GUID nella sezione successiva hello.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>Aggiornare l'URL della home page hello

Hello stesso modulo di PowerShell utilizzati per il passaggio 1, l'esecuzione hello alla procedura seguente:

1. Verificare di avere hello correggere app e sostituire *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* con hello ObjectID copiata nel passaggio precedente hello.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Ora che è stato confermato app hello, sei pronto tooupdate hello home page come indicato di seguito.

2. Creare un toohold oggetto applicazione vuota modifiche hello che si desidera toomake. Questa variabile contiene i valori hello che si desidera tooupdate. Non viene creato nulla in questo passaggio.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. Impostare hello homepage URL toohello valore desiderato. il valore di Hello deve essere un percorso di sottodominio di app pubblicata hello. Ad esempio, se si modifica hello URL della home page da *https://sharepoint-iddemo.msappproxy.net/* troppo*https://sharepoint-iddemo.msappproxy.net/hybrid/*, gli utenti di app andare direttamente toohello personalizzato pagina iniziale.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Rendere hello aggiornamento utilizzando hello GUID (ObjectID) che è stato copiato in "passaggio 1: trovare hello ObjectID dell'applicazione hello."

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. tooconfirm che modifica hello è stata completata correttamente, riavviare l'applicazione hello.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Le modifiche apportate app toohello potrebbero reimpostata hello URL della home page. Se viene reimpostato l'URL della home page, ripetere il passaggio 2.

## <a name="next-steps"></a>Passaggi successivi

- [Abilitare accesso remoto tooSharePoint con Proxy dell'applicazione Azure AD](application-proxy-enable-remote-access-sharepoint.md)
- [Abilitare il Proxy di applicazione nel portale di Azure hello](active-directory-application-proxy-enable.md)
