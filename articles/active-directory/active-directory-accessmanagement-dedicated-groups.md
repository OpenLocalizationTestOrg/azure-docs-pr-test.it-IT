---
title: Gruppi dedicati in Azure Active Directory | Documentazione Microsoft
description: Panoramica del funzionamento dei gruppi dedicati in Azure Active Directory e della loro creazione.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Gruppi dedicati in Azure Active Directory
In Azure Active Directory (Azure AD), la funzionalità gruppi dedicati crea e popola automaticamente l'appartenenza per gruppi di Azure AD predefiniti. Non è possibile aggiungere o rimuovere membri nei gruppi dedicati tramite il portale di Azure classico, i cmdlet di Windows PowerShell oppure a livello di codice.

> [!NOTE]
> I gruppi dedicati richiedono che venga assegnata una licenza Azure AD Premium a:
>
> * l'amministratore che gestisce la regola in un gruppo
> * tutti gli utenti che vengono selezionati in base alla regola come membro del gruppo
>
>

**Per abilitare i gruppi dedicati**

1. Nel [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e aprire la directory dell'organizzazione.
2. Selezionare la scheda **Gruppi** e aprire il gruppo da modificare.
3. Selezionare la scheda **Configura** e impostare **Abilita gruppi dedicati** su **Sì**.

Dopo aver impostato l'opzione Abilita gruppi dedicati su **Sì**, è anche possibile consentire alla directory di creare automaticamente il gruppo dedicato Tutti gli utenti impostando l'opzione **Abilita il gruppo "Tutti gli utenti"** su **Sì**. È quindi possibile modificare il nome di questo gruppo dedicato digitando il nuovo nome nel campo **Nome visualizzato per il gruppo “Tutti gli utenti”** .

Il gruppo Tutti gli utenti può essere usato per assegnare le stesse autorizzazioni a tutti gli utenti in una directory. Ad esempio, è possibile consentire a tutti gli utenti di una directory di accedere a un'applicazione SaaS tramite l'assegnazione dell'accesso a tale applicazione al gruppo dedicato Tutti gli utenti.

Il gruppo Tutti gli utenti include tutti gli utenti della directory, compresi gli utenti guest e gli utenti esterni. Se è necessario un gruppo che esclude gli utenti esterni, è possibile creare un gruppo con una regola dinamica basata su attributi come la seguente:

                (user.userPrincipalName -notContains "#EXT#@")

Per un gruppo che esclude tutti gli utenti guest, usare una regola come la seguente:

                (user.userType -ne "Guest")

Per informazioni su come creare regole *avanzate* (ovvero regole che possono contenere più confronti) per l'appartenenza dinamica ai gruppi, vedere [Uso di attributi per la creazione di regole avanzate](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Informazioni su Azure Active Directory](active-directory-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
