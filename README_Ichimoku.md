Spiegazione del codice

Questo codice Pine è un'implementazione della strategia Ichimoku Cloud, inclusi gli avvisi per potenziali segnali di acquisto e vendita in base a determinate condizioni. 

1. Parametri di input:
conversionPeriods: periodo per la linea di conversione (predefinito 9).
basePeriods: periodo per la linea di base (predefinito 26).
laggingSpan2Periods: periodo per lo Span 2 in ritardo (predefinito 52).
displacement: spostamento per lo Span A e lo Span B (predefinito 26).

2. Funzione canale Donchian:
donchian(len): calcola la media dei prezzi più alti e più bassi in un dato periodo (len).

3. Componenti Ichimoku:
Linea di conversione (Tenkan-sen): una linea di tendenza a breve termine calcolata utilizzando la funzione Donchian con conversionPeriods. Base Line (Kijun-sen): una linea di tendenza a medio termine calcolata utilizzando la funzione Donchian con basePeriods.
Span A (Senkou Span A): la media della Conversion Line e della Base Line, tracciata con un offset in avanti (spostamento).
Span B (Senkou Span B): una linea di tendenza a lungo termine calcolata utilizzando la funzione Donchian con laggingSpan2Periods, tracciata anche con un offset in avanti (spostamento).
Lagging Span (Chikou Span): il prezzo di chiusura corrente tracciato all'indietro tramite periodi di spostamento.

4. Tracciamento:
lo script traccia la Conversion Line, la Base Line, Span A, Span B e Lagging Span sul grafico.
l'area tra Span A e Span B è colorata (verde se Span A > Span B, altrimenti rosso).

5. Regole di trading:
Incrocio tra Conversion Line e Base Line:

ConvBaseBuy: un incrocio della Conversion Line sopra la Base Line, che indica un potenziale segnale di acquisto. ConvBaseSell: un crossunder della Conversion Line sotto la Base Line, che indica un potenziale segnale di vendita.
Kumo Cloud Rule:

Ideal Buy (idealbuy): un set di condizioni in cui il prezzo è sopra la cloud e la Conversion Line è sopra la Base Line, che indica un forte segnale di acquisto.

Ideal Sell (idealsell): un set di condizioni in cui il prezzo è sotto la cloud e la Conversion Line è sotto la Base Line, che indica un forte segnale di vendita.

Memory (buymem e sellmem): variabili booleane che ricordano il precedente segnale di acquisto o vendita per evitare segnali ripetuti.

Final Buy (longCond): innesca un segnale di acquisto quando si verifica una condizione di acquisto ideale e non c'era un segnale di acquisto sulla barra precedente.

Final Sell (shortCond): innesca un segnale di vendita quando si verifica una condizione di vendita ideale e non c'era un segnale di vendita sulla barra precedente.


Cloud Crossover:

buycloud: un crossover di Span A sopra Span B, con condizioni aggiuntive sul prezzo, che indica un segnale di acquisto. 

sellcloud: un crossunder di Span A sotto Span B, con condizioni aggiuntive sul prezzo, che indica un segnale di vendita.

6. Avvisi:
Lo script crea avvisi per le varie condizioni di acquisto e vendita, con messaggi personalizzati.
Scenario di esempio:
Supponiamo di analizzare un grafico giornaliero di un titolo:

Impostazione di Ichimoku Cloud:

Conversion Line = media di 9 giorni di prezzi alti e bassi.
Base Line = media di 26 giorni di prezzi alti e bassi.
Span A = media di Conversion Line e Base Line, tracciata 26 giorni prima.
Span B = media di 52 giorni di prezzi alti e bassi, tracciata 26 giorni prima.
Lagging Span = prezzo di chiusura corrente, tracciata 26 giorni prima.

Condizioni di mercato:

Il titolo è stato in un trend rialzista.
La Conversion Line attraversa sopra la Base Line, generando un segnale ConvBaseBuy. 

Generazione del segnale:

Il longCond viene attivato perché il prezzo è sopra la nuvola e la linea di conversione è sopra la linea di base.
Viene generato un avviso con il messaggio "Acquistalo come una lumaca".
Rappresentazione visiva:

Sul grafico, sono tracciati la linea di conversione, la linea di base, Span A e Span B.
E' riempita di verde (indicando condizioni rialziste).
Un triangolo che punta verso l'alto è tracciato sotto la barra in cui è soddisfatta la condizione di acquisto (longCond), segnalando un potenziale punto di ingresso.
Incrocio della nuvola:

Se Span A incrocia sopra Span B con condizioni di prezzo soddisfatte, viene generato un altro segnale di acquisto (buycloud), con il messaggio "Sono Goku".
Conclusione:

La strategia avvisa i trader di potenziali opportunità di acquisto/vendita in base ai principi di Ichimoku Cloud e ai filtri personalizzati, consentendo loro di prendere decisioni informate.
Questa configurazione consente un'analisi completa delle tendenze di mercato utilizzando Ichimoku Cloud, aiutando a identificare potenziali punti con avvisi.

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
