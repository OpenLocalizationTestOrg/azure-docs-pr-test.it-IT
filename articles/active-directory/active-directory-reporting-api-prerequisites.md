---
title: aaaPrerequisites tooaccess hello Azure AD reporting API. | Microsoft Docs
description: Informazioni sulle API reporting di hello prerequisiti tooaccess hello Azure AD
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>Prerequisiti tooaccess hello Azure AD API di creazione di report
Hello [Azure AD reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornire i dati di toohello accesso a livello di codice tramite un set di API basata su REST. È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.

Hello reporting Usa API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) web toohello di tooauthorize accesso API. 

tooprepare toohello l'accesso API di report, è necessario:

1. Creare un'applicazione nel tenant di Azure AD 
2. GRANT hello applicazione delle autorizzazioni appropriate tooaccess hello dati di Azure AD
3. Raccogliere le impostazioni di configurazione dalla directory

Per domande, problemi o suggerimenti, contattare la [Guida per la creazione di report AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Creare un'applicazione Azure AD
tooconfigure la directory tooaccess hello Azure AD reporting API, è necessario accedere toohello portale di Azure classico con un account di amministratore di sottoscrizione di Azure che è anche un membro del ruolo della directory hello amministratore globale nel tenant di Azure AD.

> [!IMPORTANT]
> Le applicazioni in esecuzione con le credenziali con privilegi "admin" simile al seguente possono essere molto potente, pertanto essere protetto le credenziali ID/chiave privata che tookeep hello dell'applicazione.
> 
> 

1. In hello [portale di Azure classico](https://manage.windowsazure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Da hello **active directory** elenco, selezionare la directory.
3. Scegliere dal menu hello in primo piano hello **applicazioni**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Nella barra inferiore hello, fare clic su **Aggiungi**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/03.png) 
5. In hello **cosa si desidera toodo?** finestra di dialogo, fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**. 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/04.png) 
6. In hello **informazioni sull'applicazione** finestra di dialogo, eseguire hello alla procedura seguente: 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. In hello **nome** casella di testo, digitare un nome (ad esempio: applicazione di Reporting API).
   
    b. Selezionare **Applicazione Web e/o API Web**.
   
    c. Fare clic su **Avanti**.
7. In hello **proprietà App** finestra di dialogo, eseguire hello alla procedura seguente: 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. In hello **Sign-on URL** casella tipo `https://localhost`.
   
    b. In hello **URI ID App** casella tipo ```https://localhost/ReportingApiApp```.
   
    c. Fare clic su **Complete**.

## <a name="grant-your-application-permission-toouse-hello-api"></a>Concedere il hello toouse di autorizzazione applicazione API
1. In hello [portale di Azure classico](https://manage.windowsazure.com/)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Da hello **active directory** elenco, selezionare la directory.
3. Scegliere dal menu hello in primo piano hello **applicazioni**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png)
4. Nell'elenco delle applicazioni hello, selezionare l'applicazione appena creata.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. Scegliere dal menu hello in primo piano hello **configura**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. In hello **autorizzazioni tooother applicazioni** sezione hello **Azure Active Directory** risorse, fare clic su hello **autorizzazioni applicazione** elenco a discesa, quindi Selezionare **lettura dati directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/09.png)
7. Nella barra inferiore hello, fare clic su **salvare**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Raccogliere le impostazioni di configurazione dalla directory
In questa sezione illustra come hello tooget seguendo le impostazioni dalla directory:

* Nome di dominio
* ID client
* Segreto client

Questi valori è necessario quando si configurano le chiamate API di creazione report toohello. 

### <a name="get-your-domain-name"></a>Ottenere il nome di dominio
1. In hello [portale di Azure classico](https://manage.windowsazure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Da hello **active directory** elenco, selezionare la directory.
3. Scegliere dal menu hello in primo piano hello **domini**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/11.png) 
4. In hello **nome di dominio** colonna, copiare il nome di dominio.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Ottenere l'ID client dell'applicazione hello
1. In hello [portale di Azure classico](https://manage.windowsazure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Da hello **active directory** elenco, selezionare la directory.
3. Scegliere dal menu hello in primo piano hello **applicazioni**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Nell'elenco delle applicazioni hello, selezionare l'applicazione appena creata.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. Scegliere dal menu hello in primo piano hello **configura**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. Copiare l' **ID client**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Ottenere segreto client dell'applicazione hello
tooget client dell'applicazione privata, è necessario toocreate una nuova chiave e salvare il relativo valore quando si salvano nuova chiave hello perché non è possibile tooretrieve questo valore in un secondo momento più.

1. In hello [portale di Azure classico](https://manage.windowsazure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Da hello **active directory** elenco, selezionare la directory.
3. Scegliere dal menu hello in primo piano hello **applicazioni**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Nell'elenco delle applicazioni hello, selezionare l'applicazione appena creata.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/07.png)
5. Scegliere dal menu hello in primo piano hello **configura**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/08.png)
6. In hello **chiavi** seguire hello alla procedura seguente: 
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. Elenco di durata hello, selezionare una durata
   
    b. Nella barra inferiore hello, fare clic su **salvare**.
   
    ![Registrare l'applicazione](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Copia valore chiave hello.

## <a name="next-steps"></a>Passaggi successivi
* È ad esempio tooaccess hello dati da Azure AD hello sarebbe reporting API in modo a livello di codice? Estrarre [introduzione hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).
* Se si desidera toofind ulteriori informazioni sui report di Azure Active Directory, vedere hello [Azure Active Directory Reporting Guida](active-directory-reporting-guide.md).  

