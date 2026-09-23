# Solution Design

## 1. Problem

Support receives ~150 tickets/day. Agents may spend time solving a problem that was already solved, or give an answer that differs from a previous resolution.

The goal is to show relevant historical tickets and their resolutions when a new ticket arrives, so the human agent can make a faster and more consistent decision.

## 2. Assumptions

- The current application is built in **OutSystems ODC**.
- Ticket data is already in the OutSystems database.
- Available fields are:
  - `title`
  - `description`
  - `resolution_note`
  - `status`
  - `category`
  - `customer`
  - `created_at`
  - `closed_at`
- Current volume is ~150 tickets/day and may grow to **300 tickets/day**.
- A ticket is considered similar when its similarity score is **>= 80%**.
- Response-time targets are:
  - High: 4 hours
  - Medium: 8 hours
  - Low: 16 hours
- The system is an **agent-assist** feature. It does not automatically close tickets or send responses.

## 3. Proposed Architecture

```text
New Ticket
   |
   v
Similarity Search
   |
   +--> Filter by configurable history window
   |
   +--> Compare title + description
   |
   +--> Apply 80% similarity threshold
   |
   v
Top matching past tickets
   |
   v
Agent UI
   |
   +--> Past ticket
   +--> Resolution note
   +--> Similarity score
   +--> Category / status / dates
