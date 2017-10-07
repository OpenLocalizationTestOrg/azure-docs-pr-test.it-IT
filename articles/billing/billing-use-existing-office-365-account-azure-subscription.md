---
title: aaaSign iscrizione a Azure con account di Office 365 | Documenti Microsoft
description: Informazioni su come toocreate una sottoscrizione di Azure utilizzando un account Office 365
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 129cdf7a-2165-483d-83e4-8f11f0fa7f8b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: cc331bf7222b5b03e740cb40a214bc13ef585f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-azure-subscription-with-your-office-365-account"></a>Iscriversi a una sottoscrizione di Azure con il proprio account di Office 365
Se si dispone di una sottoscrizione Office 365, è possibile utilizzare il toocreate account Office 365 una sottoscrizione di Azure. Accedi toohello [portale di Azure](https://portal.azure.com/) utilizzando il nome utente di Office 365 e la password. Se si desidera tooset backup di macchine virtuali o utilizzano altri servizi di Azure, è necessario iscriversi per una sottoscrizione di Azure. È possibile condividere la sottoscrizione di Azure con altri utenti e [tooyour di accesso di controllo di accesso basato sui ruoli toomanage sottoscrizione di Azure e altre risorse](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)

Se si dispone già di un account Office 365 sia una sottoscrizione di Azure, vedere [associare un tooan tenant di Office 365 sottoscrizione di Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-azure-subscription-using-your-office-365-account"></a>Ottenere una sottoscrizione di Azure tramite l'account di Office 365 personale

Se si accede ad Azure usando il nome utente e la password di Office 365, è possibile risparmiare tempo ed evitare la proliferazione di account. 

1. Acceder ad [Azure.com](https://account.azure.com/signup?offer=MS-AZR-0044p&appId=docs). 
2. Accedere usando il nome utente e la password di Office 365. Hello l'account utilizzato non è necessario toohave le autorizzazioni di amministratore. Se si dispone di più di un account Office 365, verificare che si utilizzano credenziali hello per account di Office 365 hello che si desidera tooassociate con la sottoscrizione di Azure. 

   ![Schermata che mostra hello nella pagina di accesso.](./media/billing-use-existing-office-365-account-azure-subscription/billing-sign-in-with-office-365-account.png)

3. Immettere le informazioni necessarie hello e processo di iscrizione hello completo. È possibile che alcune informazioni non siano necessarie se si dispone già di un account Office 365.

    ![Schermata che mostra modulo di iscrizione hello.](./media/billing-use-existing-office-365-account-azure-subscription/billing-azure-sign-up-fill-information.png)

- Se è necessario tooadd ad altre persone nel toohello organizzazione sottoscrizione di Azure, vedere [Introduzione alla gestione di accesso nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md). 

## <a id="more-about-subs">Altre informazioni su sottoscrizioni di Azure e abbonamenti a Office 365</a>
Office 365 e Azure è possibile utilizzare le sottoscrizioni e gli utenti di toomanage hello Azure AD del servizio. Hello directory Azure è simile a un contenitore in cui è possibile raggruppare gli utenti e le sottoscrizioni. toouse hello stessi account utente per le sottoscrizioni Azure e Office 365, è necessario che toomake tale hello Azure le sottoscrizioni vengono create in hello stessa directory sotto forma di sottoscrizioni hello Office 365. Tenere hello presente seguenti punti:

* Una sottoscrizione viene creata in una directory
* Toodirectories appartengono gli utenti
* Una sottoscrizione inserita nella directory hello di utente hello Crea sottoscrizione hello. Pertanto l'abbonamento a Office 365 è vincolata toohello stesso account come sottoscrizione Azure.
* Le sottoscrizioni di Azure appartengono a singoli utenti nella directory hello
* Le sottoscrizioni di Office 365 sono di proprietà da directory hello stesso. Gli utenti con autorizzazioni appropriate di hello all'interno di directory hello possono gestire queste sottoscrizioni.

![Schermata che mostra la relazione hello di hello directory, gli utenti e le sottoscrizioni.](./media/billing-use-existing-office-365-account-azure-subscription/19-background-information.png)

Per altre informazioni, vedere [Associare le sottoscrizioni di Azure ad Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema. 
