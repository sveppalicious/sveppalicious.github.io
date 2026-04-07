# Ornithology Quiz Question Generator

## Your Task

You are generating a bank of multiple-choice quiz questions from an Ornithology study guide. The source material is a Markdown file (`Orders.md`) that describes ~44 bird orders organized by phylogenetic clade. Each order entry contains structured fields: Distribution, Habitats, Recognition, Feeding ecology, Breeding behavior, Feet type, Chick development, Fun Facts, and Specimens.

Your output is a single JSON file (`questions.json`) that a quiz app will consume.

---

## Source Material Rules

**Use these sections** for generating questions:
- Distribution
- Habitats
- Recognition
- Feeding ecology
- Breeding behavior
- Feet
- Chick development
- Fun Facts
- Specimens (species names and order membership)
- Clade descriptions (the blockquote sections describing Palaeognathae, Neognathae, Galloanserae, Neoaves, and all named subclades like Strisores, Telluraves, Afroaves, Australaves, etc.)

**Do NOT use these sections:**
- `> [!Source]- Handbook of Bird Biology` — skip these entirely
- Any etymology-related content

---

## Question Categories

Generate questions across these categories. Aim for a balanced spread — not every category applies to every order, so use judgment.

### 1. `identification`
Given a set of morphological or behavioral traits, identify the correct order.
- *"Which order is characterized by hair-like plumage, vestigial wings, and a bill with nostrils at the tip?"*

### 2. `traits`
Given an order name, identify the correct trait (recognition feature, synapomorphy, or other distinguishing characteristic).
- *"What is a synapomorphy of Apterygiformes?"*

### 3. `distribution`
Match an order to its geographic range, or vice versa.
- *"Which of these orders is endemic to Madagascar?"*

### 4. `feeding`
Match feeding ecology or diet to the correct order.
- *"Which order is the only nocturnal frugivore among birds?"*

### 5. `breeding`
Questions about breeding systems, nesting, courtship, or parental care.
- *"In which order do females seal themselves inside tree cavities during nesting?"*

### 6. `feet`
Identify the foot type for a given order, or which order has a particular foot type.
- *"What foot type do Trogoniformes have?"*

### 7. `development`
Whether chicks are precocial, altricial, semiprecocial, or semialtricial.
- *"Which of these orders has semiprecocial chicks?"*

### 8. `phylogeny`
Clade membership, sister-group relationships, higher-level groupings.
- *"Which of these orders belongs to Strisores?"*
- *"Flamingos and grebes are united in which clade?"*

### 9. `fun_facts`
Distinctive, memorable facts from the Fun Facts sections.
- *"Which bird order lost a war against Australia in 1932?"*

### 10. `specimens`
Given a scientific or common name, identify the order it belongs to — **only when the placement is non-obvious** (e.g., falcons in Australaves rather than with hawks, or hoatzin in its own order).
- *"To which order does Falco peregrinus belong?"* ✓ (non-obvious — falcons aren't hawks)
- *"To which order does Aquila chrysaetos belong?"* ✗ (obvious — eagles are clearly Accipitriformes)

---

## Question Volume

Aim for **5–8 questions per order**, spread across applicable categories. For orders with particularly rich content (e.g., Charadriiformes, Accipitriformes, Passeriformes), you can go up to 10. For sparse orders (e.g., Opisthocomiformes, Steatornithiformes), 4–5 is fine.

Target total: **~220–260 questions**, including ~10% multiple-choice (`"multiple": true`).

**Current gaps to prioritize** (as of April 2026):
- Topics thin on questions: Elementaves — Phaethontimorphae, Galloanserae, Mirandornithes
- Categories underrepresented across all topics: `development`, `specimens`
- Multiple-choice (`"multiple": true`): 0 currently — need ~20–25

---

## Distractor Guidelines

Good distractors are essential — they should be **plausible but wrong**. Follow these principles:

1. **Draw distractors from related or superficially similar orders.** A question about foot types should use other real foot types as distractors. A question about a nocturnal order should include other nocturnal or crepuscular orders.

2. **Avoid obviously absurd options.** Every option should look reasonable to someone who hasn't fully memorized the material.

3. **For phylogeny questions**, use orders from different clades as distractors — the point is testing whether the student knows the groupings.

4. **For specimen questions**, use species from other orders that might be confusable (e.g., other raptors, other seabirds).

5. **Vary the position of the correct answer** — don't always put it first or last.

6. **Most questions should have exactly 1 correct answer.** A meaningful minority (~10% of total) should have multiple correct answers where genuinely appropriate (e.g., "Which of these orders produce crop milk? Select all that apply." — both Columbiformes and Phoenicopteriformes). Flag these with `"multiple": true`.

---

## Multiple-Choice Questions (`"multiple": true`)

The quiz UI shows **"Select N answers."** where N is derived from the number of options marked `"correct": true`. This means:

- You **must** mark exactly 2–4 options as `"correct": true` for every `multiple: true` question
- Never use `"multiple": true` with only 1 correct option — that's just a standard question mislabeled
- The scoring is all-or-nothing: the student must select the exact correct set to get the point
- Use 5 options total when there are 2 correct (so there are still 3 distractors); 5–6 options when there are 3 correct

**Good multiple-choice patterns:**
- "Which of these orders have [shared trait]? Select all that apply." (2–3 orders share it)
- "Which of the following statements about [clade] are true? Select 2." (2 true, 2–3 false)
- "Which orders belong to [subclade]?" (testing clade membership knowledge)

---

## Do's and Don'ts

### Do's
- **Base every question strictly on content in Orders.md.** If the fact isn't explicitly stated there, don't write the question.
- **Make distractors from the same ecological guild or clade.** For a shorebird feeding question, use other wading bird diets; for a nocturnal order, use other low-light foragers.
- **Write explanations that teach.** Don't just restate the correct answer — explain *why* it's right and, when space allows, why the most tempting wrong answer is wrong.
- **For `multiple: true`, ensure ALL marked-correct options are genuinely correct** per Orders.md. A single wrong "correct" option ruins the question.
- **Use `related_orders`** to list every order actually discussed in the question text or explanation.
- **Vary difficulty roughly 40/40/20** (easy/medium/hard) within each topic.
- **Cross-clade comparison questions** are valuable — "Which of these orders shares X trait?" spans multiple topics and makes for great medium/hard questions.

### Don'ts
- **Don't write trivial order-identification questions** ("What order does [common species] belong to?") unless the placement is surprising. An eagle being Accipitriformes is obvious; a falcon being Australaves (not Accipitriformes) is worth testing.
- **Don't set `"multiple": true` if only 1 option is correct.** Use `"multiple": false` instead.
- **Don't use vague hedging in correct answers** ("sometimes", "often", "can", "may"). Correct answers should be unambiguous facts, not tendencies.
- **Don't invent or extrapolate facts.** If Orders.md says "can reach 80 km/h", don't write "fastest bird in the world" unless that's also stated.
- **Don't write questions where the answer is given away by the question wording** ("The unique folivorous diet of which order...?" telegraphs hoatzin).
- **Don't use "All of the above" or "None of the above"** as options.
- **Don't repeat nearly-identical questions within the same topic.** Two questions both testing zygodactyl feet in parrots add no value — vary the angle (one on foot type, one on how they use their feet for climbing).
- **Don't make `specimens` questions trivial** — only ask if the order assignment is non-obvious or tests a specific interesting fact from the Specimens section.

---

## Output Format

Output a single JSON file with this structure:

```json
{
  "metadata": {
    "generated": "YYYY-MM-DD",
    "source": "Orders.md",
    "categories": ["identification", "traits", "distribution", "feeding", "breeding", "feet", "development", "phylogeny", "fun_facts", "specimens"]
  },
  "questions": [
    {
      "id": "q001",
      "question": "Which order is characterized by didactyl, hoof-like feet?",
      "options": [
        { "text": "Struthioniformes", "correct": true },
        { "text": "Rheiformes", "correct": false },
        { "text": "Casuariiformes", "correct": false },
        { "text": "Apterygiformes", "correct": false }
      ],
      "explanation": "Ostriches (Struthioniformes) are the only birds with didactyl (two-toed) feet, which are hoof-like — a unique synapomorphy of the order.",
      "category": "traits",
      "difficulty": "easy",
      "topic": "Palaeognathae",
      "related_orders": ["Struthioniformes"],
      "multiple": false
    }
  ]
}
```

### Field Definitions

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Sequential ID: `q001`, `q002`, ... Continue from the highest existing ID in questions.json. |
| `question` | string | The question text. Clear, unambiguous, exam-style. |
| `options` | array | 4 options (5 for multi-correct). Each has `text` (string) and `correct` (boolean). |
| `explanation` | string | 1–3 sentences explaining *why* the correct answer is right and, if useful, why a common distractor is wrong. This is the learning tool. |
| `category` | string | One of the 10 categories listed above. |
| `difficulty` | string | `"easy"`, `"medium"`, or `"hard"`. See definitions below. |
| `topic` | string | The broadest relevant clade grouping for filtering. Use exactly one of: `"Palaeognathae"`, `"Galloanserae"`, `"Mirandornithes"`, `"Columbaves"`, `"Elementaves — Cursorimorphae"`, `"Elementaves — Strisores"`, `"Elementaves — Phaethontimorphae"`, `"Elementaves — Aequinornithia"`, `"Telluraves — Afroaves"`, `"Telluraves — Australaves"`. |
| `related_orders` | array | The order(s) the question is primarily about. |
| `multiple` | boolean | `true` if more than one option is correct. Default `false`. |

### Difficulty Definitions

- **Easy**: Direct recall of a single fact from one field. ("What foot type do parrots have?" → Zygodactyl)
- **Medium**: Requires connecting two pieces of information, or distinguishing between similar orders. ("Which paleognath can fly?" → Tinamiformes)
- **Hard**: Requires knowledge of phylogenetic relationships, subtle distinctions, or integrating multiple facts. ("Which of these clades is supported by morphological synapomorphies rather than only genomic data?" → Mirandornithes)

Aim for roughly **40% easy, 40% medium, 20% hard**.

---

## Process

Work through the source material **clade by clade**, in the order it appears in the document:

1. Palaeognathae (Struthioniformes through Casuariiformes) → topic: `"Palaeognathae"`
2. Galloanserae (Anseriformes, Galliformes) → topic: `"Galloanserae"`
3. Mirandornithes (Phoenicopteriformes, Podicipediformes) → topic: `"Mirandornithes"`
4. Columbaves (Columbiformes through Cuculiformes) → topic: `"Columbaves"`
5. Elementaves — Cursorimorphae (Opisthocomiformes, Gruiformes, Charadriiformes) → topic: `"Elementaves — Cursorimorphae"`
6. Elementaves — Strisores (Caprimulgiformes through Apodiformes) → topic: `"Elementaves — Strisores"`
7. Elementaves — Phaethontimorphae (Phaethontiformes, Eurypygiformes) → topic: `"Elementaves — Phaethontimorphae"`
8. Elementaves — Aequinornithia (Gaviiformes through Pelecaniformes) → topic: `"Elementaves — Aequinornithia"`
9. Telluraves — Afroaves (Accipitriformes through Coraciiformes) → topic: `"Telluraves — Afroaves"`
10. Telluraves — Australaves (Cariamiformes through Passeriformes) → topic: `"Telluraves — Australaves"`

For each clade, also generate 1–3 questions about the **clade itself** (what it contains, what unites it, how many species, etc.) — these go in the `phylogeny` category.

After completing all clades, do a final pass to add **cross-cutting comparison questions** that span multiple clades (e.g., "Which of these orders produce crop milk?" — both Columbiformes and Phoenicopteriformes). These make excellent multiple-choice candidates.

---

## Quality Checklist

Before finalizing, verify:

- [ ] Every order in the source has at least 4 questions
- [ ] All 10 categories are well-represented
- [ ] Difficulty distribution is approximately 40/40/20
- [ ] No question draws on Handbook of Bird Biology or etymology content
- [ ] Explanations are informative and accurate
- [ ] Distractors are plausible, not joke answers
- [ ] Correct answer position varies across questions
- [ ] `topic` field consistently uses the exact clade names listed in the Field Definitions table above
- [ ] Multi-correct questions are flagged with `"multiple": true` and have 2–4 correct options (never 1)
- [ ] JSON is valid and parseable
- [ ] No question gives away the answer in its own wording
- [ ] No near-duplicate questions within the same topic
