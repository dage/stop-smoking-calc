Stop Smoking Motivator — Product Requirements Document (v0.3)

1. Purpose

Create a single‑page, share‑friendly web app that converts “hours since last cigarette” into an eye‑catching timeline of physiological milestones and a live counter for cigarettes not smoked and money saved. The page must run entirely from one self‑contained index.html file and work offline once cached.

2. Goals & Success Criteria

Goal	Success metric
Motivate recent quitters to stay smoke‑free	≥ 60 % of first‑time visitors return within 48 h (via localStorage flag)
Immediate value in ≤ 10 s	Time from first load to timeline rendered on 3G fast < 10 s
Zero‑friction deployment	App works when index.html is dragged into any browser or hosted on GitHub Pages
Privacy‑first	No network requests after first load (optional Plausible script opt‑in)

3. Target Audience
	•	Primary : People in their first 0‑30 days of quitting nicotine who want quick encouragement on mobile or desktop.
	•	Secondary : Friends/family who share the page to encourage others.

4. Key Features

4.1 Quit Data Input
	•	Relative input – three numeric fields:
	•	Days since last cigarette.
	•	Hours since last cigarette.
	•	Average cigarettes per day (default 20).
	•	Country selector – 🇹🇭 Thailand or 🇺🇸 USA (radio buttons with emoji flags).
	•	Auto‑fills pack price: 70 THB for Thailand, $8 USD for USA (2025 national average). Users can override.
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

⏳  2 days 14 h 23 m
🚭  55 cigarettes avoided
💰  ฿ 193 saved

Widget updates every second with requestAnimationFrame.

4.5 Motivational Snippets

Rotating bank of 30+ one‑liner quotes stored in JS array; one chosen at random per visit.

4.6 Share & Bookmark

Copy‑to‑clipboard permalink serialises all input as URL hash (/#d=2&h=14&c=20&ct=th). Keeps static hosting simple.

4.7 Discreet Disclaimer

Smaller, low‑contrast footer text: “Not medical advice. For information only.” Stealthed at font‑size: 0.75rem; opacity: .55;.

5. Data Content & Model

5.1 Milestone Catalogue (v1 draft — 21 entries)

Offset (h)	Label	Key Benefits (short)
0	Now	Pulse & BP drop • temp of hands/feet rises
4	4 h	CO in blood ↓ 50 %
8	8 h	O₂ in blood ↗ to normal
12	12 h	Cough reflex starts to improve
24	24 h	Heart-attack risk begins ↓
36	36 h	Taste & smell noticeably sharper
48	48 h	CO gone • nerve endings regrow
60	2.5 d	Nicotine eliminated
72	3 d	Bronchi relax • breathing easier
96	4 d	Energy levels increase
168	1 w	Sense of smell fully restored
336	2 w	Circulation improves • walking easier
720	1 m	Lung function +10 %
1440	2 m	Exercise endurance up
2160	3 m	Airway cilia regrow • chest clear
4320	6 m	Coughing/wheezing cut by 50 %
8760	1 y	CHD risk −50 %
26280	3 y	Heart attack risk = non-smoker
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
milestones[]	Array of objects {hours,label,benefit}	{48,"48 h","CO normalises"}

Milestone source curation (internal TODO): compile from WHO, CDC, NHS, Mayo Clinic; cite each benefit in code comments.

6. Technical Requirements
	•	Architecture: one index.html with inline <style> (≤ 8 KB gzipped) & ES6 <script type="module"> (≤ 15 KB gzipped).
	•	Dependencies: none. Optional CDN dayjs if code size grows.
	•	Performance: First Contentful Paint < 0.5 s on 3G Fast.
	•	Accessibility: WCAG 2.2 AA; aria‑live for counters.
	•	Responsive: Mobile‑first flexbox; grid on ≥ 768 px.
	•	Testing: Manual checklist; npm tooling out‑of‑scope until v1.1.

7. Design Guidelines
	•	Palette (minimal modern):
	•	Background: #f2f4f6 (very light gray)
	•	Primary accent: #ff6b6b (coral)
	•	Success accent: #2ecc71 (mint green)
	•	Text: #1a1a1a
	•	Soft cards (box‑shadow: 0 1px 4px rgba(0,0,0,.05)), rounded corners (6 px).
	•	Micro‑animations: fadeInUp 200 ms ease‑out on card load.
	•	Font: system stack with font‑feature‑settings: "tnum" for counters.
