# Fusion Sort
Il **Fusion Sort** è un algoritmo di ordinamento sviluppato da **Piergiorgio Riva** nel 1994.  
Si basa su una serie di passate iterative dell’array, durante le quali vengono fusi due gruppi adiacenti.  
Nella prima passata ogni gruppo è composto da un solo elemento; nelle passate successive la dimensione dei gruppi raddoppia seguendo una progressione basata sulle potenze di due (1, 2, 4, 8, ...).  
L’algoritmo è stabile nell’implementazione originale e non utilizza ricorsione.

---

## Caratteristiche principali
- **Algoritmo di fusione iterativa**
- **Struttura non ricorsiva**
- **Fondamento matematico:** potenze di due
- **Stabilità:** garantita nell’implementazione originale
- **Fusioni cieche e complete:** l’algoritmo non analizza la struttura interna dei dati
- **Gestione automatica dei gruppi spaiati**

---

## Descrizione dell’algoritmo
Il Fusion Sort procede per passate successive dell’array:

1. L’array viene suddiviso in gruppi adiacenti di dimensione fissa.
2. Ogni coppia di gruppi viene fusa in un unico gruppo ordinato.
3. A ogni passata la dimensione dei gruppi raddoppia.
4. Se rimane un **gruppo spaiato**, esso viene copiato così com’è.
5. Nelle passate successive, quando il numero totale dei gruppi torna pari, il gruppo spaiato viene automaticamente integrato nella fusione.

L’algoritmo non sfrutta sequenze già ordinate, non rileva pattern locali e non adatta il proprio comportamento ai dati: ogni fusione è completa e obbligatoria.

---

## Complessità
- **Tempo:** `O(n log n)`  
  Ogni passata richiede un attraversamento lineare dell’array, e il numero di passate è proporzionale al logaritmo della dimensione.

- **Spazio:** `O(n)`  
  L’implementazione utilizza due array alternati: uno per la lettura e uno per la scrittura.

---

## Differenze rispetto al Merge Sort iterativo tradizionale
Il Fusion Sort differisce dal Merge Sort iterativo comune per diversi aspetti:

- Le fusioni sono **sempre complete**, anche se i gruppi sono già ordinati.
- I gruppi spaiati vengono **integrati automaticamente** nella passata successiva in cui il numero dei gruppi torna pari.
- La struttura dell’algoritmo è **esplicitamente fondata sulle potenze di due**.
- Il Fusion Sort **non è adattivo**: non sfrutta alcuna struttura interna dell’array.
- La stabilità è garantita dall’implementazione originale.

---

## Esempio di implementazione (C#)
```csharp

 void Sort_FusionSort(){
     ulong j, k, n, Indice1, LimInf1, Indice2, LimInf2, IndiceCopia;
     j = 1;
     while (true)
     {
         j <<= 1; IndiceCopia = 0;
         for (k = 1; k <= gNumElem-1; k += j)
         {
             Indice1 = k; Indice2 = k + j / 2; LimInf1 = Indice2 - 1; LimInf2 = k + j - 1;
             if (Indice2 > gNumElem-1)
             {
                 if (Indice1 == 1)
                 {
                     return;
                 }
                 else
                 {
                     for (n = Indice1; n <= gNumElem-1; n++)
                     {
                         IndiceCopia++; gArray[gCopia, IndiceCopia] = gArray[gMatrice, n];
                     }
                     break;
                 }                        
             }
             if (LimInf2 > gNumElem-1) LimInf2 =  gNumElem-1;
             while (true)
             {
                 IndiceCopia++;
                 if (gArray[gMatrice, Indice1] <= gArray[gMatrice, Indice2])
                 {
                     gArray[gCopia, IndiceCopia] = gArray[gMatrice, Indice1]; Indice1++;
                     if (Indice1 > LimInf1)
                     {
                         for (n = Indice2; n <= LimInf2; n++)
                         {
                             IndiceCopia++; gArray[gCopia, IndiceCopia] = gArray[gMatrice, n];
                         }
                         break;
                     }
                 }
                 else
                 {
                     gArray[gCopia, IndiceCopia] = gArray[gMatrice, Indice2]; Indice2++;
                     if (Indice2 > LimInf2)
                     {
                         for (n = Indice1; n <= LimInf1; n++)
                         {
                             IndiceCopia++; gArray[gCopia, IndiceCopia] = gArray[gMatrice, n];
                         }
                         break;
                     }
                 }
             }
         }
         gMatrice = 1 - gMatrice; gCopia = 1 - gCopia;
     }
 }
