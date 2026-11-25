# OCR til Excel

Et lite nettleserverktøy som gjør OCR giro-filer fra Nets om til én tabell. Du kan laste tabellen ned som Excel.

**Bruk:** Åpne siden, dra inn én eller flere OCR-filer, og klikk **Last ned Excel**.

Filene leses bare i nettleseren din. Ingenting lastes opp eller lagres noe sted.

## Hva verktøyet gjør

- Leser record 20 (start oppdrag), 30 og 31 (beløpspost 1 og 2) og 88 (slutt oppdrag).
- Lager én rad per betaling med disse kolonnene: oppgjørsdato, betalt til konto, betalt fra konto, KID, beløp, transaksjonstype, oppdragsdato, arkivreferanse og avtale-ID.
- Kontrollerer antall transaksjoner og sumbeløp mot record 88 i hver fil.
- Eksporterer til `.xlsx` med beløp som tall og datoer som datoer. KID og kontonumre lagres som tekst, så nullene foran beholdes.

## Feltposisjoner (1-basert, 80 tegn per record)

| Record | Posisjon | Felt |
|---|---|---|
| 20 | 9–17 | Avtale-ID |
| 20 | 25–35 | Oppdragskonto (mottaker) |
| 30 | 5–6 | Transaksjonstype |
| 30 | 9–15 | Transaksjonsnummer |
| 30 | 16–21 | Oppgjørsdato DDMMÅÅ |
| 30 | 32 | Fortegn |
| 30 | 33–49 | Beløp i øre |
| 30 | 50–74 | KID |
| 31 | 26–34 | Arkivreferanse |
| 31 | 42–47 | Oppdragsdato DDMMÅÅ |
| 31 | 48–58 | Debetkonto (betaler) |
| 88 | 9–16 | Antall transaksjoner |
| 88 | 25–41 | Sumbeløp i øre |

Excel-eksporten bruker [SheetJS](https://sheetjs.com/) (xlsx 0.18.5) fra cdnjs.
