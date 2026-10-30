# TripPilot: Your Travel Companion for the Whole Trip

> **Working title:** TripPilot 
> **One-liner:** *Not a trip planner you use once. An AI companion that plans with you, stays with you during the trip, and changes the plan with you when you change your mind.*

**Pilot market:** Vietnam (domestic and inbound travel)
**Approach:** Open to popular, widely used travel services. Vingroup services can be added later as another provider.

---

## 1. Summary

Most AI trip planners create an itinerary once and then go quiet. But real trips change: it rains, a place is closed, someone gets tired, or you simply discover somewhere you'd rather go.

**TripPilot is a continuous travel assistant.** It helps you dream, plan, and prepare, and then it stays active throughout the trip. It reminds you of what matters at the right moment, suggests alternatives, and lets you **book tickets and stays just before you need them** instead of locking everything in days ahead. When you change your mind mid-trip, it shows your options and the cost of switching in seconds.

---

## 2. The Problem

### For individual travelers
- Planning is scattered across maps, booking sites, social media, notes, and chats.
- Booking early forces commitment before you know the weather, your energy level, or what you'll discover.
- Changing plans mid-trip is stressful: you must re-research, compare, cancel, and rebook under time pressure.
- Nobody reminds you of small but important things at the right time (check-out, closing hours, last train).

### For groups and families
- Different preferences, budgets, and energy levels.
- Hard to keep everyone informed about who booked what.

### The gap in today's market
Existing AI trip planners focus on **before the trip**. Few of them help when the trip is actually happening, which is when plans change most. *(To be verified through a short competitor test in Week 1.)*

### Similar services
- https://www.trip.com/tripgenie/ 


---

## 3. Who It's For

| User | What they need | Typical moment |
|---|---|---|
| **Spontaneous explorer** (solo/couple) | Flexibility and easy discovery | "This place is boring. Somewhere cooler within 4 hours?" |
| **Family planner** | Kid-friendly pacing and rainy-day backups | Rain at 2 pm: outdoor plan swapped for an indoor option with tickets |
| **Group of friends** | One shared plan and quick decisions | Vote on tomorrow's activity, book for everyone together |
| **Inbound tourist** | Local guidance and trusted options | "How do I get from the airport to Hoi An and what should I see?" |
| **Senior traveler** | Slow pace, clear reminders | Simple reminder cards, rest-friendly routes |

**Primary focus for the first version:** the spontaneous explorer, because this group benefits most from mid-trip flexibility.

---

## 4. The Solution

TripPilot works through the **whole trip**, in five stages:

| Stage | What TripPilot does | Example |
|---|---|---|
| **Dream** | Inspires and narrows choices | "Beach, 5 days, under 15M VND, no early mornings" gives 3 destination ideas |
| **Plan** | Builds a flexible draft | Day-by-day outline, rough budget, transport options. Nothing is locked. |
| **Prepare** | Commits only what must be early | Flights, peak-season stays, high-demand tickets. The rest stays flexible. |
| **During the trip** | Acts as a live companion | Reminders, weather swaps, "what's next?", last-minute booking, destination changes |
| **After** | Closes the loop | Trip recap, spending summary, feedback, remembered preferences |

### Guiding principles
1. **Continuous, not one-time.** The app is most valuable *after* the trip starts.
2. **Flexibility first.** Favor options with free cancellation and late booking. Changing your mind should be cheap.
3. **Open to many providers.** TripPilot works with popular, searchable travel services, not a single company's inventory.
4. **You stay in control.** The assistant suggests and prepares. You confirm anything that costs money.
5. **Respect attention.** A few useful nudges, never spam.
6. **Works with weak signal.** Essential information stays available when connectivity is poor.

---

## 5. Core Functionality

### 5.1 Conversational trip planning
- Describe your trip in plain language: dates, who's traveling, budget, interests, pace, and special needs.
- The assistant asks only what it needs, one question at a time, and states its assumptions.
- It produces a **draft**, not a final plan. Edit by chat or by tapping.
- Every day also has a **Plan B** (for example, a rainy-day or low-energy version).

### 5.2 Living itinerary
- A day-by-day timeline with map and list views.
- Every item shows its status (**idea, shortlisted, on hold, booked, replaced**), its price, cancellation terms, and travel time to the next stop.
- Changes are tracked with a reason, for example: *"Swapped the beach for a museum because of rain at 14:00."*
- Easy undo.

### 5.3 Search and compare across providers
- Say what you need ("family-friendly hotel in Hoi An, 2 nights, under 2M per night").
- The assistant gathers options from multiple popular travel services and compares them side by side: price, rating, location, cancellation terms, and a short plain-language summary of trade-offs.
- Always shows how recent the price information is.

### 5.4 Last-minute booking assistant
Instead of locking everything days ahead, each item gets a **"book by" guidance** based on how quickly that type of item sells out or changes price.

| Item | Typical timing | What the app does |
|---|---|---|
| Casual restaurant | Same day | Suggests at mealtime and offers to reserve |
| Local taxi/ride | Minutes before | One tap from your current location |
| Popular attraction ticket | Hours to 1 day before | Nudges you when the plan looks likely |
| Day tour or activity | About 1 day before | Reminds you the evening before |
| Intercity bus/train | Hours to a few days | Warns when seats are running low |
| Next-destination hotel | Hours to a few days | Prefers free-cancellation rates |
| Flights | Days to weeks | Tracks prices and suggests when to book |

*(Timings are starting assumptions to validate in user research.)*

The app tells you plainly: **"You can safely wait until 10:00"** or **"Book now, this usually sells out."**
For the first version, booking is completed through the provider's checkout (with a smooth hand-off). Booking directly inside the app is a later step.

### 5.5 Mid-trip destination change ("Pivot")
This is the flagship feature.

**When you say:** *"Let's go somewhere else."* / *"Skip tomorrow's tour."* / *"Extend two days."* / *"Add Hue."*

**TripPilot will:**
1. Check where you are, how many days remain, your budget left, and what you've already booked.
2. Show what you'd lose or get refunded if you change.
3. Offer about three options: where to go, how to get there (tonight or tomorrow), where to stay, and the cost difference.
4. Explain the trade-offs and give a recommendation.
5. After you confirm, update the itinerary, tickets, and reminders, and notify travel companions.

**Example:**

```
You're in Da Nang (Day 3 of 6). Budget left: 9.2M VND.

Option A: Hue (2.5 h by train, leaves 16:10)
  Cost: about 1.6M for the next 2 nights + 180k train.
  Current hotel: fully refundable.
  Best for: culture, cooler weather.

Option B: Da Lat (1 h flight tomorrow 09:20)
  Cost: about 2.9M including flight and 2 nights.
  Current hotel: 50% refund (-700k).
  Best for: cool weather, nature.

Option C: Stay, change the plan
  Replace tomorrow's tour with Ba Na Hills + Hoi An night market.
  No cancellation cost.
```

### 5.6 Suggestions, reminders, and alerts
TripPilot pays attention to time, location, weather, and your plan, and speaks up when it matters.

| Situation | Example message |
|---|---|
| Mealtime nearby | "It's 11:45 and you're near X. 3 well-rated lunch spots within 5 minutes." |
| Weather change | "Rain from 14:00. Swap the beach for a museum? I can book tickets." |
| Closing time | "The temple closes at 17:00. You have 40 minutes." |
| Selling out | "Tickets for tomorrow's show are going fast. Hold two?" |
| Price drop | "The Hue hotel you saved is 18% cheaper." |
| Logistics | "Check-out is 12:00. Taxi to the station at 13:30?" |
| Flight changes | "Your flight is delayed 90 minutes. Pickup moved." |
| Documents | "Visa application deadline in 3 days." |
| Pace and energy | "Big walking day. Want a café or massage break?" |
| Budget | "70% of budget used, 3 days left." |
| Safety | "Typhoon warning for your next stop. Here are alternatives." |

**Anti-spam promise:**
- Messages are ranked: **critical** (flights, safety, deadlines), **useful** (weather, closing times), **nice-to-have** (ideas).
- Daily limit on non-critical messages, quiet hours, and user-adjustable frequency.
- Every message has quick actions and a thumbs up/down so the app learns what's helpful.

### 5.7 "What else?" alternatives
At any time, for any item or day:

| Situation | Alternatives offered |
|---|---|
| Rain or bad weather | Indoor options nearby |
| Sold out or closed | Similar activities at a similar price |
| Over budget | Cheaper or free equivalents |
| Tired | Slower, shorter, or restful options |
| Bored | Different vibe within time and budget |
| Delay | Shorter or reordered schedule |
| Companions disagree | Options that satisfy both sides |

Each alternative explains **why** it was suggested.

### 5.8 Trip wallet
- All tickets, confirmations, QR codes, addresses, and contact numbers in one place.
- A "needed in the next 24 hours" view at the top.
- Available without internet.

### 5.9 Later features
- **Group trips:** shared plan, voting, split expenses.
- **Budget tracker:** automatic spend tracking against plan.
- **Voice and multilingual support:** hands-free use, local languages.
- **Offline mode** for maps, tips, and emergency numbers.
- **Post-trip recap** and preferences remembered for next time.
- **Vingroup services as an added provider** (see Section 9).

---

## 6. Key Use Cases

### Use case 1: Plan a trip in minutes
1. The user describes their trip in one or two sentences.
2. TripPilot asks one or two clarifying questions.
3. It presents a draft itinerary with a Plan B for each day, a budget range, and "book now vs. book later" guidance.
4. The user adjusts by chat ("less temples, more cafés").
5. TripPilot recommends booking only what truly needs booking now.

### Use case 2: Morning check-in on a trip day
1. A morning card shows weather, today's plan, travel times, and anything to book today.
2. The assistant flags: "Ba Na Hills tickets sell out on weekends. Book now or decide by 10:00."
3. The user books or taps "Not today", and the item moves back to the flexible list.

### Use case 3: Rain changes the plan
1. TripPilot detects rain forecast for the afternoon.
2. It proposes 2-3 indoor alternatives nearby, with tickets and travel time.
3. One tap swaps the activity. The old item is archived with the reason.

### Use case 4: Changing destination mid-trip
1. The user says they want to leave for somewhere new.
2. TripPilot shows options, refund impact, and cost differences (see 5.5).
3. The user picks one and confirms. The plan, tickets, and reminders update automatically.

### Use case 5: Same-day transport
1. The user: "We want to leave for Hue this afternoon."
2. TripPilot compares train, bus, private car, and ride options by departure time and price.
3. The user books one. Pickup time and reminders are added.

### Use case 6: End-of-day wrap-up
1. Evening summary: what you did, spend today, tomorrow preview.
2. "Anything you'd like to change tomorrow?" gives a quick edit.

---

## 7. Requirements

### 7.1 Functional requirements

**Must have (first version)**

| ID | Requirement |
|---|---|
| R1 | Users can describe a trip in natural language and receive a draft itinerary. |
| R2 | Every day has a Plan B alternative. |
| R3 | Itinerary items have clear statuses and can be edited, replaced, and undone. |
| R4 | The app searches and compares options from multiple popular travel services. |
| R5 | Each item shows price, cancellation terms, and how recent the information is. |
| R6 | The app gives "book by" guidance for items, supporting last-minute booking. |
| R7 | Users can complete booking through the provider (hand-off), and bookings are saved in the trip wallet. |
| R8 | Users can change destination mid-trip and see options with cost and refund impact. |
| R9 | The app sends reminders and suggestions based on time, location, weather, and plan. |
| R10 | The app offers alternatives for rain, closures, sold-out items, budget, and fatigue. |
| R11 | Users control notification frequency and can give feedback on each message. |
| R12 | The assistant never spends money or cancels a booking without explicit user confirmation. |

**Should have**
| ID | Requirement |
|---|---|
| R13 | Trip wallet works without internet. |
| R14 | Budget tracking against the plan. |
| R15 | Vietnamese and English. |
| R16 | Simple trip recap after the trip. |

**Could have (later)**
| ID | Requirement |
|---|---|
| R17 | Group trips with shared plans, voting, and split costs. |
| R18 | Voice interaction. |
| R19 | Booking and payment directly inside the app. |
| R20 | Additional languages (Korean, Chinese, etc.). |
| R21 | Vingroup services as an added provider. |

### 7.2 Quality requirements (non-technical)

| Area | Expectation |
|---|---|
| **Speed** | First draft itinerary in under ~30 seconds. Destination-change options in under ~20 seconds. |
| **Accuracy** | Prices, hours, and availability must come from real sources and be shown with "last checked" time. The assistant should say so when it is unsure. |
| **Trust** | Never claim something is booked unless the provider has confirmed. Label any sponsored results. |
| **Ease of use** | Usable one-handed on a phone while walking. Quick-reply buttons for common answers. |
| **Attention** | Few, relevant notifications, with user control. |
| **Privacy** | Location is opt-in and can be limited to "while using". Users can view and delete what the app has learned. |
| **Reliability on the road** | Key trip information (wallet, today's plan) remains available with weak or no signal. |
| **Safety** | Show official warnings (weather, health, entry rules). Do not present AI answers as legal or medical advice. |

### 7.3 Assumptions and dependencies
- Access to popular travel services (via public tools, affiliate links, or partner arrangements) must be confirmed with the mentor. For the first version, the project relies on public data, hand-off links, and simulated bookings for demo purposes.
- Real in-app payments are out of scope for the first version.
- Weather, map, and opening-hours information is available from public sources.

---

## 8. How It's Different

| Today | TripPilot |
|---|---|
| One-time itinerary | Companion across the whole trip |
| Book everything upfront | Book at the last sensible moment, with guidance |
| Static plan | Living plan with a built-in Plan B |
| Mid-trip change means starting over | Destination change in seconds, with cost and refund impact |
| Silent until you open it | Helpful, timely, restrained nudges |
| Tied to one company's inventory | Open to many popular providers |

---

## 9. Value and Future Path

### Value to travelers
- Less stress, more flexibility, fewer wasted bookings.
- One place for plans, tickets, reminders, and decisions.

### Value to the business
- **Engagement:** the assistant is used daily during trips, not once before them.
- **Flexible partnerships:** because the app is open to many providers, any ecosystem can plug in.
- **Vingroup path (later):** Vinpearl stays, VinWonders tickets, Xanh SM rides, and EV charging via V-Green could become providers inside the same experience. TripPilot could also be offered as a **module inside V-App**, so users don't need to download anything new.
- **What a Vin integration would add:** richer bundles (stay + park + transfer), EV-aware road trips, and loyalty and payment in one place.

### Revenue ideas (for discussion)
- Commission on bookings through partners.
- Premium features (group tools, price tracking, unlimited in-trip assistant).
- White-label or embedded version for ecosystems and operators.
- Clearly labeled sponsored placements.

---
