# UFC Event Strength Index — Methodology

## 1. Project Objective

The UFC Event Strength Index evaluates the strength of UFC fight cards using historical event and fighter statistics.

The objective is to measure the overall quality and competitiveness of an event based on its entire fight card, while also accounting for experienced fighters, main event strength, and fan interest.

The current dataset covers **788 UFC events and 8,877 fights**, with event data through September 19, 2026.

## 2. Overall Event Strength Score

Each event receives a score based on four components.

| Component | Weight |
|---|---:|
| Card Quality | 46% |
| Star Experience | 22% |
| Main Event Strength | 22% |
| Fanfare | 10% |

When all components are available, the overall score is calculated as:

**Event Strength = (0.46 × Card Quality) + (0.22 × Star Experience) + (0.22 × Main Event Strength) + (0.10 × Fanfare)**

If a component is unavailable, its weight is redistributed proportionally among the available components.

## 3. Card Quality

Card Quality measures the competitive strength of the full fight card.

| Metric | Weight |
|---|---:|
| Ranking Depth Index | 30% |
| Title Fights | 14% |
| Average UFC Experience | 14% |
| Average UFC Win Percentage | 14% |
| Average Win Streak | 14% |
| Average Finish Rate | 14% |

The model combines these measurements into a Card Quality Score.

This approach rewards events with competitive depth across multiple fights, rather than focusing only on the main event.

## 4. Ranking Depth Index

Ranking Depth measures the overall strength of ranked competition across an event.

| Metric | Weight |
|---|---:|
| Total Ranking Points | 45% |
| Ranked Fighter Breadth | 25% |
| Ranked Matchups | 20% |
| Title Fights | 10% |

### Ranking Points

Fighters receive ranking points based on their position entering the event.

- Champion: 16 points
- Ranked #1: 15 points
- Ranked #2: 14 points
- Continuing downward through ranked #15: 1 point
- Unranked fighters: 0 ranking points when ranking data is available

The index also accounts for the number of ranked fighters, ranked-versus-ranked matchups, and title fights on the card.

**Historical ranking availability:** Events without reliable ranking information are treated as missing ranking data, not as events with zero ranking depth.

## 5. Star Experience

Star Experience evaluates fighters' established UFC résumés entering an event.

It uses historical experience and achievement information available before the event.

This component is intended to measure established UFC experience, rather than assuming that experience automatically equals popularity.

## 6. Main Event Strength

Main Event Strength measures the competitive and historical credentials of the event's headline fight.

The main event is evaluated separately from the overall card to recognize the importance of the headline matchup without allowing it to determine the entire event's score.

Only information available before the event is used.

## 7. Fanfare

Fanfare measures available indicators of public interest and drawing power.

Its existing data sources include:

- Commercial audience information, when available
- Historical drawing-power information
- Search-interest acceleration

Coverage varies significantly across historical events.

The current Fanfare component does not yet provide a complete measurement of the popularity of every fighter on a card.

Research into a more comprehensive whole-card Fanfare measure remains separate from the current scoring model.

## 8. Normalization

The model converts individual metrics into comparable scores before combining them.

Percentile-based normalization helps compare measurements that have different units or scales.

For applicable metrics, genuine zero values are preserved as zero rather than being converted into nonzero percentile scores.

## 9. Missing Data

Missing information is not automatically treated as zero.

When an input is unavailable, the model uses available information and adjusts applicable weights.

This is especially important for historical rankings and fan-interest measures, where coverage differs across time periods.

## 10. Preventing Future-Result Leakage

Fighter statistics are based on information available before the relevant UFC event.

Examples include:

- Prior UFC fights and experience
- Prior UFC wins and losses
- Entering-event win streaks
- Prior finish statistics
- Rankings available at the time

Future results are not used to strengthen an earlier event's score.

## 11. Dataset Coverage

| Measurement | Coverage |
|---|---:|
| UFC events | 788 |
| Historical fights | 8,877 |
| Earliest event | March 11, 1994 |
| Latest event | September 19, 2026 |
| Events with Ranking Depth data | 564 |

The dataset contains event-level scoring components, overall scores, rankings, and historical statistics.

## 12. Interpretation and Limitations

The Event Strength Index measures modeled event strength, not the entertainment value of the fights after they occur.

A high score indicates that an event had strong statistical characteristics according to the model.

Important limitations include incomplete historical ranking coverage, limited commercial audience information, and differences in available data across eras.

The correlation between Ranking Depth and overall Event Strength is approximately **0.841** among events with ranking-depth information. Because Ranking Depth contributes directly to the overall score, this correlation is descriptive and should not be interpreted as independent validation.

## 13. Future Research

Potential areas for improvement include:

- Expanding reliable historical ranking coverage
- Developing more complete whole-card fan-interest measures
- Testing model results against independent external indicators
- Improving historical data completeness and documentation

Any future adjustments should be evaluated empirically rather than designed to force specific events into preferred ranking positions.

---

**Author:** Adam Votto  
**Project:** UFC Event Strength Index  
**Data through:** September 19, 2026
