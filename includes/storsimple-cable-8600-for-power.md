<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a>toocable il dispositivo per l'alimentazione
> [!NOTE]
> Entrambi gli enclosure nel dispositivo StorSimple includono PCM ridondanti. Per ogni enclosure, hello PCM deve essere installato e connesso toodifferent power origini tooensure la disponibilità elevata.
> 
> 

1. Assicurarsi che tutti i moduli PCM hello interruttori di alimentazione hello siano in posizione OFF hello.
2. Sull'enclosure principale hello, connettersi tooboth cavi di alimentazione hello PCM. Hello cavi di alimentazione sono identificati in rosso in power hello cablaggio diagramma, di seguito.
3. Assicurarsi che hello due moduli PCM hello enclosure principale usino separato fonti di alimentazione.
4. Collegare hello power cavi toohello accensione unità di distribuzione di hello rack come illustrato nel diagramma di cablaggio di alimentazione hello.
5. Ripetere i passaggi da 2 a 4 per hello enclosure EBOD.
6. Accendere l'enclosure EBOD hello girando l'interruttore di alimentazione hello in posizione on toohello ogni PCM.
7. Verificare che hello enclosure EBOD sia attiva assicurandosi che il LED verde hello su hello parte posteriore di controller EBOD hello è accesi.
8. Accendere l'enclosure principale hello girando toohello in posizione on commutatore ogni PCM.
9. Verificare che il sistema hello sia nel assicurandosi che i controller di dispositivo hello che LED siano accesi.
10. Assicurarsi che la connessione hello tra controller EBOD hello e controller del dispositivo hello sia attiva verificando che siano di colore verde hello quattro LED Avanti toohello porta SAS sul controller EBOD hello.
    
    > [!IMPORTANT]
    > tooensure la disponibilità elevata per il sistema, si consiglia di attenersi schema illustrato nel seguente diagramma hello di cablaggio di alimentazione di toohello.
    > 
    > 
    
    ![Cablare il dispositivo 4U per l'alimentazione](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    **Cablaggio di alimentazione**
    
    | Etichetta | Descrizione |
    |:--- |:--- |
    | 1 |Enclosure principale |
    | 2 |PCM 0 |
    | 3 |PCM 1 |
    | 4 |Controller 0 |
    | 5 |Controller 1 |
    | 6 |Controller 0 EBOD |
    | 7 |Controller 1 EBOD |
    | 8 |Chassis EBOD |
    | 9 |PDU |

