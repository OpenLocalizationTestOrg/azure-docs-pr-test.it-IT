---
title: i ruoli di aaaAdd o modifica sottoscrizione di amministrazione di Azure | Documenti Microsoft
description: Viene descritto come tooadd o modificare Azure CO-amministratore, amministratore del servizio e l'amministratore dell'Account
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>Aggiungere o modificare i ruoli di amministratore di Azure che gestiscono la sottoscrizione hello o servizi
È possibile modificare hello Azure amministratore che gestisce la sottoscrizione di Azure o gestisce hello Azure servizi utilizzati nella sottoscrizione. le informazioni di fatturazione Azure tooview e gestire le sottoscrizioni, è necessario accedere toohello [centro Account](https://account.windowsazure.com/Home/Index) come hello amministratore dell'Account. 

## <a name="add-an-admin-for-a-subscription"></a>Aggiungere un amministratore per una sottoscrizione
È possibile aggiungere un amministratore di Azure nel portale di Azure hello o nel portale di Azure classico hello.

**Portale di Azure**

tooadd un utente come amministratore per una sottoscrizione nel portale di Azure hello, garantirvi il ruolo di proprietario hello. ruolo di proprietario Hello è possibile gestire solo alle risorse di hello nella sottoscrizione hello assegnato. Non dispone di accesso con privilegi tooother sottoscrizioni. Hello proprietari aggiunti tramite hello [portale di Azure](https://portal.azure.com) non è possibile gestire risorse in hello [portale di Azure classico](https://manage.windowsazure.com).

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, selezionare **sottoscrizione** > *hello sottoscrizione che si desidera hello admin tooaccess*.

    ![Schermata che mostra una sottoscrizione selezionata](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. Nel Pannello di sottoscrizione hello, selezionare **Access control (IAM)**.
4. Selezionare **Aggiungi** > **Ruolo** > **Proprietario**. Digitare l'indirizzo di posta elettronica hello di hello utente che si vuole tooadd come proprietario, hello selezionare utente, quindi selezionare **salvare**.

    ![Schermata che illustra il ruolo di proprietario hello selezionato](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Se si vuole che tooadd hello proprietario account come coamministratore, in hello **Access control (IAM)** pagina, fare doppio clic su utente hello e quindi selezionare **Aggiungi come coamministratore**. Questa funzionalità è ora disponibile nel [portale di anteprima di Azure](https://preview.portal.azure.com/). 

     ![Schermata per l'aggiunta di un coamministratore](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Sarà necessario utente di "Proprietario" hello tooadd come co-amministratore se l'utente di hello deve toomanage hello servizi di Azure in [portale di Azure classico](https://manage.windowsazure.com/).

    tooremove hello CO-amministratore le autorizzazioni, fare doppio clic su utente "coamministratore" hello, quindi selezionare **rimuovere coamministratore**.

    ![Schermata per la rimozione di un coamministratore](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**portale di Azure classico**

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/).
2. Nel riquadro di spostamento hello, selezionare **impostazioni**> **amministratori**> **Aggiungi**. </br>

    ![Schermata che illustra come tooget toohello pulsante Aggiungi](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Hello tipo indirizzo di posta elettronica della persona hello tooadd come coamministratore, quindi selezionare sottoscrizione hello che si desidera tooaccess CO-amministratore hello.</br>

    ![Schermata che mostra una sottoscrizione selezionata ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Hello segue l'indirizzo di posta elettronica può essere aggiunto come co-amministratore:

* **Account Microsoft**, denominato in precedenza Windows Live ID </br>
  È possibile utilizzare un Account Microsoft di toosign tooall orientata ai servizi consumer dei prodotti Microsoft e servizi cloud, ad esempio Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone e Xbox LIVE.
* **Organizational account**</br>
  Un account dell'organizzazione è un account che viene creato in Azure Active Directory. indirizzo dell'account aziendale Hello il formato è:

    utente@&lt;dominio&gt;.onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Modificare l'amministratore del servizio per una sottoscrizione
Solo amministratore dell'Account di hello modificabili hello amministratore del servizio per una sottoscrizione.

1. Accedi troppo[centro Account Azure](https://account.windowsazure.com/subscriptions) utilizzando hello amministratore dell'Account.
2. Selezionare la sottoscrizione di hello da toochange.
3. Sul lato destro di hello, selezionare **Modifica sottoscrizione** dettagli. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. In hello **amministratore del servizio** , immettere l'indirizzo di posta elettronica hello di hello nuovo amministratore del servizio. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>Modificare l'Account amministratore hello
la proprietà tootransfer di hello account tooanother account Azure, vedere [il trasferimento di proprietà di una sottoscrizione Azure](billing-subscription-transfer.md).

Si consiglia di non eliminare o rinominare l'indirizzo di posta elettronica dell'amministratore dell'Account di hello. È possibile visualizzare il comportamento di imprevisto e indesiderato con hello account Azure. Si potrebbe non essere in grado di tooAzure Accedi con tale account apportare modifiche toohello account o gestire le risorse con tale account. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Controllo hello amministratore dell'Account di sottoscrizione hello
Se non si è certi che l'amministratore dell'account hello è per la sottoscrizione, utilizzare hello seguendo i passaggi toofind out.

  1. Accedi toohello [portale di Azure](https://portal.azure.com).
  2. Nel menu Hub hello, selezionare **sottoscrizione**.
  3. Selezionare la sottoscrizione di hello toocheck desiderato e quindi cercare in **impostazioni**.
  4. Selezionare **Proprietà**. amministratore dell'account di sottoscrizione hello Hello viene visualizzato in hello **amministratore dell'Account** casella.  

## <a name="types-of-azure-admin-accounts"></a>Tipi di account amministratore di Azure
 Account amministratore, amministratore del servizio e coamministratore sono tre tipi di hello di ruoli di amministratore in Microsoft Azure. Hello nella tabella seguente descrive hello differenza tra questi tre ruoli amministrativi.

| Ruolo amministrativo | Limite | Descrizione |
| --- | --- | --- |
| Amministratore dell'account |1 per ogni account di Azure |Si tratta di hello persona iscritti a o ha acquistato le sottoscrizioni di Azure e autorizzati tooaccess hello [centro Account](https://account.windowsazure.com/Home/Index) ed eseguire varie attività di gestione. Queste includono la sottoscrizioni toocreate in grado di annullare sottoscrizioni, modificare la fatturazione hello per una sottoscrizione e modificare hello amministratore del servizio. |
| Amministratore del servizio |1 per ogni sottoscrizione di Azure |Questo ruolo è servizi autorizzati toomanage hello [portale di Azure](https://portal.azure.com). Per impostazione predefinita, per una nuova sottoscrizione, hello amministratore dell'Account è anche hello amministratore del servizio. |
| CO-amministratore (CA) in hello [portale di Azure classico](https://manage.windowsazure.com) |200 per ogni sottoscrizione |Questo ruolo hello dispone di privilegi di accesso come amministratore del servizio hello, ma non è possibile modificare l'associazione di hello delle directory tooAzure sottoscrizioni. |

Azure Active Directory Role-based Access controllo (RBAC) consente agli utenti toobe aggiunto toomultiple ruoli. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo di Azure Active Directory](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Limitazioni e restrizioni per gli account amministratore
* Ogni sottoscrizione è associata a una directory di Azure AD (noto anche come Directory predefinita Buongiorno). hello toofind sottoscrizione hello Directory predefinita è associato, andare toohello [portale di Azure classico](https://manage.windowsazure.com/)selezionare **impostazioni** > **sottoscrizioni**. Controllare hello toofind di ID sottoscrizione hello Directory predefinita.
* Se si accede con un Account Microsoft, è possibile aggiungere solo altri Accounts Microsoft o gli utenti all'interno di hello Directory predefinita come coamministratore.
* Se l'accesso è stato eseguito con un account dell'organizzazione, è possibile aggiungere come coamministratori altri account dell'organizzazione. Ad esempio, abby@contoso.com può aggiungere bob@contoso.com come amministratore del servizio o coamministratore, ma non può aggiungere john@notcontoso.com a meno che john@notcontoso.com non si trovi nella directory predefinita. Gli utenti l'accesso con account aziendali possono continuare tooadd utenti con Account Microsoft come amministratore del servizio o coamministratore.
* Ora che è possibile toosign in tooAzure con un account aziendale, ecco hello modifiche tooService amministratore e i requisiti dell'account CO-amministratore:

  | Metodo di accesso | Aggiungere un account Microsoft o utenti in una directory predefinita come coamministratori o amministratori del servizio? | Aggiungere l'account aziendale in hello stessa organizzazione come SA o CA? | Aggiungere un account aziendale in un'organizzazione diversa come coamministratore o amministratore del servizio? |
  | --- | --- | --- | --- |
  |  Account Microsoft |Sì |No |No |
  |  Account dell'organizzazione |Sì |Sì |No |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Altre informazioni sul controllo dell'accesso alle risorse e Active Directory
* toolearn ulteriori informazioni sulla modalità di controllo di accesso alle risorse in Microsoft Azure, vedere [informazioni di accesso alle risorse in Azure](../active-directory/active-directory-understanding-resource-access.md).
* Per altre informazioni sul modo in cui Azure Active Directory, vedere [Associare le sottoscrizioni di Azure ad Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) e [Assegnazione dei ruoli di amministratore in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.
