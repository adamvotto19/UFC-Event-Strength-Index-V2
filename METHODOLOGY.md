# UFC Event Strength Index — Methodology

**Author:** Adam Smith  
**Project:** UFC Event Strength Index (ESI)  
**Dataset:** 570 UFC events, including provisional UFC 333 estimates

## 1. Project Objective

The UFC Event Strength Index is a Python-based sports analytics model designed to evaluate and rank UFC fight cards.

The goal is to measure the overall strength of an event using fighter statistics, competitive depth, main event quality, and star experience.

Unlike rankings based on personal opinions or fight entertainment, the ESI uses a consistent mathematical framework to compare events.

## 2. Overall Event Strength Index

Each event receives a score from 0 to 100 based on three components.

| Component | Weight |
|---|---:|
| Card Quality | 70% |
| Main Event Strength | 20% |
| Star Experience | 10% |

**Final formula:**

ESI = (0.70 × Card Quality) + (0.20 × Main Event Strength) + (0.10 × Star Experience)

The model prioritizes the strength of the entire fight card while still recognizing the importance of the main event and experienced fighters.

## 3. Card Quality

Card Quality evaluates the competitive strength and depth of the entire event.

The model incorporates:

- Ranked fighters and ranked matchups
- Ranking depth outside the main event
- Fighter experience
- UFC win percentages
- Entering-event winning streaks
- Finishing statistics
- Title fights

### Card Quality V3 Formula

Card Quality V3 is calculated using:

| Component | Weight |
|---|---:|
| Balanced Ranking Depth | 40% |
| UFC Experience | 10% |
| UFC Win Percentage | 7% |
| Winning Streak | 4% |
| Finish Rate | 4% |
| Ranked Matchup Factor | 25% |
| Title Depth Factor | 10% |

Card Quality V3 =

(0.40 × Balanced Ranking Depth)  
+ (0.10 × Experience)  
+ (0.07 × Win Percentage)  
+ (0.04 × Win Streak)  
+ (0.04 × Finish Rate)  
+ (0.25 × Ranked Matchup Factor)  
+ (0.10 × Title Depth Factor)

### Final Card Quality Adjustment

The final Card Quality score incorporates an adjusted matchup-quality measurement.

Final Card Quality = Card Quality V3 + 0.25 × (Matchup Quality Score − Ranked Matchup Factor)

This adjustment allows the model to distinguish between events with similar numbers of ranked matchups but different overall competitive profiles.

## 4. Ranking Depth

Ranking Depth evaluates how much ranked talent appears throughout the event, especially outside the main event.

Ranking points are assigned as follows:

- Champion: 16 points
- Ranked #1: 15 points
- Ranked #2: 14 points
- Continuing downward to ranked #15: 1 point
- Unranked: 0 points when ranking information is available

The model calculates ranking depth using both average depth and total ranking points.

### Outside-Main-Event Depth

Outside-Main Depth Score = Outside-Main Weighted Ranking Points / [0.48 × (Total Fights − 1)]

### Balanced Depth Score

Balanced Depth Score = (Average Depth Percentile + Total Depth Percentile) / 2

These calculations reward events with strong ranked competition across multiple fights rather than relying entirely on the headline matchup.

## 5. Ranked Matchup Factor

The Ranked Matchup Factor measures the percentage of fights featuring ranked-versus-ranked matchups.

Ranked Matchup Factor = 100 × (Ranked Matchups / Total Fights)

For example, an event with 5 ranked matchups across 14 fights receives a Ranked Matchup Factor of approximately 35.71.

The final model also uses a separate Matchup Quality Score to refine Card Quality.

## 6. Title Depth Factor

The Title Depth Factor accounts for title-fight strength alongside the overall depth of the event.

Title Depth Factor = Title Score × [0.50 + 0.50 × (Balanced Depth Score / 100)]

This rewards championship events that also feature strong supporting cards.

## 7. Main Event Strength

Main Event Strength evaluates the historical and competitive credentials of the event's headline matchup.

Relevant inputs include:

- Main event fighters' UFC experience
- UFC win percentages
- Winning streaks
- Previous championship appearances
- Previous main event appearances
- Ranking strength

Main Event Strength contributes 20% to the final Event Strength Index.

## 8. Star Experience

Star Experience evaluates the established UFC experience and accomplishments of fighters appearing on the event.

Relevant inputs include:

- UFC fight experience
- Previous title fights
- Previous main events
- Historical fighter accomplishments

Star Experience contributes 10% to the final Event Strength Index.

This component represents established UFC credentials, not a direct measurement of popularity or commercial drawing power.

## 9. Normalization and Historical Comparisons

The model converts different statistical measurements into comparable scores.

Percentile-based normalization is used for ranking-depth calculations and other historical comparisons.

This allows statistics measured on different scales to contribute to a combined scoring system.

Because some scores depend on the historical comparison dataset, adding new events may affect percentile-based values and rankings.

## 10. Missing Data and Limitations

Historical UFC data is not equally complete across all events.

Important limitations include:

- Incomplete historical fighter rankings
- Differences in statistical availability across eras
- Missing fighter-level historical records
- Estimated values for certain recent events
- Limited direct measurement of commercial popularity

Missing data is not automatically assumed to represent zero performance.

Estimated inputs should be identified separately from verified historical statistics.

## 11. UFC 333 — Provisional Analysis

UFC 333 is included as a provisional entry in the 570-event dataset.

| Metric | Provisional Result |
|---|---:|
| Event Strength Index | 82.83 |
| Overall Ranking | #44 of 570 |
| Final Card Quality | 84.49 |
| Main Event Strength | 72.21 |
| Star Experience | 92.53 |

Some UFC 333 fighter statistics, historical rankings, and scoring components remain estimated or require additional verification.

These results should not be interpreted as fully verified historical measurements.

## 12. Dataset Coverage

| Measurement | Coverage |
|---|---:|
| Events ranked | 570 |
| Scoring scale | 0–100 |
| Main components | 3 |
| Historical baseline | 569 events |
| Provisional UFC 333 entry | 1 |

The complete event-level dataset is available here:

[View the 570-event dataset](data/ufc_event_strength_index_570_events_provisional.csv)

## 13. Interpretation

A higher ESI score indicates stronger statistical characteristics according to the model.

The index is designed to measure the strength of an event's lineup, not the entertainment value of fights after they occur.

The results should be understood as model-based rankings rather than definitive judgments about the greatest UFC events.

## 14. Future Improvements

Planned improvements include:

- Verifying additional historical fighter statistics
- Expanding historical ranking coverage
- Refining matchup-quality calculations
- Developing stronger measures of fighter recognition and drawing power
- Testing the model against independent measures of event quality
- Automating event updates and visualizations

The long-term goal is to create a transparent, reproducible UFC analytics system that can be updated as new events occur.

---

**Created by Adam Smith**  
**UFC Event Strength Index — Sports Analytics Project**
