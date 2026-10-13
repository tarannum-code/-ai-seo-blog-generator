## Quality Review: Study Nursing Abroad: What It Actually Pays Off in 2026

### Overall Score: 89/100 - Strong

| Category | Score | Max | Notes |
|----------|-------|-----|-------|
| Content Quality | 25 | 30 | Solid coverage and a genuinely differentiated "match your test-taking profile to the pathway" angle; several sentences/list items and one paragraph still exceed VOICE.md's length ceilings |
| SEO Optimization | 25 | 25 | Clean heading hierarchy, 8 unique internal anchors, 3 tier-1 external domains, accurate meta/title |
| E-E-A-T Signals | 10 | 15 | NCLEX sourcing is now fully consistent, but the Canada Express Entry CRS/vacancy figures are unsourced everywhere they appear |
| Technical Elements | 15 | 15 | FAQPage schema verified correct and matching, WebP hero confirmed genuine, wordCount verified in-tolerance; page speed/mobile marked N/A (no Gate 3 evidence) and denominator reweighted |
| AI Citation Readiness | 14 | 15 | Self-contained sections, TL;DR, table, ordered list; citability dinged slightly by the same unsourced Canada stat |

### Rating: 80-89 Strong

### Editorial Style Diagnostics
- Sentence-length variation: not formally computed; qualitatively high burstiness (short declaratives mixed with longer explanatory sentences) - descriptive only
- Configured style phrases: 0 taboo phrases found (no "game-changer," "dive in," "seamlessly," "cutting-edge," "delve," "navigate the landscape," etc.)
- Vocabulary diversity sample: not formally computed; domain terminology (NCLEX-RN, NMC, CRS, Express Entry, NNAS, NMBA) is used consistently throughout, no arbitrary term-swapping
- These observations do not infer authorship and do not affect the score.

### Independent Verification of Prior-Pass Claims

Verified directly against the files, not taken on trust:

1. **NCLEX sourcing consistency - CONFIRMED FIXED.** Grepped both files for "51%," "30% repeat," and "early 2026" - zero hits. The single 2025 NCSBN figure (47.3% international vs 86.7% US-educated) appears identically in Key Takeaways (md line 23), body prose (md line 73/119), the second SVG chart's `aria-label`/`<title>`/`<desc>`/`<figcaption>` (all four match), and the Sources list. No unsourced or inconsistent NCLEX number remains anywhere.
2. **FAQPage JSON-LD - CONFIRMED CORRECT.** The `@graph` array in the HTML `<script type="application/ld+json">` block contains one `BlogPosting` and one `FAQPage` with exactly 4 `Question`/`Answer` pairs, and the question text and answer text match the rendered `## Frequently Asked Questions` H3/paragraph pairs verbatim.
3. **Hero WebP - CONFIRMED GENUINE.** `file hero.webp` reports `RIFF ... Web/P image, VP8 encoding, 1200x630` (not a renamed JPEG). `hero.jpg` (60,250 bytes) and `hero.webp` (29,376 bytes) both exist at matching 1200x630 dimensions; frontmatter `coverImage`/`ogImage` and the rendered `<img src="hero.webp">`/`og:image`/`twitter:image` all reference the WebP.
4. **wordCount JSON-LD mismatch - CONFIRMED FIXED (within tolerance).** JSON-LD reports `wordCount: 2486`. Reproducing `blog_render.py`'s exact tag-stripping method against the rendered `<article>` (including header/byline/footer overhead the JSON-LD count excludes) yields 2556 - consistent with 2486 for body-only content. No drift bug detected.
5. **tags/keywords YAML-array parsing bug - CONFIRMED FIXED.** Read `scripts/blog_render.py` lines 274-305: `_parse_frontmatter` now special-cases a bracketed inline value (`value.startswith("[") and value.endswith("]")`) and splits/strips it into a real list before line 487 joins `fm.get("tags", [])` for the JSON-LD `keywords` field. The rendered `keywords` field reads `"study nursing abroad, nursing abroad, NCLEX-RN, nursing career, international nursing"`, correctly matching all 5 frontmatter tags with no bracket/quote artifacts.
6. **Test suite - CONFIRMED.** `python3 -m pytest tests/ -q` returns `313 passed, 1 skipped, 5 errors`. The 5 errors are all in `tests/test_google_search_behavior.py`, a pytest-fixture teardown `AssertionError` (`assert not self._finalizers`) unrelated to `blog_render.py` or this draft.
7. **Bold-text violations - CONFIRMED FIXED.** Only two `<strong>` tags remain in the rendered HTML: the "Key Takeaways" label (VOICE.md's required "Summary label") and the byline's "By [author]" chrome. Neither is body-copy bolding; the 13 prior violations are gone. No em dashes found anywhere.
8. **Blockquote/Sources rendering, duplicate hero, template tag - CONFIRMED FIXED.** Key Takeaways renders as a proper `<blockquote><ul><li>` list (not collapsed dash-paragraphs); the closing Sources section renders as a real `<ul><li><a>` list; only one hero `<img>` appears in the document; no literal `[UNIQUE INSIGHT]` or bracketed template placeholder exists anywhere in the markdown.

### New Issue Found (Not Caught in Passes 1 or 2)

While the NCLEX stat is now airtight, a parallel unsourced-statistic problem exists for a different figure: **Canada's Express Entry CRS score and nursing-vacancy numbers**. These appear five separate times with zero citation anywhere in the post and no matching source in the closing Sources list:

- Key Takeaways (md line 25): "CRS scores as low as 462-476... roughly 40-60 points below general draws, against over 60,000 projected nursing vacancies"
- Body, "Why Nursing Abroad Pays Off" (md line 36): "CRS cutoffs of 462-476... against a projected 60,000+ nursing vacancies through 2026"
- Body, "Why the UK Route Got Harder" (md line 102): "CRS scores 40-60 points below general draws"
- Destination table, Canada row (md line 112): "CRS 462-476 in 2026, 60,000+ vacancies"
- FAQ #3 (md line 151): "Canada's 2026 healthcare Express Entry draws are currently the most accessible PR route"

These are precise, publicly verifiable government statistics (IRCC Express Entry round-of-invitation data), exactly the kind of claim the earlier NCLEX fix correctly insisted must be sourced. Right now they read as authoritative but have no citation and no retrieval date, unlike every NCLEX/NMC/WHO figure in the piece. This is the same failure mode pass 2 flagged for the NCLEX stat, just on a different number that neither prior pass caught.

### Issues Found

#### Critical (must fix before publishing)
- **Unsourced numeric claims: Canada Express Entry CRS/vacancy figures (5 locations, listed above).** No citation, no retrieval date, no corresponding entry in the Sources list. Fix: add an IRCC/Government of Canada Express Entry source link (with retrieval date, matching the NCSBN/NMC citation pattern already used elsewhere in this post) or remove the specific numbers and reframe qualitatively if a citable source can't be confirmed. This meets editorial-heuristics.md heuristic 5's P0 bar ("multiple unsourced numeric claims").

#### High (should fix)
- VOICE.md's 25-word sentence ceiling is still exceeded in roughly 6-9 places after the trim pass, including: "Nurses who treat these as one connected sequence..." (33 words, md line 137), the three destination-fit bullets under "A few patterns worth acting on" (29-34 words each, md lines 121-123), "It verifies your existing qualification and clinical hours..." (26 words, md line 94), and the closing "Explore Jusst Nursing's destination pages..." sentence (28 words, md line 161). The claim that "several of the longest" were trimmed is accurate but incomplete - re-run a full sentence-length pass.
- The Conclusion's opening paragraph (md line 159) is 108 words, over VOICE.md's 100-word paragraph ceiling.

#### Medium (recommended)
- The "6.2 million (2020)" figure (md line 40, Key Takeaways is not affected, only body) is cited to the same WHO State of the World's Nursing 2025 URL used for the 2023/2030 figures. If the 2020 baseline actually originates in a different WHO report edition, cite that edition specifically; if it's genuinely restated in the 2025 report, a short parenthetical ("as cited in the 2025 report") would remove any doubt, matching the precision already applied to the NCLEX and NMC citations.
- No table of contents / in-page jump links on a ~2,500-word post (editorial-heuristics.md heuristic 3 recommends a TOC over 1,500 words). Heading `id` attributes already exist in the rendered HTML, so a TOC would be low-effort to add.
- Author attribution is a named team/brand ("Jusst Nursing Counselling Team") rather than a named individual with credentials. Acceptable under BRAND.md's positioning, but it caps the E-E-A-T author-attribution subscore versus a named counsellor with a stated credential.

#### Low (nice to have)
- None beyond the above; the piece is otherwise clean and well-structured.

### Prioritized Fix List
1. Source the Canada Express Entry CRS/vacancy figures (or remove/soften them) - this is the single remaining P0 and the only thing separating this draft from a clean pass.
2. Re-run a sentence-length pass against VOICE.md's 25-word ceiling; a handful of sentences and list items still exceed it.
3. Trim the 108-word Conclusion opening paragraph to VOICE.md's 100-word ceiling.
4. Optional: tighten the 2020 WHO citation precision and consider a lightweight TOC given the post's length.

Nonce: 3b9675a736ca7959fd7bea17f23e2304
BLOCKING: true (89/100, below the 90 threshold, and one P0 remains: Canada Express Entry CRS/vacancy figures are unsourced in 5 locations with no matching Sources entry, meeting editorial-heuristics.md heuristic 5's fabricated/unsourced-stat P0 bar)
