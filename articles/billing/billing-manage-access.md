---
title: aaaManage tooAzure di accesso tramite ruoli di fatturazione | Documenti Microsoft
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Gestire le informazioni di accesso toobilling per Azure tramite il controllo di accesso basato sui ruoli

È possibile concedere l'accesso per Azure toomembers informazioni fatturazione del team tramite l'assegnazione di uno di hello sottoscrizione tooyour di ruoli utente di seguenti: Account amministratore, amministratore del servizio, coamministratore, proprietario, collaboratore, lettore e lettore fatturazione. Hanno accesso toobilling informazioni in hello [portale di Azure](https://portal.azure.com/), e possono usare hello [fatturazione API](billing-usage-rate-card-overview.md) tooprogrammatically Visualizza fatture (una volta scelto-in) e informazioni di utilizzo. Per altre informazioni su chi può concedere ruoli e i compiti per ogni ruolo, vedere [Ruoli in Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Consentendo a utenti aggiuntivi tooaccess fatture

Hello amministratore dell'Account deve acconsentire esplicitamente all'invio tramite hello [portale di Azure](https://portal.azure.com/) Consenti tooinvoices accesso ad altri utenti e tramite l'API.

1. Come amministratore dell'Account di hello, selezionare la sottoscrizione da hello [pannello sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) nel portale di Azure.

1. Selezionare **fatture** e quindi **accedere tooinvoices**.

    ![Schermata illustrata toodelegate accesso tooinvoices](./media/billing-manage-access/AA-optin.png)

1. Attivare **su** accesso hello seguita da salvare le modifiche di hello, gli utenti tooallow nella fattura toodownload ruoli con ambito di sottoscrizione.

    ![Schermata mostra tooinvoice accesso toodelegate-off](./media/billing-manage-access/AA-optinAllow.png)

Acconsentito esplicitamente tradizionale di amministratore del servizio, coamministratore, proprietario, collaboratore, lettore e fatturazione lettore hello sottoscrizione toodownload PDF fatture hello portale di Azure. Tuttavia, più vecchi di dicembre 2016 sono disponibile toohello solo amministratore dell'Account per il momento.

Hello amministratore dell'Account è anche possibile configurare le fatture toohave inviate tramite posta elettronica. vedere, più toolearn [ottenere la fattura nel messaggio di posta elettronica](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Aggiunta del ruolo di lettore fatturazione toohello utenti

ruolo di lettore fatturazione Hello dispone di accesso in sola lettura toosubscription le informazioni di fatturazione nel portale di Azure e non tooservices di accesso, ad esempio le macchine virtuali e gli account di archiviazione. Assegnare hello fatturazione lettore ruolo toosomeone che deve accedere alle informazioni di fatturazione sottoscrizione toohello ma non hello possibilità toomanage Azure servizi. Questo ruolo è appropriato per gli utenti che in un'organizzazione eseguono solo la gestione finanziaria e dei costi per le sottoscrizioni di Azure.

1. Selezionare la sottoscrizione da hello [pannello sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) nel portale di Azure.

1. Selezionare **Controllo di accesso (IAM)** e quindi fare clic su **Aggiungi**.

    ![Schermata mostra IAM nel Pannello di sottoscrizione hello](./media/billing-manage-access/select-iam.PNG)

1. Scegliere **lettore fatturazione** in hello **selezionare un ruolo** pagina.

    ![Schermata mostra fatturazione lettore nella visualizzazione popup hello](./media/billing-manage-access/select-roles.PNG)

1. Tipo di messaggio di posta elettronica hello per utente hello tooinvite desiderato, quindi fare clic su **OK** invito hello toosend.

    ![Schermata che mostra tooenter tooinvite di posta elettronica a un utente](./media/billing-manage-access/add-user.PNG)

1. Seguire le istruzioni toolog di posta elettronica di invito hello in come un lettore di fatturazione.

    ![Schermata che mostra cosa hello fatturazione lettura possa vedere nel portale di Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> funzionalità di fatturazione lettore Hello è disponibile in anteprima e non supporta ancora le sottoscrizioni enterprise (EA) o il cloud non globali.

## <a name="adding-users-tooother-roles"></a>Aggiunta di utenti tooother ruoli

Gli utenti in altri ruoli, ad esempio proprietario o collaboratore, possono accedere non solo alle informazioni di fatturazione, ma anche ai servizi di Azure. toomanage questi ruoli, vedere [aggiungere o modificare ruoli di amministratore di Azure che gestiscono la sottoscrizione hello o servizi](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Chi può accedere hello [centro Account](https://account.windowsazure.com)?

Centro Account toohello può accedere solo hello amministratore dell'Account. Hello amministratore dell'Account è hello legittimo proprietario sottoscrizione hello. Per impostazione predefinita, hello persona iscritti a o acquistati hello sottoscrizione di Azure è hello amministratore dell'Account, a meno che non hello [la proprietà di sottoscrizione è stata trasferita](billing-subscription-transfer.md) toosomebody else. Hello amministratore dell'Account può creare sottoscrizioni, annullare sottoscrizioni, modificare l'indirizzo di fatturazione hello per una sottoscrizione e gestire i criteri di accesso per la sottoscrizione di hello.

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.

Se è ancora più domande, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.
