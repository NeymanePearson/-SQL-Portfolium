tutorial instructions (in italian):
Per svolgere questo esercizio utilizzeremo il database foodmart . Seguite le istruzioni del docente per
accedere all’ambiente di lavoro (o in alternativa leggete le istruzioni apposite nel sito del corso).
Esercizi
Nei prossimi esercizi, vi sarà richiesto di analizzare le vendite del 1998, contenute nella tabella sales_fact_1998.
Le query seguenti servono per effettuare una valutazione delle attività di gestione della catena di supermercati.
L’obiettivo della valutazione è identificare degli interventi per aumentare sia il fatturato sia il reddito dei
supermercati. Dopo aver realizzato le query descritte nei punti seguenti, create ulteriori query liberamente, in
modo da completare a vostro piacere l’attività di valutazione. Le indicazioni sui risultati sono riportate dopo
l’ultimo punto
Attività di marketing. Le query seguenti permettono di analizzare le attività di marketing svolte
1. Ci sono dei prodotti venduti sottocosto nel 1998? I prodotti sottocosto sono quelli per cui il valore
dell’attributo store_cost è maggiore del valore di store_sales
2. Individuate le promozioni che hanno fatto guadagnare di più nelle vendite del 1998. Il guadagno associato
ad una promozione è dato dal guadagno originato dalle vendite dei beni oggetto della promozione. Per
avere informazioni sulle promozioni guardate l’attributo sales_fact_1998.promotion_id e la tabella
promotion. Visualizzate il guadagno totale generato e il nome di ogni promozione. Nel calcolo, non
considerate i costi presenti nella tabella promotion. Visualizzate le promozioni in ordine decrescente di
guadagno totale (escludete dalla visualizzazione la non promozione indicata con il nome “No Promotion”).
Margine e redditività. Le query seguenti permettono di analizzare come l’azienda costruisce utile e margine. Il
margine è un indicatore definito con qs formula: margine = (ricavo tot.– costo tot.) / ricavo tot.
3. Individuate i 5 prodotti che offrono il margine maggiore (suggerimento: ordinate il risultato di una query e
del risultato considerate solo le prime 5 tuple).
4. Individuate le 5 categorie di prodotti che offrono il margine maggiore. La categoria di un prodotto è
identificata dall’attributo ‘product_class.product_category’.
5. Individuate i 5 settori merceologici del supermercato che offrono il margine maggiore. Il settore
merceologico è identificata dall’attributo ‘product_class.product_department’.
6. Come il punto precedente, tuttavia visualizzate i product_department che offrono un margine superiore al
valore di 0,6 (60%).
Analisi del porfoglio vendite. Le query seguenti permettono di analizzare le attività di vendita
7. In questo punto vi sarà richiesto di scrivere delle query che permettano di confrontare, per ogni
supermercato della catena, le vendite del settore carni con il settore prodotti in scatola. Questo esercizio
sarà suddiviso in sottopunti.
a. Individuate per ogni negozio il ricavo conseguito vendendo i prodotti del settore merceologico “Prodotti
in scatola” (valore “Canned Products” dell’attributo product_department della tabella product_class). La
query deve visualizzare l’id del supermercato e il ricavo conseguente alla vendita dei prodotti del settore
“Prodotti in scatola”. Per ogni supermercato deve apparire una sola riga.
b. Come la query precedente, analizzando però il settore carni (valore “Meat” dell’attributo
product_department della tabella product_class).
c. [NB: per svolgere questo punto è necessario utilizzare le query annidate] Costruite una query che per
ogni supermercato mostri: il valore delle vendite del settore “Prodotti in scatola”; il valore delle vendite
del settore carni; il rapporto tra le vendite del settore carni e le vendite del settore “Prodotti in scatola”.
Suggerimento: per poter scrivere la query richiesta è necessario utilizzare le dei due punti precedenti
come query annidate. L’esempio che segue mostra l’uso delle query annidate (o sottoquery):
select …
from tab_a, tab_b, (select store_id, sum(store_value*unit_sales) from sales_fact_1998 group by store_id)
as tab_virtuale_c
where tab_virtuale_c.store_id = tab_a.store_id …
La query esterna contiene al suo interno una query (la parte sottolineata e in corsivo) il cui risultato viene
usato come se fosse una tabella vera e propria e a cui si fa riferimento con il nome tab_virtuale_c nella
query esterna. In generale, in una query SQL dopo la parola chiave from possono essere riportate tabelle
reali oppure il risultato di una query (che in questo caso viene chiamato query annidata).
8. Determinate il ricavo totale suddiviso per “state” (attributo store.store_state) e mostrate gli stati in ordine
decrescente di ricavo (ogni “state” deve apparire una sola volta). Per ogni riga del risultato, visualizzate
anche il campo store_country oltre che il campo store_state.
9. Identificate i prodotti che hanno fatto guadagnare di più nel 1998 (visualizzate product_id, product_name, e
totale del guadagno conseguito nel 1998, visualizzate i prodotti in ordine decrescente).
10. Considerando le vendite della tabella sales_fact_1998, limitando la ricerca ai soli negozi di tipo
supermarket (store.store_type=’Supermarket’), visualizzate una lista di supermercati (ogni supermercato
deve apparire al massimo una sola volta) ordinata in base al rapporto (guadagno totale del supermercato) /
(qt totale di oggetti venduti dal supermercato).
Analisi varie.
11. Visualizza l’utile generato dalle diverse tipologie di clientela. Le tipologie di clienti sono identificate
dall’attributo customer.member_card. Nella tabella risultato ci dovrà essere un solo valore per ogni
tipologia di member_card.
12. In questo esercizio saranno analizzati i margini dei settori merceologici nei diversi supermercati.
L’esercizio è diviso in sottopunti.
a. Visualizzate per ogni coppia <supermercato, settore merceologico> il margine corrispondente (i
supermercati sono identificati dall’attributo store.store_id mentre i settori merceologici sono
identificati product_class.product_department). Tenete presente che il margine non è una grandezza
additiva (per calcolare il margine di un insieme di record di vendita non si possono sommare i
margini dei singoli record, ma occorre calcolare sia l’utile totale sia il ricavo totale dell’insieme dei
record considerati e infine effettuare la divisione). Facoltativo: nei risultati, accanto allo store_id,
visualizzate anche la tipologia del supermercato (attributo store.store_type).
b. Visualizzate per ogni coppia <tipologia supermercato, settore merceologico> il margine
corrispondente. Questa query deve calcolare il margine di un certo settore merceologico per tutti i
supermercati di una stessa tipologia. In questo sottopunto, i record di vendita (utilizzati per calcolare
il margine) vanno raggruppati diversamente rispetto al sottopunto precedente.
c. [NB: per svolgere questo punto è necessario utilizzare le query annidate] Usando le due query
precedenti come sottoquery, individuate quelle coppie di <supermercato, settore merceologico> per i
quali il margine è inferiore al 96% del margine calcolato su <tipologia supermercato, settore
merceologico> . Quest’ultimo è il margine del corrispondente settore merceologico calcolato su tutti
i supermercati della stessa tipologia. Per costruire la query dovete mettere in join i risultati delle
query del sottopunto a) e del sottopunto b). Visualizzare solamente i dati dei supermercati che hanno
un margine inferiore al 96% del margine dei supermercati della stessa categoria (quest’ultima
informazione è presente nei risultati della query del punto b).
13. L’esercizio è diviso in sottopunti
a. Visualizzate, per ogni product_id, le quantità vendute nel primo trimestre del 1998. Le informazioni
sul trimestre si trovano in time_by_day.quarter, il primo trimestre è ’Q1’, il secondo trimestre è ‘Q2’,
…). Nel risultato potete limitarvi a visualizzare il product_id, non serve il product_name. Per ogni
product_id deve essere visualizzata una sola riga nella tabella risultato.
b. Visualizzate, per ogni product_id, le quantità vendute in tutto il 1998. Nel risultato potete limitarvi a
visualizzare il product_id, non serve il product_name. Per ogni product_id deve essere visualizzata una
sola riga nella tabella risultato.
c. [NB: per svolgere questo punto è necessario utilizzare le query annidate] Usando le due query
precedenti come sottoquery, visualizzate, per ogni product_id, la quantità di beni venduta nel 1°
trimestre, la quantità di beni venduta in tutto l’anno, e il rapporto tra queste due quantità. Visualizzate i
risultati in ordine crescente rispetto a product_id. Nel risultato potete limitarvi a visualizzare il
product_id, non serve il product_name. Se usate SQLITE, moltiplicate per 1.0 il numeratore (in modo
da non ottenere un risultato solamente intero)
14. L’esercizio è diviso in sottopunti
a. Visualizzate, per ogni customer_id, il numero medio di quantità acquistate per transazione. Una
transazione corrisponde ad un singolo record della tabella sales_fact_1998. Nel risultato potete
limitarvi a visualizzare il customer_id, non servono i nomi e cognomi dei clienti. Per ogni customer_id
deve essere visualizzata una sola riga nella tabella risultato.
b. [NB: query annidate] Visualizzate, per ogni customer_id il numero di transazioni effettuate (cioè il n.
di record di sales_fact_1998) in cui il cliente ha acquistato un numero di beni superiore alla quantità
mediamente acquistata dal cliente nelle sue transazioni (in altre parole, ogni cliente avrà una media
diversa). Si suggerisce di calcolare in una sottoquery le quantità medie per transazione dei clienti.
Ordinate il risultato in ordine crescente rispetto al customer_id.
c. [NB: query annidate] Arricchite la query del punto precedente visualizzando anche, per ogni cliente, il
numero totale delle transazioni effettuate e il rapporto tra numero di transazioni in cui si è acquistata
una quantità superiore alla media e numero di transazioni totali. Per farlo, si suggerisce di aggiungere
alla query precedente una sottoquery che calcola, per ogni customer_id, il numero totale di transazioni
svolte. Ordinate il risultato in ordine crescente rispetto al customer_id.
