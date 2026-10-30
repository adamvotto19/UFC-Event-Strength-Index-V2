# UFC Event Strength Index

**A data-driven sports analytics project evaluating and ranking UFC events using fighter quality, competitive depth, main event strength, and star experience.**

Created by **Adam Smith**

---

## Project Overview

The UFC Event Strength Index is a Python-based analytics model designed to measure the overall strength of UFC fight cards.

Rather than evaluating an event based only on its main event or popularity, the model considers the quality and depth of the entire card.

The current dataset contains **570 UFC events**, with historical fighter and event information used to develop the rankings.

## The Three Main Components

- **Card Quality:** Measures the competitive depth and quality of the entire fight card.
- **Main Event Strength:** Evaluates the quality and experience of the main event fighters.
- **Star Experience:** Measures the experience, accomplishments, and recognition of fighters across an event.

The three components are combined to produce an overall Event Strength Index (ESI).

---

## UFC Event Rankings

### Top 10 UFC Events of All Time

![Top 10 UFC Events of All Time](visuals/top_10_ufc_events_all_time.png)

### Top 10 UFC Events of 2026

![Top 10 UFC Events of 2026](visuals/top_10_ufc_events_2026.png)

### Top 10 UFC Fight Nights of All Time

*Excludes numbered UFC events.*

![Top 10 UFC Fight Nights](visuals/top_10_ufc_fight_nights_all_time.png)

---

## Component Rankings

### Top 10 — Card Quality

![Top 10 Card Quality](visuals/top_10_ufc_card_quality.png)

### Top 10 — Main Event Strength

![Top 10 Main Event Strength](visuals/top_10_ufc_main_event_strength.png)

### Top 10 — Star Experience

![Top 10 Star Experience](visuals/top_10_ufc_star_experience.png)

---

## Featured Analysis: UFC 333

The model currently produces the following provisional results for UFC 333:

| Metric | Result |
|---|---:|
| Event Strength Index | 82.83 |
| Historical Ranking | #44 of 570 |
| Card Quality V3 | 70.19 |
| Final Card Quality | 84.49 |
| Main Event Strength | 72.21 |
| Star Experience | 92.53 |

**Data status:** Provisional estimate. Some historical fighter statistics, bonus records, and pre-event rankings require further verification.

---

## Dataset

The project includes a 570-event dataset containing event-level scoring information and ranking components.

[View the complete 570-event dataset](data/ufc_event_strength_index_570_events_provisional.csv)

## Methodology

The model uses historical UFC event and fighter information to evaluate:

- Fighter experience and win percentage
- Winning streaks and finishing ability
- Previous title fights and main events
- Official fighter rankings and ranking depth
- Ranked matchups and competitive depth
- Main event quality and fighter experience

See [METHODOLOGY.md](METHODOLOGY.md) for additional details.

---

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Jupyter Notebook
- GitHub

## Project Goals

- Build a data-driven UFC event ranking system.
- Analyze historical trends in UFC event quality.
- Compare numbered events and Fight Nights.
- Develop visualizations that communicate complex sports analytics.
- Continuously improve the model as new UFC events take place.

---

**Project Status:** Ongoing  
**Latest Dataset:** 570 UFC events  
**Creator:** Adam Smith
