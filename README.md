Create un nuovo progetto utilizzando Vite e Vue 3 e definite i componenti necessari per strutturare il layout come da screenshot allegato.
Al caricamento della pagina, effettuate una chiama ajax all'API di Yu Gi Oh: https://db.ygoprodeck.com/api/v7/cardinfo.php e con i dati restituiti, stampate una card per ogni carta.
ATTENZIONE:
l’api restituisce tutti i risultati in un colpo solo.
Per evitare attese e/o rallentamenti nelle richieste, potete diminuire il numero di risultati sfruttando i parametri num e offset
https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0
Bonus:
Creare un componente loader da visualizzare fintantoché i risultati non sono pronti.
Documentazione:
https://ygoprodeck.com/api-guide/


----- PASSAGGI -----
- creo macrostruttura con componenti AppHeader e AppMain, collegando i nuovi componenti ad AppVue
- AppHeader: creo un semplice header con una navbar di bootstrap
- AppMain:
    - creo un container per racchiudere tutto il contenuto di main
    - creo un nuovo componente per una section per raggruppare gli elementi card
        - richiamo con l'API la lista di carte
        - creo un div per racchiudere gli article che saranno riempiti con il componente delle carte singole attraverso un v-for
    - creo un nuovo componente che si occuperà di gestire la singola carta