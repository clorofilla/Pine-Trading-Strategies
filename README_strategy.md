Codice Spiegazione/Esempi

Questo script è una strategia in Pine per TradingView che utilizza i frattali per prendere decisioni di trading. 

1. Informazioni sullo script
Lo script utilizza Pine Script versione 5

Definisce una strategia chiamata "Fractal strategy", che è sovrapposta al grafico. La dimensione predefinita della transazione è impostata al 10% del capitale.

2. Input
showPatterns: input casella di controllo per mostrare o nascondere i pattern frattali sul grafico.
showBarColors: input casella di controllo per mostrare o nascondere i colori delle barre.
filterBW: input casella di controllo per filtrare i frattali di Bill Williams.

3. Input di gestione del rischio
stopLossPercent: input per definire la percentuale di stop-loss (2% per impostazione predefinita).
takeProfitPercent: input per definire la percentuale di take-profit (4% per impostazione predefinita).

4. Costanti di riconoscimento frattale
UP: rappresenta un frattale verso l'alto.
DOWN: rappresenta un frattale verso il basso.

5. Funzioni di riconoscimento frattale
isRegularFractal(mode): determina se si è verificato un frattale regolare (non Bill Williams).
Per un frattale ascendente: controlla se il massimo di una barra specifica è più alto dei massimi delle due barre precedenti e delle due successive.
Per un frattale discendente: controlla se il minimo di una barra specifica è più basso dei minimi delle due barre precedenti e delle due successive.
isBWFractal(mode): determina se si è verificato un frattale Bill Williams.
Le condizioni sono simili al frattale regolare ma leggermente modificate in base alla definizione di Bill Williams.

6. Filtraggio frattale
filteredTopFractal e filteredBottomFractal: queste variabili memorizzano i frattali superiore e inferiore in base all'applicazione o meno del filtro di Bill Williams.

7. Tracciamento dei frattali
plotshape: traccia le forme sul grafico per indicare la posizione dei frattali rilevati.
Frattali superiori: tracciati sopra la barra utilizzando un triangolo verso il basso (rosso). Bottom Fractals: tracciati sotto la barra usando un triangolo verso l'alto (lime).

8. Logica di trading automatizzata
Le variabili topFractalPrice e bottomFractalPrice vengono utilizzate per memorizzare il prezzo dei frattali più recenti.
Se viene rilevato un bottom fractal, memorizza il prezzo basso in bottomFractalPrice.
Se viene rilevato un top fractal, memorizza il prezzo alto in topFractalPrice.
Se sono disponibili entrambi i prezzi dei frattali:
Posizione lunga (acquisto): l'ingresso viene effettuato al prezzo stop (basso), con un ordine limite impostato su basso * (1 - stopLossPercent).
Posizione corta (vendita): l'ingresso viene effettuato al prezzo stop (alto), con un ordine limite impostato su alto * (1 + stopLossPercent).
Le posizioni vengono chiuse utilizzando i livelli take-profit e stop-loss. 

9. Massimi più alti, massimi più bassi, minimi più alti, minimi più bassi
Questi sono input aggiuntivi per tracciare e tracciare massimi più alti, massimi più bassi, minimi più alti e minimi più bassi in base ai frattali.
higherHigh, lowerHigh, higherLow e lowerLow: condizioni booleane per verificare se il frattale rilevato è un massimo più alto, un massimo più basso, un minimo più alto o un minimo più basso.
Tracciamento: se abilitate, queste condizioni vengono tracciate sul grafico con le etichette [HH], [LH], [HL] e [LL].

10. Frattali da un intervallo di tempo più alto
Consente di mostrare i frattali da un intervallo di tempo più alto.
isTFFractal(mode, tf): verifica se il frattale nell'intervallo di tempo corrente corrisponde a uno da un intervallo di tempo più alto.
higherHighTF e lowerLowTF: utilizzati per identificare e tracciare massimi più alti e minimi più bassi dall'intervallo di tempo più alto. 11. Traccia canali in base ai frattali
showChannel1 e showChannel2: opzioni per tracciare canali in base ai frattali.
Canale 1: utilizza frattali superiori e inferiori per tracciare.
Canale 2: utilizza massimi più alti e minimi più bassi per tracciare.
Riepilogo
Questo script automatizza le decisioni di trading in base a modelli frattali e regole di gestione del rischio. Offre flessibilità tramite input utente per mostrare modelli frattali, massimi/minimi più alti e canali sul grafico. La strategia inserisce ordini di acquisto/vendita quando si verificano modelli frattali specifici e gestisce il rischio con ordini stop-loss e take-profit.

Scenario:
Abbiamo abilitato filterBW, quindi lo script utilizzerà la definizione frattale di Bill Williams.
Lo stop loss è impostato al 2% e il take profit è impostato al 4%. Stiamo anche visualizzando i massimi più alti/massimi più bassi e i minimi più alti/minimi più bassi.
Contesto di mercato:
Movimento recente dei prezzi:

Il titolo è in un leggero trend rialzista.
Un frattale di Bill Williams è stato rilevato tre barre fa.
Un frattale di Bill Williams è stato rilevato una barra fa.
Dati delle barre (esempio):

high[4] = $100
high[3] = $101
high[2] = $102 (frattale rilevato)
high[1] = $101
high[0] = $100
low[4] = $95
low[3] = $96
low[2] = $97 (frattale rilevato)
low[1] = $96
low[0] = $95

Come viene eseguito lo script:
Rilevamento dei frattali:

Lo script controlla i frattali.
Identifica un frattale di punta a $102 e un frattale di fondo a $97. Logica di trading:

Ordine di acquisto:
Poiché viene rilevato un frattale di fondo a $ 97, lo script prepara un ordine di acquisto.
Prezzo di stop di ingresso: $ 97.
Stop loss: 97 * (1 - 0,02) = $ 95,06.
Take profit: 97 * (1 + 0,04) = $ 100,88.
Ordine di vendita:
Poiché viene rilevato un frattale superiore a $ 102, lo script prepara un ordine di vendita.
Prezzo di stop di ingresso: $ 102.
Stop loss: 102 * (1 + 0,02) = $ 104,04.
Take profit: 102 * (1 - 0,04) = $ 97,92.

Con l'avanzare dell'azione del prezzo, se le condizioni corrispondono ai prezzi di stop o limite impostati dalla strategia, le negoziazioni verranno eseguite.
Se il prezzo raggiunge $ 97, verrà aperta una posizione lunga con i livelli di stop loss e take profit definiti.

Esempio di grafico:
Frattali: tracciati a $ 102 (in alto) e $ 97 (in basso).
Ordine di acquisto: piazzato a $ 97 con stop loss a $ 95,06 e take profit a $ 100,88.
Ordine di vendita: piazzato a $ 102 con stop loss a $ 104,04 e take profit a $ 97,92.

Risultati:
Se il prezzo scende a $ 97, viene attivato un ordine di acquisto. Se il prezzo sale a $ 100,88, la posizione viene chiusa con profitto. Se scende a $ 95,06, la posizione viene chiusa con perdita.
Se il prezzo sale a $ 102, viene attivato un ordine di vendita. Se il prezzo scende a $ 97,92, la posizione viene chiusa con profitto. Se sale a $ 104,04, la posizione viene chiusa con perdita.
Ecco come funzionerebbe il codice Pine Script fornito in uno scenario di trading reale, in base al rilevamento frattale e ai parametri della strategia configurati.


high[0]: si riferisce al prezzo alto della barra corrente (la barra più recente sul grafico).
high[1]: si riferisce al prezzo alto della barra precedente, che è la barra prima di quella corrente.
high[2]: si riferisce al prezzo alto della barra prima di quella a cui fa riferimento high[1], quindi due barre fa.
high[3]: si riferisce al prezzo alto della barra tre barre fa.
high[4]: si riferisce al prezzo alto della barra quattro barre fa. Esempio in una sequenza:
Supponiamo di guardare un grafico di 1 ora con i seguenti prezzi massimi per le ultime cinque barre:

Indice barra Ora Prezzo massimo
high[4] 9:00 $105
high[3] 10:00 $107
high[2] 11:00 $110
high[1] 12:00 $108
high[0] 13:00 $106
high[4] è $105 (dalla barra alle 9:00).
high[3] è $107 (dalla barra alle 10:00).
high[2] è $110 (dalla barra alle 11:00).
high[1] è $108 (dalla barra alle 12:00).
high[0] è $106 (dalla barra corrente alle 13:00).
Questi riferimenti consentono allo script di analizzare i dati passati e di prendere decisioni basate sui movimenti dei prezzi rispetto alle barre più recenti.

Copyright (c) the respective contributors, as shown by the AUTHORS file.

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
