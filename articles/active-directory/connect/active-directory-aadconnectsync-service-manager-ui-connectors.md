---
title: in Azure Active Directory Synchronization Service Manager UI hello aaaConnectors | Microsoft documenti
description: Comprendere scheda Connectors hello in hello Synchronization Service Manager per Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>Utilizzo dei connettori con hello Azure AD Connect sincronizzazione Service Manager

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

scheda Connectors Hello è usato toomanage motore di sincronizzazione di tutti i sistemi hello è connesso a.

## <a name="connector-actions"></a>Azioni del connettore
| Azione | Commento |
| --- | --- |
| Create |Non usare. Per la connessione AD tooadditional foreste, utilizzare Installazione guidata di hello. |
| Proprietà |Si usa per i filtri di unità organizzativa e dominio. |
| [Eliminazione](#delete) |Tooeither usato eliminare dati hello hello connettore spazio o toodelete connessione tooa foresta. |
| [Configura profili di esecuzione](#configure-run-profiles) |Ad eccezione di dominio di applicazione di filtri, nothing tooconfigure qui. È possibile utilizzare questa azione toosee già configurati profili di esecuzione. |
| Esegui |Utilizzare toostart una tantum esecuzione di un profilo. |
| Arresto |Arresta un connettore che sta eseguendo attualmente un profilo. |
| Esporta connettore |Non usare. |
| Importa connettore |Non usare. |
| Aggiorna connettore |Non usare. |
| Aggiorna schema |Aggiorna schema memorizzati nella cache di hello. Si tratta toouse preferito hello opzione nell'installazione guidata di hello, invece, dopo che anche gli aggiornamenti di sincronizzazione regole. |
| [Spazio connettore di ricerca](#search-connector-space) |Gli oggetti toofind utilizzati e troppo[seguire un oggetto e i relativi dati tramite il sistema hello](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Elimina
azione di eliminazione Hello viene utilizzato per due scopi diversi.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

opzione Hello **Elimina solo lo spazio connettore** rimuove tutti i dati, ma Mantieni hello configurazione.

opzione Hello **spazio eliminare connettori e** rimuove hello dati e la configurazione di hello. Questa opzione viene utilizzata quando non si desidera più tooconnect tooa foresta.

Entrambe le opzioni di sincronizzazione di tutti gli oggetti e aggiornare gli oggetti metaverse hello. L'esecuzione di questa azione richiede molto tempo.

### <a name="configure-run-profiles"></a>Configura profili di esecuzione
Questa opzione consente di hello toosee profili configurati per un connettore di esecuzione.

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Spazio connettore di ricerca
azione di spazio connettore ricerca Hello è utile toofind oggetti e risolvere i problemi di dati.

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Iniziare selezionando un **ambito**. È possibile eseguire la ricerca in base ai dati (RDN, DN, ancoraggio, sottostruttura ad albero), o dello stato dell'oggetto hello (tutte le altre opzioni).  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
Se ad esempio si esegue una ricerca nel sottoalbero, si ottengono tutti gli oggetti in una OU.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
In questa griglia è possibile selezionare un oggetto, selezionare **proprietà**, e [seguono](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) da spazio connettore di origine hello, tramite hello metaverse e toohello destinazione connettore.

### <a name="changing-hello-ad-ds-account-password"></a>Modifica password dell'account di dominio Active Directory hello Active Directory
Se si modifica la password dell'account hello, hello servizio di sincronizzazione non sarà più possibile tooimport esportare le modifiche locali tooon Active Directory.   Viene visualizzato il seguente hello:

- passaggio di importazione/esportazione Hello per hello Active Directory connector non riesce con errore "no-start-credenziali".
- In Visualizzatore eventi di Windows, log eventi dell'applicazione hello contiene un errore con ID evento 6000 e il messaggio "hello toorun di gestione agente"contoso.com"non è riuscita perché hello credenziali non sono valide."

eseguire tooresolve hello, account utente di aggiornamento hello di dominio Active Directory con hello seguenti:


1. Avviare hello Synchronization Service Manager (servizio di sincronizzazione iniziale →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Passare toohello **connettori** scheda.
3. Selezionare hello Active Directory Connector che è configurato toouse hello account di dominio Active Directory.
4. In Azioni selezionare **Proprietà**.
5. Nella finestra di dialogo popup hello, selezionare Connetti tooActive Directory foresta:
6. nome della foresta Hello indica hello corrispondente locale Active Directory.
7. nome utente Hello indica l'account di dominio Active Directory hello AD utilizzato per la sincronizzazione.
8. Immettere hello nuova password dell'account di dominio Active Directory AD hello nella casella di testo Password hello ![Azure AD Connect sincronizzazione crittografia chiave utilità](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. Fare clic su OK toosave hello nuova password e riavviare hello servizio di sincronizzazione tooremove hello vecchia password dalla cache di memoria.



## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
