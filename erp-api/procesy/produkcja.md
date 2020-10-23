---
language: PL
title: "Obsługa produkcji"
required-app: paanda, platformaERP
---

# Produkcja

## 0 Resources

- Produkcja https://github.com/kotynia/platforma-docs/tree/master/02-Produkcja


## 1 DB - Objects

### Tabele

- [wms].[commision] , [wms].[commisionLine]   - zlecenie produkcyjne i pozycje
- [mrp].[requisition] -  wstepnie obliczone zapotrzebowanie materiałowe
  - uwzglednia zlecenia
  - uwzglednia strukture 
-	[wms].[technology], [wms].[technologyline]  - operacje technologiczne 
-	[wms].[technologyMade] - realizacja operacji
- [wms].[structure], [wms].[structureline]  - struktura materialowa indeksu 

### Procedury

- [wms].[commision_calculateExpectedDates] - obliczanie spodziewanych czasów realizacji zleceni
- [mrp].[requisition_list] zapotrzebowanie
-	[wms].[technologyDashboard_List] - procedura panel

## 10 API - REST API
### 10.1 Pobranie pozycji i dokumentu

**Request**

```http

```

**Response**
