---
title: Uso di un gruppo per gestire l'accesso ad applicazioni SaaS| Documentazione Microsoft
description: Come usare i gruppi in Azure Active Directory Premium o Basic per assegnare l'accesso ad applicazioni SaaS integrate in Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a>Uso di un gruppo per gestire l'accesso ad applicazioni SaaS
Con Azure Active Directory (Azure AD) con licenza Azure AD Premium o Azure AD Basic, è possibile usare i gruppi per assegnare l'accesso a un'applicazione SaaS integrata in Azure AD. Ad esempio, se si desidera assegnare al reparto marketing l'accesso per l'uso di cinque applicazioni SaaS diverse, è possibile creare un gruppo contenente gli utenti del reparto marketing e quindi assegnare a tale gruppo le cinque applicazioni SaaS necessarie. In questo modo è possibile velocizzare le operazioni grazie alla gestione dei membri del reparto marketing in un'unica posizione. Gli utenti vengono quindi assegnati all'applicazione quando vengono aggiunti come membri del gruppo marketing. In modo analogo, le relative assegnazioni vengono rimosse dall'applicazione quando gli utenti vengono rimossi dal gruppo marketing.

> [!IMPORTANT]
> Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo. 

Questa funzionalità può essere usata con centinaia di applicazioni che è possibile aggiungere dalla raccolta di applicazioni Azure AD.

**Per assegnare a un gruppo l'accesso a un'applicazione SaaS**

1. Nel [portale di Azure classico](https://manage.windowsazure.com), selezionare trovare **Active Directory** nella barra di spostamento sulla sinistra.
2. Selezionare la scheda **Directory** e aprire la directory in cui si desidera assegnare a un gruppo l'accesso a un'applicazione Saas.
3. Selezionare la scheda **Applicazioni** . Selezionare un'applicazione aggiunta dalla raccolta di applicazioni e quindi fare clic sulla scheda **Utenti e gruppi**.
4. Nella scheda **Utenti e gruppi**, nel campo **Inizia con** immettere il nome del gruppo a cui si desidera assegnare l'accesso e selezionare il segno di spunta in alto a destra. È sufficiente digitare la prima parte del nome di un gruppo.
5. Selezionare il gruppo, quindi scegliere il pulsante **Assegna accesso** . Selezionare **Sì** quando viene visualizzato il messaggio di conferma. In questo momento, le appartenenze ai gruppi annidati non sono supportate per l'assegnazione alle applicazioni in base al gruppo.
6. È inoltre possibile visualizzare quali utenti sono assegnati all'applicazione direttamente o in base all'appartenenza a un gruppo. Per farlo, A tale scopo, impostare **Mostra elenco a discesa da "Gruppi"** su **"Tutti gli utenti"**. Nell'elenco sono visualizzati gli utenti nella directory ed è indicato se ogni utente è assegnato o meno all'applicazione. Nell'elenco è inoltre indicato se gli utenti sono assegnati direttamente all'applicazione (il tipo di assegnazione è indicato come 'Diretto') oppure in base all'appartenenza al gruppo (il tipo di assegnazione è indicato come 'Ereditato').

> [!NOTE]
> La scheda Utenti e gruppi è visibile solo dopo aver abilitato Azure AD Premium o Azure AD Basic.
>
>

### <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Informazioni su Azure Active Directory](active-directory-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
