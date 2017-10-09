---
title: 'Sincronizzazione di Azure AD Connect: modifica della configurazione predefinita di hello | Documenti Microsoft'
description: Fornisce le procedure consigliate per la modifica di configurazione predefinita di hello di sincronizzazione di Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Sincronizzazione di Azure AD Connect: procedure consigliate per la modifica della configurazione predefinita di hello
scopo di Hello di questo argomento è toodescribe supportati e non supportati di sincronizzazione di modifiche tooAzure AD Connect.

configurazione di Hello creata da Azure AD Connect funziona "così com'è" per la maggior parte degli ambienti che la sincronizzazione di Active Directory locale con Azure AD. Tuttavia, in alcuni casi, è necessario tooapply alcuni toosatisfy di configurazione tooa modifiche un particolare necessario o requisito.

## <a name="changes-toohello-service-account"></a>Account del servizio toohello modifiche
Sincronizzazione di Azure AD Connect è in esecuzione con un account di servizio creato dalla procedura guidata di installazione di hello. Questo account del servizio contiene database di hello crittografia chiavi toohello utilizzato dalla sincronizzazione. Viene creato con una password lunga di 127 caratteri e la password di hello è impostata toonot scadenza.

* È **non supportato** toochange o la reimpostazione della password di hello hello dell'account di servizio. Questa operazione comporta l'eliminazione di chiavi di crittografia hello e hello servizio non è in grado di tooaccess hello database e non è in grado di toostart.

## <a name="changes-toohello-scheduler"></a>Utilità di pianificazione toohello modifiche
A partire da versioni di hello dalla compilazione 1.1 (febbraio 2016) è possibile configurare hello [dell'utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md) toohave ciclo di sincronizzazione diversa rispetto al valore predefinito di hello 30 minuti.

## <a name="changes-toosynchronization-rules"></a>Le modifiche tooSynchronization regole
installazione guidata di Hello fornisce una configurazione che si suppone toowork per scenari più comuni di hello. Nel caso in cui necessaria la configurazione di toohello toomake le modifiche, è necessario seguire queste regole toostill configurazione è supportata.

* È possibile [modificare i flussi di attributi](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) se i flussi di attributi diretto di hello predefinito non sono adatti per l'organizzazione.
* Se si desidera troppo[flusso non di un attributo](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) e rimuovere i valori di qualsiasi attributo esistente in Azure AD, è necessario toocreate una regola per questo scenario.
* [Disabilitare una regola di sincronizzazione indesiderata](#disable-an-unwanted-sync-rule) invece di eliminarla. Una regola eliminata viene ricreata durante un aggiornamento.
* troppo[modificare una regola di out-of-box](#change-an-out-of-box-rule), è necessario effettuare una copia di hello originale delle regole e disabilitare la regola di hello out-of-box. Editor regole di sincronizzazione Hello richiesto e consente di.
* Esportare le regole di sincronizzazione utilizzando hello Editor regole di sincronizzazione. editor Hello fornisce con uno script di PowerShell, è possibile utilizzare tooeasily ricrearli in uno scenario di ripristino di emergenza.

> [!WARNING]
> le regole di sincronizzazione out-of-box Hello hanno un'identificazione personale. Se si apportano una modifica di regole toothese, identificazione personale hello non corrispondenti. Potrebbero essersi verificati problemi in futuro hello quando si tenta di tooapply una nuova versione di Azure AD Connect. Solo lasciare modifiche hello che è descritto in questo articolo.

### <a name="disable-an-unwanted-sync-rule"></a>Disabilitare una regola di sincronizzazione indesiderata
Non eliminare una regola di sincronizzazione predefinita. Verrà ricreata durante l'aggiornamento successivo.

In alcuni casi, installazione guidata di hello ha generato una configurazione che non funziona per la topologia. Ad esempio, se si dispone di una topologia di foresta account-risorse ma si dispone di schema esteso hello nella foresta di account hello con uno schema di Exchange hello, le regole per Exchange vengono create per la foresta di account hello e foresta di risorse hello. In questo caso, è necessario toodisable hello regola di sincronizzazione per Exchange.

![Regola di sincronizzazione disabilitata](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

Nella figura hello precedente, hello è stato rilevato uno schema di Exchange 2003 precedente nella foresta di account hello. Questa estensione dello schema è stato aggiunto prima di foresta delle risorse hello è stato introdotto nell'ambiente di Fabrikam. tooensure attributi dall'implementazione di Exchange precedente hello non sono sincronizzati, la regola di sincronizzazione hello deve essere disabilitata, come illustrato.

### <a name="change-an-out-of-box-rule"></a>modificare una regola predefinita
unica volta Hello che è necessario modificare una regola di out-of-box è quando è necessaria una regola di join toochange hello. Se è necessario toochange un flusso dell'attributo, è necessario creare una regola di sincronizzazione con precedenza maggiore rispetto alle regole di hello out-of-box. Hello solo regola desiderate praticamente tooclone è hello **In ingresso da AD – User Join**. È possibile eseguire l'override di tutte le altre regole con una regola di precedenza superiore.

Se occorre una regola di toomake modifiche tooan out-of-box, è necessario effettuare una copia della regola out-of-box hello e disabilitare la regola originale hello. Verificare quindi regola clonato toohello modifiche di hello. Hello Editor regole di sincronizzazione si protegge con questi passaggi. Quando si apre una regola predefinita, viene visualizzata questa finestra di dialogo:   
![Avviso regola predefinita](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Selezionare **Sì** toocreate una copia della regola hello. regola di Hello duplicato viene quindi aperto.  
![Regola clonata](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

Questa regola clonato, apportare eventuali modifiche necessarie tooscope, join e trasformazioni.

## <a name="next-steps"></a>Passaggi successivi
**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
