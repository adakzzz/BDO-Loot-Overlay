# BDO Loot Overlay — Requirements

*Last updated: 28 Oct 2026*

## 1. Overview

**Problem statement** —There is no UI for loot collected during a grind session unless its specially in Marni Realm but most don't use it. To track you loot you have to open your inventory every time which is annoying

**Vision** — To be able to track the players loot whilst grinding and also show how much silver you have made during that time

**Why build it (not just use Garmoth)?** —Because I honestly like to play BDO and because this project can also be used to help me improve my skills as a cs student looking for a placement, its a win win.

## 2. Users and use cases

**Target user** — Any BDO mob grinders in general

1. As a grinder I want to be able to see my loot that I got in a box U
2. As a grinder I want to see the amount of silver I made during the grind session
3. As a grinder I want to review my session after to see what loot I got and compare to previous sessions

## 3. MVP functional requirements

| ID | Requirement | Priority |
| --- | --- | --- |
| FR-1 | Capture the chat/loot region of the screen at a set interval | Must |
| FR-2 | Extract item name and quantity from each loot line | Must |
| FR-3 | Avoid counting the same line twice | Must |
| FR-4 | Start/pause/stop a session | Must |
| FR-5 | Show totals in an overlay | Must |
| FR-6 | Save sessions for later review | Should |
| FR-7 | Silver/hour using market prices | Must |
| FR-8 | gui can you minimised or maximized(maximized will show item in column with its market price  ) | could |
| FR-9 | User selects the screen region to capture (the chat/loot box) | Must |

## 4. Non-functional requirements

| ID | Quality | Target |
| --- | --- | --- |
| NFR-1 | Accuracy — loot lines read correctly | ≥ 95% |
| NFR-2 | Latency — drop to overlay update | < 2 s |
| NFR-3 | Performance — CPU cost while gaming | < 5% CPU, no FPS drop |
| NFR-4 | Safety — never reads game memory, files or network; never sends input | Must hold always |
| NFR-5 | Reliability — session data survives a crash | a crash saves loses at most 1 minute of session data |
| NFR-6 | Platform | Windows 10/11, BDO borderless |

## 5. Out of scope

- Any automation of gameplay or input (ToS — permanent)
- Reading game memory, files or network traffic (ToS — permanent)
- Mobile app, multi-user accounts, Garmoth sync

## 6. Constraints and risks

| Risk | Likelihood | Impact | Mitigation |
| --- | --- | --- | --- |
| Anti-cheat flags the tool → account ban | Low | Severe | Develop offline on screenshots; ask Pearl Abyss support in writing before live use |
| OCR can't read BDO's font/background reliably | Medium | High | Spike first; tune chat tab background/font; try 2+ OCR engines |
| Game UI update breaks parsing | Medium | High | Keep all text-matching rules in one parser module; keep a folder of saved test screenshots and re-run them after every BDO patch, so a break is spotted in minutes and the fix only touches the parser |
| Limited time around uni | Medium | Low | Work 1 hour every day; if a week slips, move a Should feature to v2 rather than pushing the deadline |

**Constraints** — Time: 1 hour every day (~7 hours/week). Some days uni work or low motivation will cut into this, so the plan should survive a few missed days

Money: £0 — free OCR engines only (Windows' built-in OCR or Tesseract, both free); no paid cloud APIs

Deadline: What to get it done by December

Hardware: No constraint I running project on pc r7 9800x3D 32gbDDR5 5090

## 7. Success criteria

- [ ] All Must requirements implemented and tested
- [ ] Accuracy ≥ target on a labelled set of 50+ real screenshots
- [ ] Ran a full 1-hour grind session without crashing
- [ ] README lets a stranger install and run it in 10 minutes

## 8. Open questions

- [ ] Which language/stack? (Python is fastest to prototype; C#/.NET is native on Windows — decide after the spike)
- [ ] Will Pearl Abyss support confirm screen-reading is OK?
