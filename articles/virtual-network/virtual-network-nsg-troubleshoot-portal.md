---
title: aaaTroubleshoot gruppi di sicurezza di rete - portale | Documenti Microsoft
description: Informazioni su come gruppi di sicurezza di rete tootroubleshoot nella distribuzione di Azure Resource Manager hello del modello utilizzando hello portale di Azure.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>Risolvere i problemi relativi a gruppi di sicurezza di rete utilizzando hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Se si sono verificati problemi di connettività di macchina virtuale configurato rete sicurezza gruppi sulla macchina virtuale (VM), in questo articolo fornisce una panoramica delle funzionalità di diagnostica per NSGs toohelp risolvere il problema.

NSGs consentono tipi hello toocontrol di traffico che il flusso da e verso le macchine virtuali (VM). NSGs può essere applicato toosubnets in una rete virtuale di Azure (VNet), le interfacce di rete (NIC) o entrambi. Hello regole efficaci applicate tooa NIC sono un'aggregazione di regole hello esistenti hello NSGs applicato tooa NIC e hello subnet è connesso a. Talvolta le regole nei gruppi di sicurezza di rete possono essere in conflitto tra loro e influire sulla connettività di rete della VM.  

È possibile visualizzare tutte le regole di sicurezza efficace hello dal NSGs, così come applicato nelle schede NIC della macchina virtuale. Questo articolo illustra come problemi di connettività VM tootroubleshoot usando queste regole in hello modello di distribuzione Azure Resource Manager. Se non si ha familiarità con i concetti di rete virtuale e di gruppo, leggere hello [rete virtuale](virtual-networks-overview.md) e [gruppi di sicurezza di rete](virtual-networks-nsg.md) articoli Panoramica.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Utilizzando le regole di sicurezza efficace tootroubleshoot VM il flusso del traffico
scenario di Hello che segue è un esempio di un problema di connessione comuni:

Una macchina virtuale denominata *VM1* fa parte di una subnet denominata *Subnet1* in una rete virtuale denominata *WestUS-VNet1*. Un toohello tooconnect tentativo di VM che utilizzano il protocollo RDP sulla porta TCP 3389 ha esito negativo. NSGs vengono applicate a entrambi hello NIC *VM1 NIC1* e hello subnet *Subnet1*. La porta 3389 tooTCP di traffico è consentita in hello NSG associata con l'interfaccia di rete hello *VM1 NIC1*, tuttavia TCP effettuare il ping ha esito 3389 negativo di porta del tooVM1.

Mentre in questo esempio viene usata la porta TCP 3389, hello i passaggi seguenti può essere utilizzati toodetermine errori di connessione in ingresso e in uscita su qualsiasi porta.

### <a name="vm"></a>Visualizzare le regole di sicurezza effettive per una macchina virtuale
Completare hello seguendo i passaggi tootroubleshoot NSGs per una macchina virtuale:

È possibile visualizzare l'elenco completo delle regole di sicurezza efficace hello su una scheda di rete dalla macchina virtuale stessa hello. È inoltre possibile aggiungere, modificare ed eliminare le regole di gruppo NIC sia subnet dal pannello regole efficaci hello, se si dispone delle autorizzazioni tooperform queste operazioni.

1. Portale di Azure all'indirizzo https://portal.azure.com toohello di account di accesso.
2. Fare clic su **più servizi**, quindi fare clic su **macchine virtuali** nell'elenco visualizzato hello.
3. Selezionare tootroubleshoot una macchina virtuale dall'elenco di hello che viene visualizzata e viene visualizzato un pannello della macchina virtuale con opzioni.
4. Fare clic su **Diagnostica e risoluzione dei problemi** e quindi selezionare un problema comune. Per questo esempio, **toomy macchina virtuale di Windows non riesco a connettermi** è selezionata. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. Passaggi appaiono sotto problema hello, come illustrato nella seguente immagine hello: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    Fare clic su *regole gruppo di sicurezza efficace* nell'elenco di hello di procedure consigliate.
6. Hello **ottenere le regole di sicurezza efficace** pannello viene visualizzato, come illustrato nella seguente immagine hello:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    Tenere presente le sezioni seguenti di immagine hello hello:
   
   * **Ambito:** impostare troppo*VM1*, hello macchina virtuale selezionata nel passaggio 3.
   * **Interfaccia di rete:***VM1-NIC1* . Una VM può avere più interfacce di rete (NIC). Ogni interfaccia di rete può avere regole di sicurezza effettive univoche. Per risolvere il problema, le regole di sicurezza efficace hello tooview potrebbe essere necessario per ogni scheda di rete.
   * **Associato NSGs:** NSGs può essere applicato tooboth hello NIC e hello subnet hello è connessa al. Nell'immagine di hello, un gruppo è stato applicato tooboth hello NIC e hello subnet a che è connesso. È possibile fare clic sui nomi di gruppo hello toodirectly modificare le regole in hello NSGs.
   * **Scheda VM1 nsg:** elenco hello delle regole visualizzate nell'immagine di hello è hello NSG applicato toohello scheda di rete. Azure crea diverse regole predefinite quando viene creato un gruppo di sicurezza di rete. Non è possibile rimuovere le regole predefinite di hello, ma è possibile eseguirne l'override con regole di priorità più alta. altre informazioni sulle regole predefinite, leggere hello toolearn [Panoramica gruppo](virtual-networks-nsg.md#default-rules) articolo.
   * **Colonna di destinazione:** alcune regole hello con testo nella colonna hello, mentre gli altri sono i prefissi di indirizzo. testo Hello è il nome di hello della regola di sicurezza predefinita tag applicati toohello quando è stata creata. tag di Hello sono identificatori forniti dal sistema che rappresentano più prefissi. Selezione di una regola con un tag, ad esempio *AllowInternetOutBound*, Elenca i prefissi di hello in hello **prefissi di indirizzo** blade.
   * **Download:** elenco hello delle regole può richiedere tempi lungo. È possibile scaricare un file CSV di regole hello per l'analisi non in linea, fare clic su **scaricare** e salvataggio file hello.
   * **AllowRDP** regola in ingresso: questa regola consente a toohello connessioni RDP macchina virtuale.
7. Fare clic su hello **Subnet1 NSG** scheda tooview hello valide le regole da hello NSG applicate toohello subnet, come illustrato nella seguente immagine hello: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    Hello preavviso *denyRDP* **in ingresso** regola. Le regole in entrata applicate al subnet hello vengono valutate prima delle regole applicate all'interfaccia di rete hello. Poiché hello Nega regola viene applicata a subnet hello, hello richiesta tooconnect tooTCP 3389 ha esito negativo, hello consente la regola in hello NIC non viene mai valutata. 
   
    Hello *denyRDP* regola è motivo di hello motivi hello connessione RDP. Rimuoverlo dovrebbe risolvere il problema di hello.
   
   > [!NOTE]
   > Se hello VM associata con hello NIC non è in esecuzione, o NSGs non sono stato applicato toohello NIC o una subnet, le regole non vengono visualizzate.
   > 
   > 
8. Fare clic su regole NSG tooedit, *Subnet1 NSG* in hello **NSGs associata** sezione.
   Verrà visualizzata hello **Subnet1 NSG** blade. È possibile modificare direttamente le regole di hello facendo clic su **sicurezza regole connessioni in entrata**.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. Dopo la rimozione di hello *denyRDP* regola in entrata in hello **Subnet1 NSG** e l'aggiunta di un *allowRDP* regola, l'elenco di regole efficaci hello è simile a hello seguente immagine:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    Verificare che la porta TCP 3389 sia aperta aprendo un toohello connessione RDP macchina virtuale o lo strumento PsPing hello. È possibile approfondire PsPing da lettura hello [pagina di download PsPing](https://technet.microsoft.com/sysinternals/psping.aspx).

### <a name="nic"></a>Visualizzare le regole di sicurezza effettive per un'interfaccia di rete
Se il flusso di traffico della macchina virtuale ha un impatto per una scheda di rete specifico, è possibile visualizzare un elenco completo delle regole di validità hello per hello NIC dal contesto di interfacce di rete hello completando hello alla procedura seguente:

1. Portale di Azure all'indirizzo https://portal.azure.com toohello di account di accesso.
2. Fare clic su **più servizi**, quindi fare clic su **interfacce di rete** nell'elenco visualizzato hello.
3. Selezionare un'interfaccia di rete. In hello seguente immagine, una scheda di rete denominata *VM1 NIC1* è selezionata.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    Si noti che hello **ambito** è impostata l'interfaccia di rete toohello selezionata. altre informazioni sulle toolearn hello informazioni aggiuntive visualizzate, leggere passaggio 6 di hello **NSGs risoluzione dei problemi per una macchina virtuale** sezione di questo articolo.
   
   > [!NOTE]
   > Se un gruppo viene rimosso da un'interfaccia di rete, subnet hello gruppo è ancora valida in hello data scheda di rete. In questo caso, output di hello permetterebbe di visualizzare solo le regole dalla subnet hello gruppo. Le regole vengono visualizzate solo se hello NIC associata tooa macchina virtuale.
   > 
   > 
4. È possibile modificare direttamente le regole per i gruppi di sicurezza di rete associati a un'interfaccia di rete e a una subnet. toolearn, vedere passaggio 8 di hello **visualizzare le regole di sicurezza efficace per una macchina virtuale** sezione di questo articolo.

## <a name="nsg"></a>Visualizzare le regole di sicurezza effettive per un gruppo di sicurezza di rete
Quando la modifica delle regole di gruppo, è opportuno impatto hello tooreview delle regole di hello aggiunto in una determinata macchina virtuale. È possibile visualizzare un elenco completo delle regole di sicurezza efficace hello per tutti hello NIC che viene applicato un determinato gruppo, senza la necessità di contesto tooswitch da hello pannello gruppo specificato. tootroubleshoot regole valide all'interno di un gruppo, hello completo alla procedura seguente:

1. Portale di Azure all'indirizzo https://portal.azure.com toohello di account di accesso.
2. Fare clic su **più servizi**, quindi fare clic su **gruppi di sicurezza di rete** nell'elenco visualizzato hello.
3. Selezionare un gruppo di sicurezza di rete. Nella seguente immagine di hello, è stato selezionato un gruppo denominato VM1 gruppo.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    Tenere presente le sezioni seguenti di immagine precedente hello hello:
   
   * **Ambito:** impostare toohello gruppo selezionato.
   * **Macchina virtuale:** NSG un quando è applicato tooa subnet, è subnet della rete interfacce tooall collegato macchine virtuali connesse toohello tooall applicato. Questo elenco indica tutte le VM alle quali è applicato questo gruppo di sicurezza di rete. È possibile selezionare qualsiasi macchina virtuale dall'elenco di hello.
     
     > [!NOTE]
     > Se un gruppo è applicato tooonly una subnet vuota, non verranno elencate le macchine virtuali. Se un gruppo è applicato tooa scheda di rete che non è associata a una macchina virtuale, le schede NIC anche non verranno elencate. 
     > 
     > 
   * **Interfaccia di rete:** una macchina virtuale può avere più interfacce di rete. È possibile selezionare un'interfaccia di rete toohello collegato selezionato macchina virtuale.
   * **AssociatedNSGs:** in qualsiasi momento, una scheda di rete può essere composto tootwo NSGs efficace, uno applicato toohello NIC e le altre subnet toohello hello. Sebbene l'ambito hello VM1-gruppo, viene selezionata se hello NIC è una subnet efficace NSG, output di hello verranno visualizzati entrambi NSGs.
4. È possibile modificare direttamente le regole per i gruppi di sicurezza di rete associati a un'interfaccia di rete o a una subnet. toolearn, vedere passaggio 8 di hello **visualizzare le regole di sicurezza efficace per una macchina virtuale** sezione di questo articolo.

altre informazioni sulle toolearn hello informazioni aggiuntive visualizzate, leggere passaggio 6 di hello **visualizzare le regole di sicurezza efficace per una macchina virtuale** sezione di questo articolo.

> [!NOTE]
> Sebbene ogni una subnet e la scheda di rete può avere un solo gruppo applicato toothem, un gruppo può essere associato toomultiple NIC e più subnet.
> 
> 

## <a name="considerations"></a>Considerazioni
Prendere in considerazione hello seguenti punti durante la risoluzione dei problemi di connettività:

* Regole predefinite di NSG bloccherà l'accesso in ingresso da hello internet e solo Consenti rete virtuale il traffico in ingresso. Le regole devono essere aggiunto esplicitamente tooallow accesso in entrata da Internet, come richiesto.
* Se non sono presenti regole di sicurezza gruppo causando toofail connettività di rete della macchina virtuale, problema di hello può essere dovuto a:
  * Software di firewall in esecuzione all'interno del sistema operativo della macchina virtuale di hello
  * Route configurate per appliance virtuali o traffico locale. Il traffico Internet può essere reindirizzati tooon locali tramite il tunneling forzato. Una connessione RDP/SSH da hello Internet tooyour macchina virtuale potrebbe non funzionare con questa impostazione, a seconda di come hardware di rete locale hello gestisce tale traffico. Hello lettura [risoluzione dei problemi delle route](virtual-network-routes-troubleshoot-powershell.md) toolearn articolo come problemi di route toodiagnose che potrebbero ostacolare hello flusso del traffico in e out di hello macchina virtuale. 
* Se si dispongano di peering reti virtuali, per impostazione predefinita, hello tag VIRTUAL_NETWORK espanderà automaticamente i prefissi tooinclude per il peering reti virtuali. È possibile visualizzare tali prefissi nella hello **ExpandedAddressPrefix** elencare, tootroubleshoot qualsiasi tooVNet correlate a problemi peering di connettività. 
* Le regole di sicurezza efficace vengono visualizzate solo se è che un gruppo associato della macchina virtuale di hello NIC e o una subnet. 
* Se non sono non NSGs associato hello NIC o subnet e si dispone di un indirizzo IP pubblico assegnato tooyour VM, tutte le porte sarà aperte per l'accesso in ingresso e in uscita. Se hello macchina virtuale ha un indirizzo IP pubblico, l'applicazione NSGs toohello NIC o una subnet è consigliabile.

