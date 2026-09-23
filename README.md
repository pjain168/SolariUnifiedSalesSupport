# SolariUnifiedSalesSupport
This a simple support app. When a new ticket comes in, shows past tickets to a human agent and how they were resolved


### `README.md`

```md
# README

## What this solution does

When a new support ticket arrives, the application finds similar resolved tickets and shows their resolution notes to the human agent.

The goal is to help agents:

- find previous solutions faster
- give more consistent answers
- avoid solving the same issue from scratch

## Current setup

- Platform: **OutSystems ODC**
- Data: OutSystems database
- Expected volume: **150–300 tickets/day**
- Default similarity threshold: **80%**

Ticket fields used:

- `title`
- `description`
- `resolution_note`
- `status`
- `category`
- `customer`
- `created_at`
- `closed_at`

## How to run

This is designed to run inside the existing OutSystems ODC application.

1. Load the sample ticket data into the OutSystems database.
2. Open/create a support ticket.
3. Run the similarity search for that ticket.
4. Display matching resolved tickets on the agent screen.
5. Select a historical ticket to view its resolution note.

Configuration should be exposed through an OutSystems configuration entity/screen.

Recommended defaults:

| Setting | Default |
|---|---:|
| Similarity threshold | 80% |
| History window | Configurable |
| Maximum matches shown | 5 |
| High priority target | 4 hours |
| Medium priority target | 8 hours |
| Low priority target | 16 hours |

## Gaps / Known limitations

- The initial approach is text-based and may not understand synonyms or deeper meaning.
- An 80% threshold needs to be validated against real support data.
- No automatic answer generation is included.
- No automatic ticket resolution is included.
- Performance needs to be tested as the historical ticket database grows.
- The exact history window has intentionally been left configurable rather than fixed.
- The solution does not currently learn from agent feedback.

## Future improvement

If text similarity produces too many false negatives, add an embedding/vector-search layer while keeping the same agent-facing experience and configuration.

The system should continue to show the original historical ticket and resolution so the agent can verify the recommendation.
