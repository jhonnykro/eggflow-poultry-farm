# EggFlow — Smart Poultry Farm & Egg Business Management

EggFlow is a lightweight MVP that helps a small egg-producing poultry farm improve
profitability, reduce waste, manage egg inventory, track daily production, control
feed costs, and organize customer orders — from a phone, in under 5 minutes a day.

> **Status:** MVP prototype (single-page web app, no backend). Ships with clearly
> labeled **mock data for a small farm in El Salvador** so every feature can be
> explored immediately. Mock data is sample-only and is never presented as a real
> business result.

---

## 1. Business problem and target users

Small egg farms lose money invisibly: broken/rejected eggs are not quantified,
inventory doesn't match reality, feed cost is never tied back to each egg, and
orders slip because nobody knows real stock. Decisions on pricing, feed purchases,
and customer priorities become guesswork.

**Target users:** owner-operators and workers of small poultry farms
(~100–2,000 laying hens) selling eggs directly to shops, markets, and neighbors.

## 2. Goals and scope

**Goals**
- One simple daily record that captures production, quality, sales, and feed.
- A dashboard that answers: *did we make money today, and where did we lose it?*
- Measurable baselines for breakage, feed cost per egg, and order fulfillment.

**Non-goals (v1)**
- No accounting system, invoicing, or payroll.
- No IoT/sensors or automated data capture.
- No external messages or financial actions without explicit human approval.

## 3. MVP features

| Module | What it does |
|---|---|
| A. Daily production | Log eggs collected, broken, rejected; computes saleable count & %; daily/weekly comparison. |
| B. Inventory & sales | Stock by tray/carton/unit; order entry deducts confirmed sales exactly once; low-stock and unfulfillable-order flags. |
| C. Feed & costs | Feed purchases vs. consumption; other expenses; feed cost per egg and operating cost per saleable tray. |
| D. Dashboard | Production, saleable %, damaged, stock, revenue, feed use, expenses; anomaly highlights; daily ops report. |
| E. Alerts | In-dashboard alert recommendations (low stock, abnormal production, excess breakage, feed shortage). **Display only — nothing is sent externally.** |

## 4. Requirements

**Functional**
- FR-1: Record daily eggs collected / broken / rejected; reject impossible values (negatives, broken+rejected > collected).
- FR-2: Compute saleable eggs = collected − broken − rejected, and saleable %.
- FR-3: Track inventory in units, cartons (12), and trays (30); never let inventory go negative silently.
- FR-4: Record orders with quantity, price, and status; deduct stock only when a sale is confirmed, exactly once.
- FR-5: Record feed purchases (quintales/bags) and daily consumption; compute feed cost per egg.
- FR-6: Produce a daily operations report and flag anomalies.

**Non-functional**
- NFR-1: Responsive, usable on a 375px-wide phone.
- NFR-2: Zero cost to run: static HTML/CSS/JS, opens from any browser.
- NFR-3: Data persists in the browser (localStorage); exportable.
- NFR-4: No credentials, customer PII, or real prices committed to this repo.

## 5. Data definitions and calculations

- **Saleable eggs** = collected − broken − rejected
- **Saleable %** = saleable / collected × 100
- **Breakage rate** = broken / collected × 100
- **Feed cost per egg** = (feed consumed in lbs × price per lb) / eggs collected
- **Operating cost per saleable tray** = (feed cost + other daily expenses) / saleable trays
- **Gross margin** = revenue − feed cost − other operating costs (only when all inputs are recorded; otherwise shown as *insufficient data*)
- Collected ≠ saleable ≠ sold · inventory ≠ confirmed sales · revenue ≠ profit · feed purchased ≠ consumed · actuals ≠ estimates — the app keeps these strictly separate and labels every estimate.

## 6. Architecture

Single-page **HTML/CSS/JavaScript** app (`index.html`). No build step, no server.
Data is entered via validated forms, stored in `localStorage`, validated on write,
and rendered to the dashboard from the same records (single source of truth in the
app). Backup path: browser data export; future path: Google Sheets as the shared
data store (planned, not yet implemented).

## 7. Setup and testing

1. Clone the repo and open `index.html` in any browser — that's it.
2. The app seeds **mock data for a sample farm in El Salvador** (prices in USD,
   trays of 30, feed by the quintal/100-lb bag) on first run, clearly marked as
   sample data. Use "Reset demo data" to regenerate or "Clear data" to start empty.
3. Manual test plan: add a production day → verify saleable % and dashboard update;
   confirm a sale → verify stock deducted once; attempt an over-sale → verify the
   unfulfillable warning; log feed → verify cost per egg.

## 8. Measurable success criteria

Baselines must come from the farm's real records before targets are set (the mock
data illustrates the metrics; it is not a baseline):

- Egg breakage/rejection rate
- Feed cost per egg
- Inventory accuracy (system vs. physical count)
- Unfulfilled customer orders
- Daily record completion %
- Operating cost per saleable tray
- Gross margin / operating profit (when data exists)

## 9. Current status and limitations

- ✅ Repo, README, and MVP prototype with mock El Salvador data.
- ⚠️ localStorage only — data lives in one browser; no multi-device sync yet.
- ⚠️ Alerts are in-dashboard only; no external notifications.
- ⚠️ No real farm baseline yet — real numbers must replace the mock data.
- ❌ No Google Sheets integration yet (planned follow-up).

## License

MIT (proposed).
