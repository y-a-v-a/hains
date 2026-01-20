# Hains, the Curator Agent

The auto art curator agent. An autonomous agent that searches the web and assembles art exhibitions, questioning the role of the human curator.

## Concept

If curation is pattern-matching plus articulated reasoning, can an algorithm do it credibly? This agent performs curation earnestly—no irony, no winking. The cynicism emerges from the competence itself.

The output is a collection of artists/artworks with a curatorial statement. The real material is the decision-making made visible: what got selected, what got rejected, and why.

Relates to: Broodthaers' Musée d'Art Moderne, Département des Aigles; Siegelaub's catalog-as-exhibition; institutional critique as generative practice.

## How it works

1. Agent receives a seed (theme, starting artist, question) and a stopping condition
2. Searches the web, evaluates findings, decides what to search next
3. Logs every query, source, and verdict (selected/rejected with reasoning)
4. Commits selections to individual files
5. Synthesizes a final curatorial statement when done

## Project structure
```
/exhibition-{slug}/
  config.md              # seed + stopping condition
  search-log.md          # append-only decision ledger
  /collection/
    artist-name.md       # source, context, work, reason
  synthesis.md           # title, statement, final list
```

## config.md format
```markdown
# Exhibition Config

- **Seed:** [theme, starting point, or question]
- **Stopping condition:** [e.g., "5 artists" or "10 searches"]
```

## Usage

1. Create a new exhibition: `./new-exhibition <slug>`
2. Edit the generated `config.md` to set your seed and stopping condition
3. Run the curator: `cd exhibitions/exhibition-<slug> && ../../hains`
4. The hook system will remind the agent to update `search-log.md` after each search
5. Review `search-log.md` for the reasoning trail
6. Find the final exhibition in `synthesis.md`

## Hook System

The project includes a tool-use hook (`.claude/hooks.json`) that triggers after web searches. It reminds the agent to update `search-log.md` with:
- Query used
- Source URL examined
- Verdicts table (all artists encountered: SELECTED/REJECTED with reasoning)
- Next intended query

This ensures the decision-making process stays visible and complete.

## Note

The agent must trace every claim to a source URL. It cannot invent artists or works. Rejections are logged alongside selections—they define the edges of the curatorial concept.