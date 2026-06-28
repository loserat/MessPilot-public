# MessPilot System Overview

This document describes the current system shape in a public-friendly way. It intentionally avoids internal implementation notes and real customer data.

## Storage Model

Current beta storage is JSON/file based. A later database migration is planned.

```text
Browser
  |
  |  HTTP / JSON
  v
Express API
  |
  |  read/write
  v
storage/demoStore.json
  |
  +-- customers
  +-- locations
  +-- buildings
  +-- rooms
  +-- measurements
  +-- defects
```

Some editor state is still local to the browser while the workflows are being hardened.

```text
Browser localStorage
  |
  +-- active customer/location/building context
  +-- active protocol draft
  +-- distributor editor state
  +-- theme selection
```

Target direction:

```text
Browser
  |
  v
API
  |
  +-- PostgreSQL or SQLite
  +-- file storage for generated exports
  +-- audit and user/session tables
```

## Object Structure

MessPilot structures inspection data from customer to technical object.

```text
Customer
  |
  +-- Location
        |
        +-- Building
              |
              +-- Room
              |     |
              |     +-- Lighting measurements
              |
              +-- Distribution board
                    |
                    +-- Prefuse
                          |
                          +-- RCD group
                                |
                                +-- Circuit
                                      |
                                      +-- Cable data
                                      +-- Measurement values in protocol snapshots
```

## Protocol Workflow

All protocols use the same shell: assignment first, then type-specific steps.

```text
1  Assignment & standard
   |
2  Protocol base data
   |
3  Type-specific structure
   |
4  Inspection / test steps
   |
5  Measurement entry
   |
6  Evaluation
   |
7  Completion / export
```

For VDE-style distribution board protocols, the current workflow is:

```text
1  Zuordnung & Norm
   |
2  Grunddaten & Verteiler
   |
3  Stromkreise
   |
4  Besichtigen
   |
5  Erproben
   |
6  Messen
   |
7  Bewertung
   |
8  Abschluss
```

Important rule:

```text
Distribution board master data
  -> copied into protocol as circuit snapshot
  -> measurement values belong to the protocol
  -> later board edits do not overwrite existing protocol measurements
```

## Export Flow

```text
Protocol draft
  |
  +-- validate required fields
  |
  +-- build print model
  |
  +-- render PDF preview
  |
  +-- user confirms/downloads
```

PDF templates are still being refined. VDE-style protocols use a first page for header and inspection results, followed by landscape circuit tables.
