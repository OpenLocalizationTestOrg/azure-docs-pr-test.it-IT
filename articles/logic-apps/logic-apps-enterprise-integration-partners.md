---
title: i partner aaaCreate per i messaggi di business-to-business (B2B) - App Azure per la logica | Documenti Microsoft
description: Informazioni su come integrazione di tooyour tooadd partner account con Enterprise Integration Pack hello e App per la logica
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a>Aggiungere o aggiornare i partner nei contratti Business to Business nel proprio flusso di lavoro

I partner sono le entità che partecipano alle transazioni e allo scambio di messaggi Business-To-Business (B2B). Prima di poter creare i partner che rappresentano l'utente e l'altra organizzazione nelle transazioni, è necessario che entrambe le parti condividano le informazioni che identificano e convalidano i messaggi inviati. Dopo aver discuterne i dettagli e sono pronti toostart la relazione di business, è possibile creare partner il toorepresent di account di integrazione da entrambi.

## <a name="what-roles-do-partners-have-in-your-integration-account"></a>Che ruoli hanno i partner nell'account di integrazione?

toodefine informazioni dettagliate relative ai messaggi hello scambiati tra i partner, creare contratti tra tali partner. Tuttavia, prima di poter creare un accordo, è necessario aver aggiunto account di integrazione tooyour almeno due partner. L'organizzazione deve far parte del contratto di hello hello **partner host**. Hello altri partner, o **partner guest** rappresenta hello organizzazione che scambia messaggi con l'organizzazione. partner guest Hello può essere un'altra società, o anche un reparto dell'organizzazione.

Dopo aver aggiunto i partner, è possibile creare un contratto.

Ricevere e inviare le impostazioni sono orientate da hello punto di vista di hello Partner ospitato. Ad esempio, hello impostazioni di ricezione in un contratto di determinare come partner di hello ospitato riceve i messaggi inviati da un partner guest. Analogamente, le impostazioni di invio hello contratto hello indicano come partner ospitato hello invia al partner guest toohello di messaggi.

## <a name="how-toocreate-a-partner"></a>Come toocreate un partner?

1. Nel portale di Azure hello, selezionare **Sfoglia**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Nella casella di ricerca hello filtro immettere **integrazione**, quindi selezionare **account di integrazione** nell'elenco risultati hello.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Selezionare l'account di integrazione hello in cui si desidera tooadd i partner.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Seleziona hello **partner** riquadro.

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. Nel Pannello di partner hello, scegliere **Aggiungi**.

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. Immettere il nome del partner, quindi selezionare un **Qualificatore**. Infine, immettere un **valore** toohelp identificare documenti che entrano in App.

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. stato di avanzamento hello toosee per il processo di creazione di partner, seleziona hello *campanello* icona di notifica.

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. tooconfirm che nuovo partner sono stati aggiunti, seleziona hello **partner** riquadro.

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    Dopo aver selezionato il riquadro di partner hello, si noterà anche partner appena aggiunto nel Pannello di hello partner.

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a>Tooedit esistente come partner nell'account di integrazione

1. Seleziona hello **partner** riquadro.
2. Dopo l'apertura di blade partner hello, selezionare il partner di hello desiderato tooedit.
3. In hello **aggiornamento Partner** riquadro, apportare le modifiche.
4. Al termine, scegliere **salvare**, o selezionare le modifiche, toocancel **ignorare**.

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a>Come toodelete un partner

1. Seleziona hello **partner** riquadro.
2. Dopo l'apertura di blade Partner hello, selezionare il partner di hello che si desidera toodelete.
3. Scegliere **Elimina**.

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sui contratti](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  

