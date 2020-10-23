---
status: ALPHA
language: PL
title: "Obsługa technologii wykonania"
required-app: paanda, platformaERP
---

# Produkcja

## 0 Resources

- Produkcja https://github.com/kotynia/platforma-docs/tree/master/02-Produkcja


## 1 DB - Objects

### Tabele

- [wms].[commision]     - zlecenie produkcyjne
-	[wms].[commisionLine] - zlecenie produkcyjne pozycje
- [mrp].[requisition] -  wstepnie obliczone zapotrzebowanie materiałowe
  - uwzglednia zlecenia
  - uwzglednia strukture 
  - uwzgl
-	[wms].[technology], [wms].[technologyline]  - operacje technologiczne 
-	[wms].[technologyMade] - realizacja operacji
- [wms].[structure], [wms].[structureline]  - struktura materialowa indeksu materałwoego
- [


### Procedury

- [wms].[commision_calculateExpectedDates] - obliczanie spodziewanych czasów realizacji zleceni
- [mrp].[requisition_list] zapotrzebowanie
-	[wms].[technologyDashboard_List] - procedura

## 10 API - REST API
### 10.1 Pobranie pozycji i dokumentu

**Request**

```http

```

**Response**
