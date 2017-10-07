---
title: 'Azure Active Directory B2C: reimpostazione password self-service | Documentazione Microsoft'
description: "Un argomento che illustra la modalità di reimpostazione tooset di password self-service per consentire agli utenti in Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Azure Active Directory B2C: configurare la reimpostazione password self-service per gli utenti
Con hello funzionalità di reimpostazione password self-service, il consumer (che hanno effettuato l'iscrizione per gli account locali) possono reimpostare la password in modo autonomo. Questo riduce notevolmente onere hello per il personale di supporto, soprattutto se l'applicazione dispone di milioni di clienti utilizzarlo a intervalli regolari. Attualmente, è supportato solo l’utilizzo di un indirizzo di posta elettronica verificato come metodo di ripristino. Metodi di ripristino aggiuntivi (numero di telefono verificato, domande di sicurezza e così via) verrà aggiunto in futuro hello.

> [!NOTE]
> Questo articolo riguarda tooself-service password reset usata nel contesto di hello di criteri di accesso. Se è necessario richiamare dall'app criteri di reimpostazione delle password completamente personalizzabili, vedere [questo articolo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).
> 
> 

Per impostazione predefinita, la directory non avrà la reimpostazione password self-service attivata. Utilizzare hello seguendo i passaggi tooturn su:

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) come hello amministratore della sottoscrizione. Si tratta di hello stesso lavoro o scuola account o hello stesso account Microsoft usato toocreate della directory.
2. Passare l'estensione Active Directory toohello sulla barra di spostamento hello sul lato sinistro di hello.
3. Trovare la directory in hello **Directory** scheda e farvi clic sopra.
4. Fare clic su hello **configura** scheda.
5. Scorrere verso il basso toohello **criteri di reimpostazione password utente** hello sezione e attiva/disattiva **utenti abilitati per la reimpostazione della password** opzione troppo**Sì**. Si noti che hello **indirizzo di posta elettronica alternativo** opzione è selezionata, rimane invariato.
   
    ![Reimpostazione della password self-service](./media/active-directory-b2c-reference-sspr/sspr.png)
6. Fare clic su **salvare** nella parte inferiore di hello della pagina hello. L'operazione è completata.

tootest, utilizzo funzionalità "Esegui" hello in un criterio di accesso con account locali come provider di identità. Hello LocalAccount Accedi pagina (in cui si immette un indirizzo di posta elettronica e password, o un nome utente e password), fare clic su **non è possibile accedere all'account?** esperienza di tooverify hello consumer.

> [!NOTE]
> Hello pagine di reimpostazione della password self-service possono essere personalizzate tramite hello [funzionalità di branding aziendale](../active-directory/active-directory-add-company-branding.md).
> 
> 

