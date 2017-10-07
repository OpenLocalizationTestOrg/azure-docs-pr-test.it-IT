---
title: i dispositivi aaaManaging usando hello portale di Azure - anteprima | Documenti Microsoft
description: Informazioni su come toouse hello dispositivi toomanage portale Azure.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>Gestendo i dispositivi con hello portale di Azure - anteprima

>[!NOTE]
>Questa funzionalità è attualmente disponibile in anteprima pubblica. Essere preparati toorevert o rimuovere tutte le modifiche. funzionalità di Hello è disponibile in alcuna sottoscrizione di Azure Active Directory (Azure AD) durante l'anteprima pubblica. Tuttavia, quando la funzionalità hello diventa disponibile in genere, alcuni aspetti della funzionalità hello potrebbero richiedere una sottoscrizione di Azure Active Directory premium.


Tramite la gestione dei dispositivi in Azure Active Directory (Azure AD) è possibile garantire che gli utenti accedano alle risorse da dispositivi che soddisfano gli standard di sicurezza e conformità. 

In questo argomento:

- Si presuppone che abbia familiarità con hello [gestione toodevice introduzione in Azure Active Directory](device-management-introduction.md)

- Vengono fornite con informazioni sulla gestione dei dispositivi utilizzando hello portale di Azure


dispositivi toomanage in hello portale di Azure, è necessario tooclick **dispositivi** in hello **Gestisci** sezione di hello hello **Azure Active Directory** blade.

![Gestire un dispositivo Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>Configurare le impostazioni dei dispositivi

i dispositivi con hello portale di Azure, è necessario toobe toomanage registrato o unita tooAzure Active Directory. Come amministratore, è possibile ottimizzare il processo di hello di registrazione e l'unione dei dispositivi, configurare le impostazioni di dispositivo hello.

![Gestire un dispositivo Intune](./media/device-management-azure-portal/22.png)


pannello delle impostazioni di dispositivo Hello consente tooconfigure:

- **Gli utenti possono aggiungere dispositivi tooAzure AD** - questa impostazioni consente agli utenti di hello tooselect in grado di aggiungere dispositivi tooAzure AD. valore predefinito di Hello è **tutti**.

- **Altri amministratori locali in Azure AD i dispositivi appartenenti** -è possibile selezionare gli utenti di hello che vengono concessi diritti di amministratore locale su un dispositivo. Gli utenti aggiunti vengono aggiunti toohello *amministratori dispositivo* ruolo in Azure AD. Agli amministratori globali di Azure AD e ai proprietari dei dispositivi vengono concessi i diritti di amministratore locale per impostazione predefinita. Questa opzione è una funzionalità di edizione premium disponibile tramite prodotti, come Azure AD Premium o Enterprise Mobility Suite (EMS) hello. 

- **Gli utenti possono registrare i propri dispositivi con Azure AD** -è necessario tooconfigure toobe di dispositivi tooallow questa impostazione è registrato con Azure AD. Se si seleziona **Nessuno**, i dispositivi non sono consentiti tooregister quando non sono parte di Azure AD o ibrida aggiunto AD Azure. L'iscrizione a Microsoft Intune o Gestione dispositivi mobili per Office 365 richiede la registrazione. Se è stato configurato uno di questi servizi, sarà selezionata l'opzione **TUTTI**, mentre l'opzione **NESSUNO** sarà disabilitata.

- **Richiedi multi-Factor Authentication toojoin dispositivi** -è possibile scegliere se gli utenti sono necessari tooprovide una seconda autenticazione fattori toojoin loro tooAzure dispositivo Active Directory. valore predefinito di Hello è **n**. Si consiglia di richiedere l'autenticazione a più fattori quando si registra un dispositivo. Prima di abilitare multi-factor authentication per questo servizio, è necessario assicurarsi che l'autenticazione a più fattori è configurato per gli utenti di hello che registrano i propri dispositivi. Per altre informazioni sui diversi servizi di autenticazione a più fattori di Azure, vedere [Introduzione ad Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md). 

- **Numero massimo di dispositivi** -questa impostazione consente massimo hello tooselect di dispositivi che un utente può disporre di Azure AD. Se un utente raggiunge questa quota, non sono in altri dispositivi in grado di tooadd fino a quando una o più dispositivi esistenti hello vengono rimossi. offerta dispositivo Hello viene conteggiata per tutti i dispositivi che sono parte di Azure AD o Azure AD attualmente registrata. valore predefinito di Hello è **20**.

- **Gli utenti possono sincronizzare le impostazioni e dati delle app tra dispositivi** -per impostazione predefinita, questa impostazione è troppo**Nessuno**. Selezionare utenti specifici o gruppi o tutti consente le impostazioni dell'utente hello e app dati toosync tra i propri dispositivi Windows 10. Leggere altre informazioni sul funzionamento della sincronizzazione in Windows 10.
Questa opzione è delle funzionalità disponibile tramite prodotti, come Azure AD Premium o Enterprise Mobility Suite (EMS) hello.
 
    ![Gestire un dispositivo Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>Individuare i dispositivi

Come amministratore, nel portale di Azure hello sono disponibili due opzioni toolocate registrato e aggiunto i dispositivi:

- **Tutti i dispositivi** in hello **Gestisci** sezione di hello **dispositivi** pannello  

    ![Tutti i dispositivi](./media/device-management-azure-portal/41.png)


- **Dispositivi** in hello **Gestisci** sezione di un **utente** pannello
 
    ![Tutti i dispositivi](./media/device-management-azure-portal/43.png)



Con entrambe le opzioni, è possibile ottenere la visualizzazione tooa che:


- Consente di toosearch per i dispositivi con nome visualizzato hello come filtro.

- Fornisce una panoramica dettagliata dei dispositivi registrati e aggiunti

- Consente di tooperform delle attività di gestione comuni di dispositivi
   

![Tutti i dispositivi](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>Attività di gestione dei dispositivi

Come amministratore, è possibile gestire hello registrato o aggiunto i dispositivi. Questa sezione fornisce informazioni sulle attività comuni di gestione dei dispositivi.


**Gestire un dispositivo Intune**: un amministratore di Intune può gestire i dispositivi contrassegnati come **Microsoft Intune**. L'amministratore può visualizzare un dispositivo aggiuntivo 

![Gestire un dispositivo Intune](./media/device-management-azure-portal/31.png)


**Abilitare o disabilitare un dispositivo Azure AD**

tooenable o disattivare un dispositivo, è necessario toobe un amministratore globale di Azure AD. La disabilitazione di un dispositivo ne impedisce l'accesso alle risorse di Azure AD.  dispositivo hello toodisable, è possibile fare clic su *...* Fare clic su dispositivo hello per altri dettagli.

 
![Gestire un dispositivo Intune](./media/device-management-azure-portal/33.png)

La disabilitazione di un dispositivo cambia lo stato di hello in hello **abilitato** colonna troppo**n**.

![Disabilitare un dispositivo](./media/device-management-azure-portal/32.png)


**Eliminare un dispositivo di Azure AD** -toodelete un dispositivo, è necessario toobe un amministratore globale di Azure AD.  
L'eliminazione di un dispositivo comporta quanto segue:
 
- Impedisce l'accesso del dispositivo alle risorse di Azure AD 

- Rimuove tutti i dettagli dispositivo toohello collegato, ad esempio, le chiavi di BitLocker per i dispositivi Windows  

- È un'attività non reversibile e non è consigliata, a meno che non sia necessaria

Se un dispositivo è gestito da un'altra autorità di gestione (ad esempio Microsoft Intune), assicurarsi che il dispositivo hello è stato cancellato / ritirato prima di eliminarlo hello in Azure AD.

È possibile selezionare "…" toodelete hello dispositivo oppure fare clic sul dispositivo hello per altri dettagli
 
![Eliminare un dispositivo](./media/device-management-azure-portal/34.png)


**Consente di visualizzare o copiare l'ID dispositivo** -è possibile utilizzare un dispositivo ID tooverify hello dispositivo ID dettagli sul dispositivo di hello o utilizzo di PowerShell durante la risoluzione dei problemi. copia di hello tooaccess opzione, fare clic su dispositivo hello.

![Visualizzare l'ID dispositivo](./media/device-management-azure-portal/35.png)
  

**Consente di visualizzare o copiare le chiavi BitLocker** -se si è un amministratore, è possibile visualizzare e hello copia BitLocker chiavi toohelp utenti toorecover le unità crittografata. Queste chiavi sono disponibili solo per i dispositivi Windows crittografati e le cui chiavi sono archiviate in Azure AD. È possibile copiare queste chiavi quando si accede ai dettagli del dispositivo hello.
 
![Visualizzare le chiavi BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>Log di controllo


le attività di Hello dispositivo sono disponibili tramite log attività hello. Sono incluse attività attivata dal servizio Registrazione dispositivi di hello o dall'utente hello:

- Creazione di un dispositivo e l'aggiunta di proprietari/gli utenti sul dispositivo hello

- Modifica le impostazioni di toodevice

- Funzionamento del dispositivo, ad esempio eliminazione o aggiornamento
 
Il toohello punto di ingresso dati di controllo è **log di controllo** in hello **attività** sezione di hello **dispositivi* blade.

![Log di controllo](./media/device-management-azure-portal/61.png)


Un log di controllo è una visualizzazione elenco predefinita che include:

- Hello data e ora dell'occorrenza hello

- destinazioni Hello

- Hello iniziatore / attore (che) di un'attività

- attività Hello (novità)

![Log di controllo](./media/device-management-azure-portal/63.png)

È possibile personalizzare una visualizzazione elenco hello facendo **colonne** nella barra degli strumenti hello.
 
![Log di controllo](./media/device-management-azure-portal/64.png)


toonarrow verso il basso hello segnalati livello tooa dati che funziona per l'utente, è possibile filtrare i dati di controllo hello utilizzando hello seguenti campi:

- Categoria
- Activity resource type (Tipo di risorsa dell'attività)
- Attività
- Intervallo di date
- Destinazione
- Azione avviata da (attore)

Inoltre toohello filtri, è possibile cercare voci specifiche.

![Log di controllo](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>Passaggi successivi

* [Gestione toodevice introduzione in Azure Active Directory](device-management-introduction.md)



