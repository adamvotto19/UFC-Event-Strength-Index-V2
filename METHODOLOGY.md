# UFC Event Strength Index V2 — Methodology

## 1. Objective

The UFC Event Strength Index is designed to quantify the strength of a UFC event using information available **entering the event**.

The goal is not to determine whether an event ultimately produced entertaining fights. Instead, the model evaluates the quality, experience, ranking strength, star experience, main-event strength, and available fanfare surrounding the card before the fights occurred.

Each UFC event receives a score on a **0–100 scale**.

The current V2 dataset contains **788 UFC events from March 11, 1994 through September 19, 2026**.

---

## 2. Core Modeling Rule: No Future Leakage

The most important methodological rule is that fighter statistics are calculated using only information available **before the fight being evaluated**.

For each fighter appearance, historical variables are calculated entering that fight.

Examples include:

- Previous UFC fights
- Previous UFC wins and losses
- UFC win percentage
- Current UFC win streak
- Recent UFC form
- Previous UFC finishes
- Historical finish rate
- Previous UFC title fights
- Previous UFC main events
- Previous UFC performance bonuses

A fighter's later career accomplishments are therefore not applied retroactively to earlier events.

This allows events to be evaluated based on what was known at the time.

---

## 3. Overall V2 Model

The V2 Event Strength score consists of four major components:

| Component | Overall Weight |
|---|---:|
| Card Quality | 46% |
| Star Experience | 22% |
| Main Event Strength | 22% |
| Fanfare | 10% |

Conceptually:

`Event Strength = 0.46(Card Quality) + 0.22(Star Experience) + 0.22(Main Event Strength) + 0.10(Fanfare)`

When a component is legitimately unavailable, the model uses dynamic weighting across available components rather than treating missing information as zero.

---

## 4. Card Quality V2

Card Quality evaluates the strength and depth of the entire event.

V2 redesigns this component to give ranking depth substantially greater influence.

| Card Quality Variable | Weight |
|---|---:|
| Ranking Depth Index | 30% |
| Title Fights | 14% |
| Average UFC Experience | 14% |
| Average UFC Win Percentage | 14% |
| Average Win Streak | 14% |
| Average Finish Rate | 14% |

The Ranking Depth Index is the largest individual component.

---

## 5. Ranking Depth Index

### Motivation

In the original model, ranking strength was only one variable among several equally weighted Card Quality inputs.

Testing showed that this gave the depth of ranked talent relatively little influence on the final Event Strength score.

V2 addresses this with a dedicated Ranking Depth Index.

### Construction

| Ranking Depth Variable | Weight |
|---|---:|
| Total Ranking Points | 45% |
| Ranked Fighter Breadth | 25% |
| Ranked Matchups | 20% |
| Title Fights | 10% |

### Ranking Points

Ranked fighters receive points based on their position entering the event:

| Rank | Points |
|---|---:|
| Champion | 16 |
| #1 | 15 |
| #2 | 14 |
| #3 | 13 |
| ... | ... |
| #15 | 1 |
| Unranked | 0 |

An unranked fighter receives zero ranking points only when official rankings are available for that period.

Official ranking information is treated as unavailable before the UFC rankings era rather than assigning historical fighters artificial zero values.

### Overall Influence

Ranking Depth represents **30% of Card Quality**.

Card Quality represents **46% of the overall V2 model**.

Therefore, Ranking Depth has approximately:

`46% × 30% = 13.8%`

direct influence on the overall Event Strength score when ranking information is available.

---

## 6. Star Experience

Star Experience measures the amount of established UFC résumé and high-profile experience present on the card.

The component incorporates historical measures including:

- Previous UFC title-fight experience
- Previous UFC main-event experience
- Previous UFC performance bonuses

Only accomplishments occurring before the event being evaluated are counted.

This component represents **22% of V2 Event Strength**.

---

## 7. Main Event Strength

Main Event Strength separately evaluates the event's headlining matchup.

The current V2 candidate retains the original Main Event methodology after alternative redesigns were tested.

Inputs include historical measures such as:

- Combined UFC experience
- UFC win percentage
- Win streaks
- Previous title fights
- Previous UFC main events
- Previous performance bonuses
- Ranking strength

The Main Event component represents **22% of V2 Event Strength**.

---

## 8. Fanfare

Fanfare attempts to represent public and commercial interest surrounding an event.

The current V2 candidate retains the existing Fanfare methodology and assigns it **10% of the overall model**.

Available evidence includes measures such as:

- Search-interest acceleration
- Historical drawing evidence
- Commercial or audience evidence where available

Fanfare has significantly less historical coverage than the core fight and fighter variables.

Missing Fanfare information is not treated as zero.

---

## 9. Whole-Card Fanfare Research

A separate Fanfare V2 redesign was investigated during development.

The experimental framework expanded fanfare beyond the main event and evaluated fighters throughout the entire card.

Research included:

- Whole-card fighter placement
- Historical drawing evidence
- Commercial demand
- Search-interest acceleration
- Fighter star-power proxies

Card placement was also investigated so that main-event and co-main-event fighters could receive greater individual influence while the remainder of the card still contributed collectively.

The experimental framework was **not incorporated into the current V2 model**.

Testing indicated that résumé-based star-power proxies should not automatically be interpreted as actual fighter popularity.

Future Fanfare development therefore requires stronger historical absolute-popularity data before replacing the existing component.

---

## 10. Normalization

Many raw variables exist on very different scales.

For example:

- Ranking points
- UFC fights
- Win streaks
- Previous title fights

cannot be directly averaged in raw form.

The model therefore converts variables to comparable score distributions before combining them.

A zero-preserving percentile approach is used where appropriate:

- Missing values remain missing.
- Genuine zero values remain zero.
- Positive observations are percentile-ranked relative to other positive observations.

This prevents a genuine absence of an accomplishment from being confused with missing data.

---

## 11. Missing Data

Missing data is handled explicitly.

The model does **not** automatically convert missing observations to zero.

Examples of structurally unavailable data include:

- UFC rankings before the official rankings era
- Fanfare evidence for some historical events
- Commercial or audience information unavailable for many cards

When one of the four overall components is unavailable, its weight can be redistributed across the available components.

This prevents missing historical information from automatically lowering an event's score.

---

## 12. V1 vs. V2 Validation

V2 was compared against the original published model across all 788 events.

The redesign remained highly correlated with the original model while changing the treatment of ranking depth.

During validation:

- Overall score correlation remained approximately **0.996**.
- Rank correlation remained approximately **0.995**.
- **46 of the original Top 50 events remained in the V2 Top 50.**
- None of the original Top 50 fell outside the V2 Top 75.

This suggests that the redesign preserves the broad structure of the original model while allowing ranking depth to meaningfully affect individual cards.

---

## 13. Examples of V2 Rank Movement

The redesigned methodology changes some events more than others.

Examples include:

| Event | Published Rank | V2 Rank | Movement |
|---|---:|---:|---:|
| UFC 300: Pereira vs. Hill | 14 | 7 | +7 |
| UFC 205: Alvarez vs. McGregor | 10 | 5 | +5 |
| UFC 217: Bisping vs. St-Pierre | 4 | 2 | +2 |
| UFC 229: Khabib vs. McGregor | 11 | 10 | +1 |
| UFC 269: Oliveira vs. Poirier | 1 | 1 | 0 |
| UFC 329: McGregor vs. Holloway 2 | 30 | 30 | 0 |
| UFC 330: Makhachev vs. Machado Garry | 42 | 52 | -10 |
| UFC 302: Makhachev vs. Poirier | 9 | 25 | -16 |

These movements are model outputs rather than manually assigned adjustments.

---

## 14. Current Dataset

The current V2 dataset contains:

- **788 unique UFC events**
- **8,877 UFC fights** in the underlying updated fight dataset
- Historical coverage beginning **March 11, 1994**
- Current coverage through **September 19, 2026**

The latest event currently included is:

**UFC 331: Van vs. Pantoja 2**

---

## 15. Current Status

V2 remains a separate candidate model.

The original published UFC Event Strength Index has not been overwritten.

Current priorities for future development include:

1. Historical absolute fighter-popularity data
2. Improved whole-card Fanfare
3. Division and talent-pool depth analysis
4. Additional validation
5. Automated updating as new UFC events occur

The goal is to improve the model only when additional evidence supports the change rather than adjusting formulas to force particular events toward predetermined rankings.
