---
title: aaaEnable Microsoft Windows Hello for Business dell'organizzazione | Documenti Microsoft
description: Tooenable di istruzioni di distribuzione Microsoft Passport all'interno dell'organizzazione.
services: active-directory
documentationcenter: 
keywords: configurare Microsoft Passport, distribuzione di Microsoft Windows Hello for Business
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>Abilitare Microsoft Windows Hello for Business nell'organizzazione
Dopo aver [collegamento dei dispositivi appartenenti a un dominio Windows 10 con Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), hello seguenti tooenable Microsoft Windows Hello for Business dell'organizzazione:

1. Distribuire System Center Configuration Manager  
2. Configurare le impostazioni dei criteri
3. Configurare il profilo di certificato hello  

## <a name="deploy-system-center-configuration-manager"></a>Distribuire System Center Configuration Manager
i certificati utente toodeploy basati su Windows Hello per le chiavi di Business, è necessario seguente hello:

* **System Center Configuration Manager Current Branch** -è necessario tooinstall versione 1606 o migliori. Per ulteriori informazioni, vedere hello [documentazione per System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) e [blog del Team di System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).
* **Infrastruttura a chiave pubblica (PKI)** -tooenable Microsoft Windows Hello for Business utilizzando i certificati utente, è necessario disporre di un'infrastruttura PKI sul posto. Se non si dispone di uno o non si desidera toouse è per i certificati utente, è possibile distribuire un nuovo controller di dominio con Windows Server 2016 compilare 10551 (o versione successiva) installato. Seguire i passaggi di hello troppo[installare un controller di dominio di replica in un dominio esistente](https://technet.microsoft.com/library/jj574134.aspx) o troppo[installare una nuova foresta di Active Directory, se si sta creando un nuovo ambiente](https://technet.microsoft.com/library/jj574166). (hello immagini ISO disponibili per il download [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)

## <a name="configure-policy-settings"></a>Configurare le impostazioni dei criteri
hello tooconfigure Microsoft Windows Hello per le impostazioni di criteri di Business, sono disponibili due opzioni:

* Criteri di gruppo in Active Directory 
* Hello System Center Configuration Manager 

Utilizza criteri di gruppo in Active Directory sono hello consigliato metodo tooconfigure, Microsoft Windows Hello per le impostazioni dei criteri di Business. 

Con System Center Configuration Manager è il metodo di hello preferito quando si utilizzano anche il toodeploy certificati. Questo scenario:

* Assicura la compatibilità con gli scenari di distribuzione più recente hello
* Richiede sul lato client di hello 1607 versione di Windows 10 o versione successiva.

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>Configurare Microsoft Windows Hello for Business tramite Criteri di gruppo in Active Directory
**Passaggi**:

1. Aprire Server Manager e passare troppo**strumenti** > **Gestione criteri di gruppo**.
2. Da Gestione criteri di gruppo passare nodo toohello corrispondente toohello dominio in cui si desidera tooenable aggiunta ad Azure AD.
3. Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo** e scegliere **Nuovo**. Assegnare un nome all'oggetto Criteri di gruppo, ad esempio Abilita Windows Hello for Business. Fare clic su **OK**.
4. Fare clic con il pulsante destro del mouse sul nuovo oggetto Criteri di gruppo e scegliere **Modifica**.
5. Passare troppo**configurazione Computer** > **criteri** > **modelli amministrativi** > **Windows Componenti** > **Windows Hello for Business**.
6. Fare doppio clic su **Abilita Windows Hello for Business** e selezionare **Modifica**.
7. Seleziona hello **abilitato** pulsante di opzione e quindi fare clic su **applica**. Fare clic su **OK**.
8. È ora possibile collegare hello oggetto Criteri di gruppo tooa nel percorso desiderato. tooenable questo criterio per tutti hello appartenenti a un dominio Windows 10 nei dispositivi dell'organizzazione, dominio toohello di collegamento hello criteri di gruppo. ad esempio:
   * Una specifica unità organizzativa in Active Directory in cui saranno posizionati i computer Windows 10 aggiunti a un dominio.
   * Uno specifico gruppo di sicurezza contenente i computer appartenenti a un dominio di Windows 10 che verranno registrati automaticamente in Azure AD.

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>Configurare Windows Hello for Business mediante System Center Configuration Manager
**Passaggi**:

1. Aprire hello **System Center Configuration Manager**, quindi passare troppo**asset e conformità > Impostazioni di conformità > accesso alle risorse aziendali > Windows Hello per i profili di Business**.
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. Nella barra degli strumenti hello in primo piano hello, fare clic su **creare Windows Hello per le aziende profilo**.
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. In hello **generale** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    a. In hello **nome** casella di testo, digitare un nome per il profilo, ad esempio, **profilo WHfB**.
   
    b. Fare clic su **Avanti**.
4. In hello **piattaforme supportate** finestra di dialogo, piattaforme selezionare hello che verranno eseguito il provisioning con questo Windows Hello per il profilo di business e quindi fare clic su **Avanti**.
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. In hello **impostazioni** finestra di dialogo, eseguire hello alla procedura seguente:
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    a. Per **Configura Windows Hello for Business** selezionare **Attivato**.
   
    b. Per **Usa Trusted Platform Module (TPM)** selezionare **Richiesto**. 
   
    c. Per **Metodo di autenticazione** selezionare **Basata su certificati**.
   
    d. Fare clic su **Avanti**.
6. In hello **riepilogo** finestra di dialogo, fare clic su **Avanti**.
7. In hello **completamento** finestra di dialogo, fare clic su **Chiudi**.
8. Nella barra degli strumenti hello in primo piano hello, fare clic su **Distribuisci**.
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>Configurare il profilo di certificato hello
Se si utilizza l'autenticazione basata su certificato per l'autenticazione locale, è necessario tooconfigure e distribuire un profilo del certificato. Questa attività è necessario tooset un server NDES e il ruolo del sito punto di registrazione certificati in hello System Center Configuration Manager. Per ulteriori informazioni, vedere hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).

1. Aprire hello **System Center Configuration Manager**, quindi passare troppo**asset e conformità > Impostazioni di conformità > accesso alle risorse aziendali > i profili certificato**.
2. Selezionare un modello dotato di utilizzo chiavi avanzato (EKU) per l'accesso con smart card.

In hello **registrazione SCEP** pagina hello profilo del certificato, è necessario toochoose **installare tooPassport per Work oppure genera errore** come hello **Provider di archiviazione chiavi**.

## <a name="next-steps"></a>Passaggi successivi
* [Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Autenticazione delle identità senza password con Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)

