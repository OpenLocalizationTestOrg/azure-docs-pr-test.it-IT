---
title: 'Azure Active Directory B2C: attributi personalizzati | Documentazione Microsoft'
description: "La modalità di attributi personalizzati di toouse in Azure Active Directory B2C toocollect informazioni utenti"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Azure Active B2C di Directory: Utilizzare attributi personalizzati toocollect informazioni utenti
La directory Azure Active Directory (Azure AD) B2C viene fornita con un set predefinito di informazioni (attributi), ad esempio nome, cognome, città, codice postale e altri attributi. Tuttavia, ogni applicazione per consumatori presenta requisiti specifici su quali toogather attributi dal consumer. Con Azure Active Directory B2C, è possibile estendere il set di hello di attributi archiviati in ogni account utente. È possibile creare attributi personalizzati in hello [portale di Azure](https://portal.azure.com/) e usare nei criteri per l'abbonamento, come illustrato di seguito. È anche possibile leggere e scrivere tali attributi tramite hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Gli attributi personalizzati usano le [Estensioni dello schema di directory dell'API Graph di Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Creare un attributo personalizzato
1. [Seguire questi blade di passaggi toonavigate toohello B2C funzionalità nel portale di Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Fare clic su **Attributi utente**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un **nome** per l'attributo personalizzato hello (ad esempio, "ShoeSize") e, facoltativamente, un **descrizione**. Fare clic su **Crea**.
   
   > [!NOTE]
   > Solo hello "Stringa" **tipo di dati** è attualmente disponibile.
   > 
   > 

attributo personalizzato Hello è ora disponibile nell'elenco di hello di **gli attributi utente**e per l'uso nei criteri per l'abbonamento.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Usare un attributo personalizzato nei criteri di iscrizione
1. [Seguire questi blade di passaggi toonavigate toohello B2C funzionalità nel portale di Azure hello](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Fare clic su **Criteri di iscrizione**.
3. Fare clic su tooopen i criteri di iscrizione (ad esempio, "B2C_1_SiUp") è. Fare clic su **modifica** nella parte superiore di hello del pannello hello.
4. Fare clic su **attributi iscrizione** e l'attributo personalizzato selezionare hello (ad esempio, "ShoeSize"). Fare clic su **OK**.
5. Fare clic su **attestazioni applicazione** e l'attributo personalizzato hello selezionare. Fare clic su **OK**.
6. Fare clic su **salvare** nella parte superiore di hello del pannello hello.

È possibile utilizzare funzionalità "Esegui" hello sull'esperienza di hello criteri tooverify hello consumer. Dovrebbero ora vedere "ShoeSize" nell'elenco di hello di attributi raccolti durante l'iscrizione consumer e visualizzarlo in un'applicazione hello token tooyour indietro inviato.

## <a name="notes"></a>Note
* Insieme ai criteri di iscrizione, gli attributi personalizzati possono essere usati anche nei criteri di iscrizione o accesso e nei criteri di modifica del profilo.
* Esiste una limitazione nota degli attributi personalizzati. È solo creato hello prima volta che viene utilizzata in tutti i criteri e non quando si aggiungerla elenco toohello di **gli attributi utente**.

