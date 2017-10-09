---
title: Installazione guidata di rieseguire hello Azure AD Connect | Documenti Microsoft
description: Viene illustrata l'installazione guidata di hello hello alla seconda esecuzione.
keywords: installazione guidata di Hello Azure AD Connect consente di configurare hello le impostazioni di manutenzione alla seconda esecuzione
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Sincronizzazione di Azure AD Connect: installazione guidata di hello una seconda volta
Hello prima volta che si esegue l'installazione guidata di hello Azure AD Connect, illustra come tooconfigure l'installazione. Se si esegue l'installazione guidata di hello nuovamente, offre opzioni per la manutenzione.

È possibile trovare l'installazione guidata di hello nel menu start hello denominato **Azure AD Connect**.

![Menu Start](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

Quando si avvia l'installazione guidata di hello, viene visualizzata una pagina con queste opzioni:

![Pagina con un elenco di attività aggiuntive](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Se con Azure AD Connect è stato installato AD FS saranno disponibili ancora più opzioni. opzioni aggiuntive disponibili per ADFS sono documentati in Hello [gestione ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Selezionare una delle attività hello e fare clic su **Avanti** toocontinue.

> [!IMPORTANT]
> Mentre installazione guidata di hello è aperto, tutte le operazioni nel motore di sincronizzazione hello vengono sospesi. Assicurarsi di chiudere installazione guidata di hello subito dopo aver completato le modifiche di configurazione.
>
>

## <a name="view-current-configuration"></a>Visualizzazione della configurazione corrente
Questa opzione consente di visualizzare rapidamente le opzioni attualmente configurate.

![Pagina con un elenco di tutte le opzioni e il relativo stato](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Fare clic su **precedente** toogo back. Se si seleziona **uscita**, si chiude l'installazione guidata di hello.

## <a name="customize-synchronization-options"></a>Personalizzazione delle opzioni di sincronizzazione
Questa opzione è una configurazione della sincronizzazione toohello modifiche toomake utilizzato. Vedrai un subset di opzioni dal percorso di installazione di hello configurazione personalizzata. Queste opzioni vengono visualizzate anche se inizialmente è stata usata l'installazione rapida.

* [Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories)(Aggiunta di altre directory). Per rimuovere una directory, vedere [Eliminazione di un connettore](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)(Modifica dei filtri di unità organizzativa e dominio).
* Remove Group filtering (Rimozione dei filtri di gruppo).
* [Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features)(Modifica delle funzionalità facoltative).

Hello altre opzioni di installazione iniziale di hello non possono essere modificati e non sono disponibili. Queste opzioni sono:

* Modificare hello toouse di attributo per gli attributi userPrincipalName e sourceAnchor.
* Modificare hello aggiunta metodo per gli oggetti da una foresta diversa.
* Abilitazione dei filtri basati sui gruppi.

## <a name="refresh-directory-schema"></a>Aggiorna lo schema della directory
Questa opzione viene utilizzata se è stata modificata schema hello in uno dei locale foreste di Active Directory. Ad esempio, si potrebbe essere installato Exchange o aggiornata lo schema tooa Windows Server 2012 con gli oggetti dispositivo. In questo caso, è necessario tooinstruct Azure AD Connect tooread hello schema nuovamente da AD DS e aggiornare la cache. Questa operazione rigenera anche le regole di sincronizzazione hello. Se si aggiunta schema Exchange hello, ad esempio, le regole di sincronizzazione hello per Exchange vengono aggiunti toohello configurazione.

Quando si seleziona questa opzione, vengono elencate tutte le directory hello nella configurazione. È possibile mantenere l'impostazione predefinita hello e aggiornare tutte le foreste o deselezionare alcuni di essi.

![Pagina con un elenco di tutte le directory nell'ambiente di hello](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Configurazione della modalità di gestione temporanea
Questa opzione consente di tooenable e disabilitare la modalità di gestione temporanea nel server di hello. Per altre informazioni sull'uso della modalità di gestione temporanea, vedere [Operazioni](active-directory-aadconnectsync-operations.md#staging-mode).

opzione Hello Mostra se gestione temporanea è attualmente abilitato o disabilitato:  
![Opzione che viene inoltre visualizzato lo stato corrente di hello della modalità di gestione temporanea](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange hello stato, selezionare questa opzione e hello selezionare o deselezionare la casella di controllo.  
![Opzione che viene inoltre visualizzato lo stato corrente di hello della modalità di gestione temporanea](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Cambia l'accesso utente
Questa opzione consente di toochange da toofederation di sincronizzazione password o viceversa hello. Non è possibile modificare troppo**non si configura**.

Per altre informazioni su questa opzione, vedere [Accesso utente](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sul modello di configurazione hello utilizzato dalla sincronizzazione di Azure AD Connect in [Provisioning dichiarativo comprensione](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
