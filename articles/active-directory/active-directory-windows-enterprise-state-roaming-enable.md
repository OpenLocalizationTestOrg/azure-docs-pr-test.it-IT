---
title: aaaEnable Enterprise State Roaming in Azure Active Directory | Documenti Microsoft
description: Domande frequenti sulle impostazioni del servizio Enterprise State Roaming nei dispositivi Windows. Enterprise State Roaming offre agli utenti un'esperienza unificata tra i propri dispositivi Windows e riducendo i tempi di hello necessari per la configurazione di un nuovo dispositivo.
services: active-directory
keywords: stato aziendali comuni, come cloud di windows, tooenable enterprise stato roaming
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Abilitare Enterprise State Roaming in Azure Active Directory
Enterprise State Roaming è organizzazione tooany disponibile con una sottoscrizione di Azure Active Directory (Azure AD) Premium. Per ulteriori informazioni su come tooget una sottoscrizione di Azure AD, vedere hello [pagina prodotto Azure AD](https://azure.microsoft.com/services/active-directory).

Quando si abilita Enterprise State Roaming, l'organizzazione verrà concesso automaticamente le licenze per tooAzure una sottoscrizione gratuita, limitazioni d'uso Rights Management. Questa sottoscrizione gratuita è limitato tooencrypting e la decrittografia dei dati applicazione sincronizzati dal servizio Enterprise State Roaming; hello e le impostazioni di enterprise è necessario disporre di una sottoscrizione a pagamento toouse hello tutte le funzionalità di Azure Rights Management.

Dopo aver ottenuto una sottoscrizione di Azure AD Premium, seguire questi passaggi tooenable Enterprise State Roaming:

1. Account di accesso toohello portale di Azure classico.
2. A sinistra di hello, selezionare **ACTIVE DIRECTORY**, quindi selezionare hello directory per cui si desidera tooenable Enterprise State Roaming.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Passare toohello **configura** scheda nella parte superiore di hello.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Scorrere verso il basso la pagina hello e selezionare **gli utenti possono SINCRONIZZARE le impostazioni e dati delle APP aziendali**, quindi fare clic su **salvare**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Per impostazioni tooroam di dispositivo di Windows 10 con hello Enterprise State Roaming servizio, il dispositivo hello deve essere autenticate utilizzando un'identità di Azure AD. Per i dispositivi che vengono unite in join tooAzure Active Directory, account di accesso primario dell'utente hello è identità hello Azure AD, pertanto non è richiesta alcuna configurazione aggiuntiva. Per i dispositivi che usano un Active Directory locale tradizionale, hello amministratore IT deve [connessione hello tooAzure di dispositivi appartenenti a un dominio Active Directory per Windows 10 esperienze](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Archiviazione dei dati di sincronizzazione
Enterprise State Roaming dei dati sono ospitati in uno o più [aree di Azure](https://azure.microsoft.com/regions/) che meglio in linea con il valore di paese/area geografica hello impostato nell'istanza di Azure Active Directory hello. I dati del servizio Enterprise State Roaming vengono partizionati in base alle tre principali aree geografiche: America del Nord, EMEA e Asia Pacifico. Enterprise State Roaming dei dati per il tenant hello si trova in locale con area geografica hello e non viene replicati in aree geografiche.  Ad esempio, i clienti che hanno le tooone di set di valore paese/area geografica dei paesi EMEA come "Francia" o "Zambia" avranno i dati ospitati in uno o di hello aree di Azure in Europa.  I clienti che ha impostato il valore del paese/area geografica in Azure AD tooone paesi dell'America del Nord, come "United States" o "Canada" avranno i dati ospitati in uno o più hello Azure aree all'interno di hello Stati Uniti.  I clienti che ha impostato il valore del paese/area geografica in Azure AD tooone dei paesi Asia Pacifico, come "Australia" o "Nuova Zelanda" avranno i dati ospitati in uno o più hello aree di Azure in Asia.  Paesi dell'America del Sud e dati Antartide verranno ospitati in uno o più aree di Azure all'interno di hello Stati Uniti.  il valore di paese/area geografica Hello è impostato come parte del processo di creazione di directory di Azure AD hello e non può essere modificato successivamente. 

Se sono necessarie altre informazioni sulla posizione di archiviazione dei dati, inviare un ticket al [supporto tecnico Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Gestire il servizio Enterprise State Roaming
Gli amministratori globali di Azure AD è possono abilitare e disabilitare Enterprise State Roaming in hello portale di Azure classico.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Gli amministratori globali possono limitare gruppi di sicurezza toospecific Impostazioni sincronizzazione.

Gli amministratori globali possono inoltre visualizzare un report di stato sincronizzazione dispositivi per utente selezionando un utente specifico nell'istanza di Active Directory hello **utenti** elenco e fare clic sul **dispositivi** scheda e selezionando visualizzazione **Sincronizzazione dispositivi impostazioni e dati delle app aziendali**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Conservazione dei dati
A meno che non viene eseguita un'operazione di eliminazione manuale o dati hello in questione sono determinato toobe obsoleti tooAzure dati sincronizzati tramite Enterprise State Roaming verrà mantenute per un periodo illimitato. 

**Eliminazione esplicita:** quando un amministratore di Azure Elimina un utente o una directory o un amministratore richiede in modo esplicito che i dati siano eliminati toobe hello dati vengono eliminati.

* **Eliminazione utente**: durante l'eliminazione di un utente in Azure AD account utente di hello roaming dati verranno contrassegnati per l'eliminazione e verranno eliminati tra 90 giorni too180. 
* **Eliminazione della directory**: l'eliminazione di un'intera directory in Azure AD è un'operazione immediata. Tutti i dati delle impostazioni di hello associate che verrà contrassegnata per l'eliminazione di directory e verrà eliminata tra 90 giorni too180. 
* **Nell'eliminazione di richiesta**: se hello Azure AD amministratore desidera toomanually Elimina i dati o dati delle impostazioni di un utente specifico, salve può inviare un ticket di [supporto tecnico di Azure](https://azure.microsoft.com/support/). 

**L'eliminazione dei dati obsoleti**: dati non è stato effettuato l'accesso per un anno ("hello periodo di memorizzazione") verrà considerato come non aggiornata e può essere eliminato da Azure. periodo di memorizzazione Hello è soggetto toochange ma non sarà minore di 90 giorni. dati non aggiornati Hello potrebbero essere un set di impostazioni di Windows o applicazioni o tutte le impostazioni per un utente specifico. ad esempio:

* Se nessuna periferica di accedere a una raccolta di specifiche impostazioni (ad esempio, un'applicazione viene rimosso dal dispositivo hello o un gruppo di impostazioni, ad esempio "Tema" è disabilitato per tutti i dispositivi dell'utente), quindi tale raccolta risulterà non aggiornata dopo il periodo di memorizzazione hello e può essere eliminato. 
* Se un utente ha disattivato la sincronizzazione delle impostazioni in tutti i suoi dispositivi, quindi nessuno dei dati delle impostazioni di hello si accederà e tutti i dati delle impostazioni hello per tale utente verranno risultino non aggiornati e potrebbero essere eliminati dopo il periodo di mantenimento hello. 
* Se directory Azure AD salve Disattiva Enterprise State Roaming per hello tutta la directory, quindi tutti gli utenti directory arresterà la sincronizzazione delle impostazioni e tutti i dati delle impostazioni per tutti gli utenti diventeranno non aggiornati e potrebbero essere eliminati dopo il periodo di mantenimento hello. 

**Eliminare il ripristino dei dati**: criteri di conservazione dati hello non sono configurabili. Una volta eliminati in modo permanente dati hello, non sarà recuperabile. Tuttavia, è importante toonote che i dati delle impostazioni di hello verrà eliminato solo da Azure, non i dispositivi degli utenti finali hello. Se tutti i dispositivi si riconnette in un secondo momento il servizio di Enterprise State Roaming toohello, le impostazioni di hello nuovamente essere sincronizzate e archiviate in Azure.

## <a name="related-topics"></a>Argomenti correlati
* [Panoramica di Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Domande frequenti su impostazioni e dati in roaming](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Criteri di gruppo e impostazioni del software MDM per la sincronizzazione delle impostazioni](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Riferimento alle impostazioni di roaming di Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Risoluzione dei problemi](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
