---
target: "https://benwwtf.github.io/"
total_score: 16
max_score: 24
na_heuristics: 5,7,9,10
p0_count: 0
p1_count: 1
timestamp: 2026-09-15T11-02-04Z
slug: benwwtf-github-io
---
## Design Health Score

| # | Heuristic | Score | Key Issue |
|---|-----------|-------|-----------|
| 1 | Visibility of System Status | 3 | No aria-expanded on the Impressum trigger |
| 2 | Match System/Real World | 4 | Plain, human copy; correctly localized legal text |
| 3 | User Control and Freedom | 1 | Escape/click-outside confirmed not to reliably close the Impressum modal |
| 4 | Consistency and Standards | 2 | Hover shows nearly the same full modal as click |
| 5 | Error Prevention | n/a | No forms, no destructive actions |
| 6 | Recognition Rather Than Recall | 2 | Secondary link underlines invisible at rest/touch; unlabeled dead controls in tab order |
| 7 | Flexibility/Efficiency | n/a | Mode rule (Persuade/Experience) |
| 8 | Aesthetic/Minimalist | 4 | Clean markup, detector zero findings |
| 9 | Error Recovery | n/a | No errors possible on static page |
| 10 | Help/Documentation | n/a | Mode rule |
| Total | | 16/24 (67%) | Acceptable |

## Design Specificity Verdict
Authored, not templated. Oversized hero, lime shadow-rectangle motif, alternating pull-quote rhythm, prose CV with citations, Arnstein's-ladder reference, wry closing line. Detector: zero findings.

## Root cause
Impressum "show" CSS rule ORs :hover, :focus-within, and [data-open]. Escape/outside-click correctly clear data-open via JS but :hover/:focus-within can independently keep it visually open if pointer/focus remain on the trigger.

## Priority Issues
[P1] Impressum modal close behavior confirmed unreliable + keyboard-unreachable (no Enter/Space handling, no aria-expanded). Fix: make [data-open] sole CSS driver, add keydown handling, add aria-expanded. -> /impeccable harden
[P2] Two unlabeled dead focusable controls in portrait shadow DOM + guaranteed 404 for .image-slots.state.json (Design Canvas editing artifacts leaking into published page). -> /impeccable harden
[P2] Secondary link underlines (#E8E8E8) fail rest-state contrast, invisible on touch. -> /impeccable adapt
[P2] Alternating pull-quote rhythm nearly disappears on mobile (alignment stripped, font-size barely differs from body). -> /impeccable adapt
[P3] Dead/overridden absolute-position CSS on Impressum popup, cosmetic only. -> /impeccable polish

## Persona Red Flags
Sam (accessibility): cannot open Impressum via keyboard at all; no aria-expanded.
Casey (mobile): link affordances vanish, pull-quote rhythm flattens.
Riley (stress tester): confirmed Escape-doesn't-close behavior directly.

## Minor Observations
CV date labels are a nice consistent detail. Duplicate link text (Wubben/Vector Foundation x2) correct, not a bug. Image alt text via aria-label on image-slot is fine (photographer credit included) - would false-positive on an <img alt>-only checker. Untested: ~768-1024px tablet band.

## Questions to Consider
1. Does Impressum need a hover preview at all, or is click/tap-only simply right?
2. Should the pull-quote rhythm get a mobile-native treatment instead of inheriting the desktop pattern with alignment removed?
