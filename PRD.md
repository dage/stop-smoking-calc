Stop Smoking Motivator — Product Requirements Document (v0.3)

1. Purpose

Create a single‑page, share‑friendly web app that converts "hours since last cigarette" into an eye‑catching timeline of physiological milestones and a live counter for cigarettes not smoked and money saved. The page must run entirely from one self‑contained index.html file and work offline once cached.

2. Goals & Success Criteria

Goal	Success metric
Motivate recent quitters to stay smoke‑free	≥ 60 % of first‑time visitors return within 48 h (via localStorage flag)
Immediate value in ≤ 10 s	Time from first load to timeline rendered on 3G fast < 10 s
Zero‑friction deployment	App works when index.html is dragged into any browser or hosted on GitHub Pages
Privacy‑first	No network requests after first load (optional Plausible script opt‑in)

3. Target Audience
	•	Primary : People in their first 0‑30 days of quitting nicotine who want quick encouragement on mobile or desktop.
	•	Secondary : Friends/family who share the page to encourage others.

4. Key Features

4.1 Quit Data Input
	•	Relative input – three numeric fields:
	•	Days since last cigarette.
	•	Hours since last cigarette.
	•	Average cigarettes per day (default 20).
	•	Country selector – 🇹🇭 Thailand or 🇺🇸 USA (radio buttons with emoji flags).
	•	Auto‑fills pack price: 70 THB for Thailand, $8 USD for USA (2025 national average). Users can override.
	•	All values persist to localStorage.

4.2 Real‑Time Progress Engine
	•	Calculates elapsedSeconds every second via Date.now() – stored as timestamp quitEpoch.
	•	Computes:
	•	Milestone progress (see Data Model).
	•	Cigarettes avoided = elapsedSeconds / 3600 × avgCigsPerDay / 24.
	•	Money saved = cigsAvoided × pricePerCig (packPrice / 20).

4.3 Benefits Timeline & Detail View
	•	Card-based timeline (vertical on mobile, horizontal scroll on wide screens).
	•	Card states: completed, in-progress (progress bar), upcoming.
	•	Tap/Click a card → modal sheet with extended benefit copy (1–3 sentences), bullet list of relevant citations (WHO, CDC, etc.).
	•	Card‑based timeline (vertical on mobile, horizontal scroll on wide screens).
	•	Card states: completed, in‑progress (shows progress bar), upcoming.
	•	Tapping a card flashes a short fact sourced from WHO / CDC / NHS.

4.4 Live Stats Widget

Large, monospace counters:

⏳  2 days 14 h 23 m
🚭  55 cigarettes avoided
💰  ฿ 193 saved

Widget updates every second with requestAnimationFrame.

4.5 Motivational Snippets

Rotating bank of 30+ one‑liner quotes stored in JS array; one chosen at random per visit.

4.6 Share & Bookmark

Copy‑to‑clipboard permalink serialises all input as URL hash (/#d=2&h=14&c=20&ct=th). Keeps static hosting simple.

4.7 Discreet Disclaimer

Smaller, low‑contrast footer text: "Not medical advice. For information only." Stealthed at font‑size: 0.75rem; opacity: .55;.

5. Data Content & Model

5.1 Milestone Catalogue (v1.1 — 26 entries)

Offset (h)	Label	Key benefits (short)
0	Now	Body starts repair • pulse & BP begin to fall
0.33	20 m	HR & BP back to normal • hands/feet warm up
2	2 h	Blood-nicotine ↓ ~50 % (≈ half-life)
4	4 h	CO in blood ↓ 50 % • O₂ rising
6	6 h	HR slows further • BP stabilises
8	8 h	O₂ back to normal • most nicotine cleared
12	12 h	CO level = non-smoker • organs get full O₂
24	24 h	Heart-attack risk begins to fall
36	36 h	Taste & smell start sharpening
48	48 h	All CO gone • nerve endings regrow • taste & smell improving further
60	2.5 d	Body nicotine-free
72	3 d	Bronchi relax • breathing easier
96	4 d	Energy levels noticeably higher
120	5 d	Collagen renewal kicks in • skin looks brighter
168	1 w	Sense of smell fully restored • breathing steadier
240	10 d	More energy & easier breathing reported by most quitters
336	2 w	Circulation improves • walking feels easier
720	1 m	Lung function +10 %
1440	2 m	Exercise endurance up
2160	3 m	Airway cilia regrow • chest clearer
4320	6 m	Coughing / wheezing cut by ≈50 %
8760	1 y	CHD risk −50 %
26280	3 y	Heart-attack risk ≈ non-smoker
43800	5 y	Stroke risk = non-smoker
87600	10 y	Lung-cancer death risk −50 %
157680	18 y	CHD risk ≈ never-smoker

Full benefit blurbs (1–3 sentences each) stored in milestoneDetails[]; sourced from WHO, CDC, NHS, Mayo Clinic. Each record also stores citationId[] for tooltip references.

5.2 Data Model

Key	Description	Example
quitEpoch	Unix epoch ms of last cigarette	1720898400000
avgCigsPerDay	User input, default 20	20
country	"th" or "us"	"th"
packPrice	Currency float (THB or USD)	70
milestones[]	Array {hours,label,benefitShort,detail,citationIds[]}	see 7.1

Key	Description	Example
quitEpoch	Unix epoch ms of last cigarette	1720898400000
avgCigsPerDay	User input, default 20	20
country	"th" or "us"	"th"
packPrice	Currency float (THB or USD)	70
milestones[]	Array of objects {hours,label,benefit}	{48,"48 h","CO normalises"}

Milestone source curation (internal TODO): compile from WHO, CDC, NHS, Mayo Clinic; cite each benefit in code comments.

6. Technical Requirements
	•	Architecture: one index.html with inline <style> (≤ 8 KB gzipped) & ES6 <script type="module"> (≤ 15 KB gzipped).
	•	Dependencies: none. Optional CDN dayjs if code size grows.
	•	Performance: First Contentful Paint < 0.5 s on 3G Fast.
	•	Accessibility: WCAG 2.2 AA; aria‑live for counters.
	•	Responsive: Mobile‑first flexbox; grid on ≥ 768 px.
	•	Testing: Manual checklist; npm tooling out‑of‑scope until v1.1.

7. Design Guidelines
	•	Palette (minimal modern):
	•	Background: #f2f4f6 (very light gray)
	•	Primary accent: #ff6b6b (coral)
	•	Success accent: #2ecc71 (mint green)
	•	Text: #1a1a1a
	•	Soft cards (box‑shadow: 0 1px 4px rgba(0,0,0,.05)), rounded corners (6 px).
	•	Micro‑animations: fadeInUp 200 ms ease‑out on card load.
	•	Font: system stack with font‑feature‑settings: "tnum" for counters.

8. Phase 2 Requirements (v2.0)

8.1 Cigarette Visualization Widget
	•	Visual representation of cigarettes not smoked as stacked cigarette packs.
	•	Display format: 20 cigarette packs stacked horizontally (lying flat) next to a human figure for scale.
	•	Pack dimensions: Each pack measures ~2.0 cm height when lying flat (based on standard cigarette pack dimensions).
	•	Human figure: SVG icon representing average adult height for visual comparison.
	•	Stacking logic: Packs stack from bottom to top, with visual indicators showing "saved" vs "remaining to next milestone."
	•	Responsive scaling: Visualization adapts to screen size while maintaining proportional relationships.

8.2 Enhanced Timeline (v2.0)
	•	Timeline orientation: Always display vertically regardless of screen size (removes horizontal scroll behavior).
	•	Updated milestone data: Use the complete v1.1 milestone catalogue (26 entries) with all micro-milestones.
	•	Current milestone detail: Display full detailed description (1-3 sentences) of the active/current milestone prominently within the timeline.
	•	Enhanced card states: 
		•	Completed: Green checkmark, full opacity
		•	In-progress: Progress bar with percentage, highlighted border
		•	Current: Expanded card showing detailed benefit description
		•	Upcoming: Muted appearance, collapsed view

8.3 Technical Updates (v2.0)
	•	SVG integration: Implement inline SVG for human figure and cigarette pack icons.
	•	Timeline refactor: Remove horizontal scroll logic, implement vertical-only layout.
	•	Milestone detail system: Add detailed descriptions for all 26 milestones with proper citation handling.
	•	Performance consideration: Ensure Phase 2 additions stay within existing size constraints (≤ 25 KB total).

8.4 Data Model Updates (v2.0)
	•	Milestone objects enhanced with:
		•	`detailDescription`: Full 1-3 sentence benefit explanation
		•	`citations`: Array of source references (WHO, CDC, NHS, etc.)
		•	`visualPriority`: Boolean for highlighting in current milestone display
	•	Visualization calculations:
		•	`packsNotSmoked`: Math.floor(cigarettesAvoided / 20)
		•	`packHeight`: 2.0 cm constant for stacking calculations
		•	`humanHeight`: 170 cm average for scale reference
