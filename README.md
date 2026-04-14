# AP1 Lernkarten – Datensatz v1.9.8

Offizielles Daten-Backup für die **Learning Factory AP1 Glossar App**.  
Dieses Repository enthält den vollständigen, validierten Lernkarten-Datensatz als maschinenlesbare Quelldaten — bereit für Notion-Import, App-Deployment und Weiterverarbeitung.

**Live-App:** [iwilfried.github.io/ap1-glossar](https://iwilfried.github.io/ap1-glossar/)  
**App-Repo:** [github.com/iwilfried/ap1-glossar](https://github.com/iwilfried/ap1-glossar)  
© 2026 Learning Factory

---

## Dateiübersicht

```
ap1-lernkarten-data/
├── README.md
├── json/
│   └── lernkarten.json          ← Quelldatei (440 Karten, vollständiges Schema)
└── csv/
    ├── 01_pruefungen.csv        ← 1 Zeile: IHK AP1
    ├── 02_module.csv            ← 5 Module (Sets)
    ├── 03_topics.csv            ← 27 Topics
    ├── 04_subtopics.csv         ← 401 Subtopics
    └── 05_lernkarten.csv        ← 440 Lernkarten (vollständig, mit Relations-IDs)
```

---

## Datensatz-Statistik

| Kennzahl | Wert |
|---|---|
| **Gesamtkarten** | 440 |
| **Davon manuell geprüft** | 54 (Original-Set) |
| **Davon auto-generiert** | 386 (IHK-Erwartungshorizonte) |
| **Module (Sets)** | 5 |
| **Topics** | 27 |
| **Subtopics** | 401 |
| **Unique Hashtags** | 817 |
| **Ø Tags pro Karte** | 4,5 |
| **Konsolidierungsregeln** | 25 (v1.9.7 + v1.9.8) |

### Kartentypen

| Typ | Anzahl |
|---|---|
| Begriff | 213 |
| Aufzählung | 170 |
| Berechnung | 39 |
| Vergleich | 18 |

### Schwierigkeitsgrade

| Grad | Anzahl |
|---|---|
| Leicht | 116 |
| Mittel | 241 |
| Schwer | 83 |

### Module (Sets)

| Modul | Karten |
|---|---|
| Fachbegriffe AP1 | 346 |
| WiSo | 35 |
| Bewertungsaspekte | 34 |
| Hardware-Berechnungen | 20 |
| Berechnungen | 5 |

---

## JSON-Schema (lernkarten.json)

Jede Karte ist ein JSON-Objekt mit folgenden Feldern:

```json
{
  "id": "uuid-v4",
  "question": "Frage im IHK-Prüfungsstil",
  "shortAnswer": "Kompakte Antwort (IHK-Erwartungshorizont, ~15–50 Wörter)",
  "longAnswer": "Ausführliche Antwort mit Prüfungshinweis und ggf. Rechenbeispiel",
  "bewertungsaspekt": "Funktional | Ökonomisch | Ökologisch | Sozial | Berechnung",
  "kartentyp": "Begriff | Aufzählung | Berechnung | Vergleich",
  "schwierigkeitsgrad": "Leicht | Mittel | Schwer",
  "set": "Fachbegriffe AP1 | WiSo | Bewertungsaspekte | Hardware-Berechnungen | Berechnungen",
  "topic": "z.B. Netzwerk | IT-Sicherheit | Datenschutz | ...",
  "subtopic": "z.B. IPv4-Subnetting | DSGVO Art. 5 | ...",
  "hashtags": ["#AP1", "#Netzwerk", "#IPv4", "..."],
  "url": "https://..."
}
```

### Pflicht-Tags (auf jeder Karte)
- `#AP1` — auf allen 440 Karten
- `#Funktional | #Ökonomisch | #Ökologisch | #Sozial | #Berechnung` — Bewertungsaspekt

---

## CSV-Struktur (Notion-Import)

Die 5 CSVs bilden eine vollständige relationale Hierarchie:

```
IHK AP1 (Prüfung)
  └── Fachbegriffe AP1 (Modul)
        └── Netzwerk (Topic)
              └── IPv4-Subnetting (Subtopic)
                    └── Lernkarte: "Was ist eine Subnetzmaske?" (Karte)
```

**Import-Reihenfolge in Notion** (Relations funktionieren nur in dieser Reihenfolge):

1. `01_pruefungen.csv` → Notion-Datenbank "Prüfungen"
2. `02_module.csv` → Notion-Datenbank "Module" (Relation: `Prüfung ID`)
3. `03_topics.csv` → Notion-Datenbank "Topics" (Relation: `Modul ID`)
4. `04_subtopics.csv` → Notion-Datenbank "Subtopics" (Relation: `Topic ID`)
5. `05_lernkarten.csv` → Notion-Datenbank "Lernkarten" (Relation: `Subtopic ID`)

Jede CSV enthält die vollständige ID-Kette (`Prüfung ID`, `Modul ID`, `Topic ID`, `Subtopic ID`) für einfache Verknüpfung.

---

## Hashtag-Taxonomie

25 Konsolidierungsregeln eliminieren Synonyme und vereinheitlichen Tags:

| Regel | Alt | → Canonical |
|---|---|---|
| 1 | `#AI` | `#KI` |
| 2 | `#GDPR` | `#DSGVO` |
| 3 | `#2FA` | `#MFA` |
| 4 | `#Authentifizierung` | `#MFA` |
| 5 | `#SSL` | `#TLS` |
| 6 | `#K8s` | `#Kubernetes` |
| 7 | `#VM` | `#Virtualisierung` |
| 8 | `#MachineLearning` | `#ML` |
| 9 | `#Datensicherung` | `#Backup` |
| 10 | `#RAID5` | `#RAID` |
| 11 | `#OOP` | `#Objektorientierung` |
| 12 | `#REST` | `#API` |
| 13 | `#ÖkologischeAspekte` | `#Ökologisch` |
| 14 | `#SozialeAspekte` | `#Sozial` |
| 15 | `#ÖkonomischeAspekte` | `#Ökonomisch` |
| 16 | `#Beschaffung` | `#Einkauf` |
| 17 | `#ISMS` | `#ITSM` |
| 18 | `#AD` | `#ActiveDirectory` |
| 19 | `#Schichtenmodell` | `#OSI` |
| 20 | `#RAID0` | `#RAID` |
| 21 | `#RAID1` | `#RAID` |
| 22 | `#RAID10` | `#RAID` |
| 23 | `#SELECT` | `#SQL` |
| 24 | `#WHERE` | `#SQL` |
| 25 | `#ifconfig` | `#ipconfig` |

---

## Versionshistorie

| Version | Datum | Highlight |
|---|---|---|
| v1.8.1 | 2026-03 | 54 Original-Lernkarten als JSON-Datenquelle |
| v1.9.3 | 2026-04 | 386 auto-generierte Karten (440 total) |
| v1.9.4 | 2026-04 | 20 schwächste shortAnswers → IHK-Horizonte |
| v1.9.5 | 2026-04 | 20 schwächste longAnswers → IHK-Horizonte |
| v1.9.6 | 2026-04 | Topic-spezifische Hashtags (Ø 4,5 Tags/Karte) |
| v1.9.7 | 2026-04-14 | Tag-Konsolidierung Regeln 1–17 (840→825 Tags) |
| **v1.9.8** | **2026-04-14** | **Tag-Konsolidierung Regeln 18–25 (825→817 Tags), vollständig validiert** |

---

## Lizenz

Datensatz erstellt und gepflegt von [Learning Factory](https://learningfactory.io).  
Inhalte orientieren sich am IHK-Prüfungsstil für IT-Berufe (AP1).  
© 2026 Learning Factory — Alle Rechte vorbehalten.
