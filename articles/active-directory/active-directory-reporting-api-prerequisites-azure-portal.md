---
title: aaaPrerequisites tooaccess hello Azure AD reporting API | Documenti Microsoft
description: Informazioni sulle API reporting di hello prerequisiti tooaccess hello Azure AD
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>Prerequisiti tooaccess hello Azure AD API di creazione di report

Hello [Azure AD reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornire i dati di toohello accesso a livello di codice tramite un set di API basata su REST. È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.

Hello reporting Usa API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) web toohello di tooauthorize accesso API. 

tooget accedere toohello segnalazione dei dati tramite l'API di hello, è necessario toohave uno dei seguenti ruoli assegnati hello:

- Ruolo con autorizzazioni di lettura per la sicurezza
- Amministrazione della protezione
- Amministratore globale


tooprepare toohello l'accesso API di report, è necessario:

1. Registrare un'applicazione 
2. Concedere le autorizzazioni 
3. Ottenere le impostazioni di configurazione 

Per domande, problemi o suggerimenti, [inviare un ticket di supporto](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Registrare un'applicazione Azure Active Directory

Anche se si accede hello API tramite uno script di segnalazione, è necessario tooregister un'app. Ciò consente un **ID applicazione**, che è necessario per una chiamata di autorizzazione e consente il token tooreceive di codice.

tooconfigure la directory tooaccess hello Azure AD reporting API, è necessario accedere toohello portale di Azure con un account amministratore di Azure che è anche un membro di hello **amministratore globale** ruolo della directory nel tenant di Azure AD .

> [!IMPORTANT]
> Le applicazioni in esecuzione con le credenziali con privilegi "admin" simile al seguente possono essere molto potente, pertanto essere protetto le credenziali ID/chiave privata che tookeep hello dell'applicazione.
> 


**tooregister un'applicazione Azure Active Directory:**

1. In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. In hello **Azure Active Directory** pannello, fare clic su **registrazioni di App**.

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. In hello **registrazioni di App** pannello, nella barra degli strumenti hello nella parte superiore di hello, fare clic su **nuova registrazione applicazione**.

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. In hello **crea** pannello eseguire hello alla procedura seguente:

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. In hello **nome** casella tipo `Reporting API application`.

    b. Per **Tipo di applicazione** selezionare **App Web/API**.

    c. In hello **Sign-on URL** casella tipo `https://localhost`.

    d. Fare clic su **Crea**. 


## <a name="grant-permissions"></a>Concedere le autorizzazioni 

obiettivo Hello di questo passaggio è l'applicazione di toogrant **lettura dati directory** autorizzazioni toohello **Windows Azure Active Directory** API.

![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant hello di toouse l'autorizzazione applicazione API:**

1. In hello **registrazioni di App** pannello, nell'elenco di App hello, fare clic su **applicazione API Reporting**.

2. In hello **applicazione API Reporting** pannello, nella barra degli strumenti hello nella parte superiore di hello, fare clic su **impostazioni**. 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. In hello **impostazioni** pannello, fare clic su **delle autorizzazioni necessarie**. 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. In hello **delle autorizzazioni necessarie** pannello in hello **API** elenco, fare clic su **Windows Azure Active Directory**. 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. In hello **Abilita accesso** pannello seleziona **lettura dati directory**. 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Nella barra degli strumenti hello in primo piano hello, fare clic su **salvare**.

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Ottenere le impostazioni di configurazione 
In questa sezione illustra come hello tooget seguendo le impostazioni dalla directory:

* Nome di dominio
* ID client
* Segreto client

Questi valori è necessario quando si configurano le chiamate API di creazione report toohello. 

### <a name="get-your-domain-name"></a>Ottenere il nome di dominio

**tooget il nome di dominio:**

1. In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. In hello **Azure Active Directory** pannello, fare clic su **i nomi di dominio**.

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Copiare il nome di dominio dall'elenco di hello dei domini.


### <a name="get-your-applications-client-id"></a>Ottenere l'ID client dell'applicazione

**tooget ID client dell'applicazione:**

1. In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. In hello **registrazioni di App** pannello, nell'elenco di App hello, fare clic su **applicazione API Reporting**.

3. In hello **applicazione API Reporting** server blade, hello **ID applicazione**, fare clic su **fare clic su toocopy**.

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Ottenere il segreto client dell'applicazione
tooget client dell'applicazione privata, è necessario toocreate una nuova chiave e salvare il relativo valore quando si salvano nuova chiave hello perché non è possibile tooretrieve questo valore in un secondo momento più.

**tooget segreto client dell'applicazione:**

1. In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. In hello **registrazioni di App** pannello, nell'elenco di App hello, fare clic su **applicazione API Reporting**.


3. In hello **applicazione API Reporting** pannello, nella barra degli strumenti hello nella parte superiore di hello, fare clic su **impostazioni**. 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. In hello **impostazioni** pannello in hello **APIR accesso** fare clic su **chiavi**. 

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. In hello **chiavi** pannello eseguire hello alla procedura seguente:

    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. In hello **descrizione** casella tipo `Reporting API`.

    b. Per **Scadenza** selezionare **In 2 years** (In 2 anni).

    c. Fare clic su **Salva**.

    d. Copia valore chiave hello.


## <a name="next-steps"></a>Passaggi successivi
* È ad esempio tooaccess hello dati da Azure AD hello sarebbe reporting API in modo a livello di codice? Estrarre [introduzione hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).
* Se si desidera toofind ulteriori informazioni sui report di Azure Active Directory, vedere hello [Azure Active Directory Reporting Guida](active-directory-reporting-guide.md).  

