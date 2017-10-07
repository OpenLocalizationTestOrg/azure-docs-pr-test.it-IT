---
title: l'autenticazione con Amazon Web Services aaaConfigure | Documenti Microsoft
description: Questo articolo viene descritto come toocreate e convalidare una credenziale AWS per i runbook in automazione di Azure, la gestione delle risorse AWS.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: autenticazione AWS, configurare AWS
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1e312df2422d9da3cd3331fe01aeaa3a43c8b9d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>Autenticare runbook con Amazon Web Services
I runbook di automazione di Azure consentono di automatizzare le attività comuni relative alle risorse in Amazon Web Services (AWS).  Esattamente come avviene per le risorse in Azure, con i runbook di Automazione è possibile automatizzare numerose attività in AWS.  A questo scopo, sono necessari due elementi:

* Una sottoscrizione di AWS e un set di credenziali.  Nello specifico, si tratta della chiave di accesso e della chiave privata di AWS.  Per ulteriori informazioni, consultare l'articolo hello [utilizzando le credenziali di AWS](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).
* Una sottoscrizione di Azure e un account di Automazione.  Per ulteriori informazioni sull'impostazione di un account di automazione di Azure, consultare l'articolo hello [configurare Azure Account runas](automation-sec-configure-azure-runas-account.md).  

tooauthenticate con AWS, è necessario specificare un set di AWS credenziali tooauthenticate i runbook in esecuzione da automazione di Azure. Se si dispone di un account di automazione creato e si desidera toouse che tooauthenticate con AWS, è possibile seguire i passaggi di hello nella seguente sezione hello.  Se si desidera toodedicated un account per le risorse AWS con i runbook, è necessario creare prima un nuovo [account di automazione](automation-offering-get-started.md) (ignorare hello opzione toocreate un'entità servizio) e quindi seguire i passaggi di hello riportati di seguito.

## <a name="configure-automation-account"></a>Configurare l'account di Automazione
Per toocommunicate di automazione di Azure con AWS, innanzitutto necessario tooretrieve le credenziali AWS e archiviarle come asset di automazione di Azure.  Eseguire i passaggi illustrati nel documento AWS hello hello [la gestione delle chiavi di accesso per l'Account di AWS](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate hello un tasto di scelta rapida e copia **ID chiave di accesso** e **chiave di accesso privata** (se lo si desidera scaricare toostore il file di chiave, in un luogo sicuro).

Dopo aver creato e copiato le chiavi di sicurezza AWS, è necessario un asset delle credenziali con un toosecurely di account di automazione di Azure toocreate archiviarli e farvi riferimento con i runbook.  Seguire i passaggi hello nella sezione hello **toocreate una nuova credenziale** in hello [credenziali asset in automazione di Azure](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) articolo e immettere le seguenti informazioni hello:

1. In hello **nome** immettere **AWScred** o un valore appropriato segue gli standard di denominazione.  
2. In hello **nome utente** nella casella del **ID di accesso** e **chiave di accesso privata** in hello **Password** e **conferma password** casella.   

## <a name="next-steps"></a>Passaggi successivi
* Articolo di soluzione hello Reivew [l'automatizzazione della distribuzione di una macchina virtuale in Amazon Web Services](automation-scenario-aws-deployment.md) toolearn come attività toocreate runbook tooautomate AWS.

