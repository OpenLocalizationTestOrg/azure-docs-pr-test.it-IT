---
title: 'Autenticazione da servizio a servizio: Data Lake Store con Azure Active Directory | Documentazione Microsoft'
description: Informazioni su come l'autenticazione di service to service tooachieve con archivio Data Lake tramite Azure Active Directory
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Autenticazione da servizio a servizio con Data Lake Store tramite Azure Active Directory
> [!div class="op_single_selector"]
> * [Autenticazione da servizio a servizio](data-lake-store-authenticate-using-active-directory.md)
> * [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store usa Azure Active Directory per l'autenticazione. Prima di creazione di un'applicazione che funziona con archivio Azure Data Lake o Azure Data Lake Analitica, è necessario innanzitutto decidere come tooauthenticate l'applicazione con Azure Active Directory (Azure AD). Hello due opzioni disponibili sono:

* Autenticazione dell'utente finale 
* Autenticazione da servizio a servizio (questo articolo) 

Entrambe queste opzioni comportare l'applicazione viene fornita con un token OAuth 2.0, che ottiene tooeach collegato richiesta effettuata tooAzure archivio Data Lake o Azure Data Lake Analitica.

Questo articolo illustra come creare un'**applicazione Web di Azure AD per l'autenticazione da servizio a servizio**. Per istruzioni sulla configurazione dell'applicazione Azure AD per l'autenticazione dell'utente finale, vedere [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) (Autenticazione dell'utente finale con Data Lake Store tramite Azure Active Directory).

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Passaggio 1: Creare un'applicazione Web di Active Directory

Creare e configurare un'applicazione Web di Azure AD per l'autenticazione da servizio a servizio con Azure Data Lake Store tramite Azure Active Directory. Per istruzioni, vedere [Creare un'applicazione Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Seguendo le istruzioni di hello in hello di sopra di collegamento, assicurarsi di selezionare **App Web / API** per il tipo di applicazione, come illustrato nella schermata di hello riportata di seguito.

![Creare un'app Web](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Creare un'app Web")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Passaggio 2: ottenere l'ID applicazione, la chiave di autenticazione e l'ID del tenant
Durante l'accesso a livello di codice, è necessario l'id hello per l'applicazione. Se un'applicazione hello viene eseguito con le proprie credenziali, è necessario anche una chiave di autenticazione.

* Per istruzioni su come ID dell'applicazione hello tooretrieve e l'autenticazione della chiave (anche segreto client hello chiamata) per l'applicazione, vedere [chiave di autenticazione e l'ID applicazione Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Per istruzioni su come tooretrieve hello ID tenant, vedere [ottenere l'ID tenant](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Passaggio 3: Assegnare file dell'account archivio Azure Data Lake hello Azure AD applicazione toohello o cartella (solo per l'autenticazione di service to service)
1. Accedere di nuovo toohello [portale di Azure](https://portal.azure.com) e aprire account archivio Azure Data Lake hello che si desidera tooassociate con hello applicazione Azure Active Directory creato in precedenza.
2. Nel pannello dell'account di Archivio Data Lake, fare clic su **Esplora dati**.
   
    ![Creare directory nell'account Data Lake Store](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Creare directory nell'account Data Lake Store")
3. In hello **Esplora dati** pannello, fare clic su hello file o una cartella per cui desidera tooprovide accesso toohello Azure AD applicazione e quindi fare clic su **accesso**. file di tooa tooconfigure access, è necessario fare clic su **accesso** da hello **anteprima File** blade.
   
    ![Configurare elenchi di controllo di accesso nel file system di Data Lake](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Configurare elenchi di controllo di accesso nel file system di Data Lake")
4. Hello **accesso** pannello elenca accesso standard di hello e toohello radice già assegnato l'accesso personalizzato. Fare clic su hello **Aggiungi** personalizzata a livello di icona tooadd ACL.
   
    ![Elencare gli accessi standard e personalizzati](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "Elencare gli accessi standard e personalizzati")
5. Fare clic su hello **Aggiungi** hello tooopen icona **aggiungere accesso personalizzato** blade. In questo pannello, fare clic su **Seleziona utente o gruppo**, quindi nel **Seleziona utente o gruppo** pannello, cercare l'applicazione di hello Azure Active Directory creato in precedenza. Se si dispone di molti gruppi toosearch da, è possibile utilizzare la casella di testo hello nella hello toofilter superiore sul nome di gruppo hello. Fare clic su gruppo hello tooadd desiderato e quindi fare clic su **selezionare**.
   
    ![Aggiungere un gruppo](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Aggiungere un gruppo")
6. Fare clic su **selezionare autorizzazioni**, selezionare le autorizzazioni di hello e se si desidera che le autorizzazioni di hello tooassign come un ACL predefinito, accedere ACL o entrambi. Fare clic su **OK**.
   
    ![Assegnare autorizzazioni toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "assegnare autorizzazioni toogroup")
   
    Per altre informazioni sulle autorizzazioni in Data Lake Store e gli ACL predefiniti/di accesso, vedere [Controllo di accesso in Data Lake Store](data-lake-store-access-control.md).
7. In hello **aggiungere accesso personalizzato** pannello, fare clic su **OK**. Hello appena aggiunti, gruppo, con le autorizzazioni di hello associata, verrà ora elencato nella hello **accesso** blade.
   
    ![Assegnare autorizzazioni toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "assegnare autorizzazioni toogroup")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>Passaggio 4: Ottenere l'endpoint token OAuth 2.0 di hello (solo per le applicazioni basate sul linguaggio)

1. Accedere di nuovo toohello [portale di Azure](https://portal.azure.com) e fare clic su Active Directory hello nel riquadro di sinistra.

2. Nel riquadro di sinistra hello, fare clic su **registrazioni di App**.

3. Dall'alto hello del Pannello di registrazioni hello App, fare clic su **endpoint**.

    ![Endpoint di token OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "Endpoint di token OAuth")

4. Elenco di endpoint hello copiare endpoint token OAuth 2.0 hello.

    ![Endpoint di token OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "Endpoint di token OAuth")   

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è creata un'applicazione web di Azure AD e raccolte informazioni hello è necessario nelle applicazioni client che si creano utilizzando il SDK di .NET SDK per Java, e così via. È ora possibile procedere toohello seguenti articoli in cui descrivere come toofirst di applicazione web di toouse hello Azure AD eseguire l'autenticazione con l'archivio Data Lake ed eseguono altre operazioni sull'archivio hello.

* [Introduzione a Azure Data Lake Store utilizzando .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Introduzione ad Azure Data Lake Store con Java SDK](data-lake-store-get-started-java-sdk.md)

In questo articolo esaminati tooget necessari passaggi di base di hello un utente principale di e in esecuzione per l'applicazione. È possibile esaminare hello seguenti articoli tooget ulteriori informazioni:
* [Entità servizio toocreate di PowerShell](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Usare l'autenticazione del certificato per l'autenticazione basata su entità servizio](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [TooAzure di tooauthenticate AD altri metodi](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


