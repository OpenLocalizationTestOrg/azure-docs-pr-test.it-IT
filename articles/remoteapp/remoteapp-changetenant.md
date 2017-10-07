---
title: tenant di Azure Active Directory aaaChange hello in Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tenant di Azure Active Directory hello toochange associata con Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Modificare il tenant di Azure Active Directory hello in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp utilizza Azure Active Directory (Azure AD) tooallow utente l'accesso. tenant Hello solo Azure AD che è possibile utilizzare in Azure RemoteApp è hello associato hello sottoscrizione di Azure. È possibile visualizzare la sottoscrizione associata hello in hello **impostazioni** hello portale. Esaminare hello **Directory** colonna hello **sottoscrizioni** scheda.

> [!NOTE]
> Per questo toosucceed di modifica, rimuovere tutti gli utenti dal tenant Azure Active Directory esistente hello da tutte le raccolte RemoteApp di Azure. toodo, andare toohello portale di Azure, visita toohello **Azure RemoteApp** scheda e aprire ogni raccolta di Azure RemoteApp. Passare toohello **utenti** scheda e rimuovere utenti che appartengono tooyour tenant di Azure Active Directory corrente. Ripetere per tutte le raccolte di RemoteApp di Azure esistenti. Senza questo modo, non sarà in grado di toocreate o raccolte di patch.
> 
> 

Se si desidera toouse un tenant diverso, utilizzare l'associazione di hello toochange questi passaggi con la sottoscrizione:

1. Nel portale di hello, rimuovere qualsiasi toowhich agli utenti di Azure AD è stato concesso l'accesso tooAzure raccolte di RemoteApp. (Vedere la nota di hello sopra per la procedura su come toodo questo.)
2. Impostare un account Microsoft (in precedenza denominato Live ID) come amministratore del servizio hello. (Non conosce già se si è amministratore del servizio hello? È possibile scoprirlo facendo clic su **Impostazioni -> Amministratori**.) A questo punto, ecco come lo si modifica:
   
   1. Fare clic su utente hello nell'angolo superiore destro di hello e quindi fare clic su **Visualizza fattura**.
   2. Fare clic sulla sottoscrizione hello. Quindi, nella pagina nuovo hello, scorrere verso il basso e fare clic su **modificare i dettagli della sottoscrizione** in hello destra. (Ordinamento di hello centrale inferiore destra, che consente di trovarlo.)
   3. Digitare hello Microsoft account utente di hello che deve essere amministratore del servizio hello
3. A questo punto, disconnettersi da portale hello e quindi accedere con un account Microsoft specificato nel passaggio precedente hello hello.
4. Fare clic su **Nuovo -> Servizi app -> Active Directory -> Directory -> Creazione personalizzata**.
5. In **Directory**, scegliere **Utilizza directory esistente**. Stiamo toohave toosign è dal portale hello a questo punto, quindi scegliere **sono pronti toobe uscire ora**.
6. Eseguire nuovamente l'accesso in hello portale come amministratore globale della directory hello desiderato tooadd. (Se non si era già un amministratore globale, lo si sarà aver avuto accesso e poi essersi disconnessi.)
7. Verrà richiesto quando si accede se si desidera toouse al tenant di Active Directory esistente con la sottoscrizione. Fare clic su **Continua**, quindi su **Esci ora**.
8. Accedere nuovamente e tornare troppo**Impostazioni -> sottoscrizioni**. Selezionare la propria sottoscrizione, quindi fare clic su **Modifica directory**. Selezionare il tenant di hello Azure AD che si desidera toouse.

È ora possibile utilizzare hello Azure AD nuovi tenant toocontrol accesso toohello accesso utente di sottoscrizione e tooconfigure Azure in Azure RemoteApp.

