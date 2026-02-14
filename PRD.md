# Product Requirements Document (PRD)
# Day Trading Journal - TradeTracker

## 1. Product Overview

**Product Name:** TradeTracker (working title)
**Product Type:** Web-based day trading journal and analytics platform
**Target Users:** Active day traders (futures, stocks, options, forex, crypto)
**Monetization:** Freemium SaaS (free trial → paid subscription tiers)

### Vision
An all-in-one trading journal that automatically syncs trades from brokers, provides deep performance analytics, and helps traders identify patterns in their behavior to consistently improve. Comparable to Tradezella but with a focus on speed, clean UX, and actionable insights.

### Current State
The project already has a working foundation:
- Node.js/Express backend with MongoDB
- React frontend with Webpack bundling
- User auth (signup/login/sessions/change password)
- Full trade CRUD (create, read, update, delete)
- Tradovate API integration with encrypted credential storage and auto-sync
- Basic dashboard with P/L calendar, stats, and analytics page
- Screenshot attachment with annotation tools (pen, arrow, text, color picker)
- Trial/premium subscription system

---

## 2. Core Features (MVP - Already Partially Built)

### 2.1 Auto-Sync Trade Import via Broker API
**Status:** Tradovate complete, others planned

Automatically pull trades from connected broker accounts so traders never have to manually log trades.

**Requirements:**
- [x] Tradovate API integration (demo + live environments)
- [x] Encrypted credential storage (AES-256-GCM)
- [x] Auto-sync on dashboard load with new trade notifications
- [x] Manual sync trigger from settings
- [x] Duplicate prevention via order ID indexing
- [ ] **Interactive Brokers** integration (Client Portal API / TWS API)
- [ ] **TD Ameritrade / Charles Schwab** integration
- [ ] **Webull** integration
- [ ] **NinjaTrader** integration
- [ ] **Robinhood** integration
- [ ] **TopStep / Apex** prop firm integration
- [x] CSV/Excel manual import as fallback for unsupported brokers
- [ ] Multi-account support (connect unlimited accounts, unified dashboard)
- [ ] Sync status indicators per account (last sync time, error states)
- [ ] Background sync scheduling (configurable intervals)

### 2.2 P/L Calendar
**Status:** Basic version complete

A monthly calendar view showing daily profit/loss with color coding.

**Requirements:**
- [x] Monthly calendar grid with daily P/L values
- [x] Green/red color coding for profit/loss days
- [x] Month-to-month navigation
- [x] Click on a day to expand and see individual trades for that day
- [x] Number of trades per day listed on the calendar.
- [ ] Weekly P/L summary row at bottom of each week
- [ ] Monthly P/L total displayed prominently
- [x] Heat map intensity (darker green = bigger win, darker red = bigger loss)
- [ ] Toggle between Gross P/L and Net P/L (after commissions/fees)
- [x] Year view option (12-month grid with monthly totals)
- [ ] Breakeven days shown in neutral color (gray/yellow)

### 2.3 Dashboard Statistics
**Status:** Basic version complete

At-a-glance performance overview on the main dashboard.

**Requirements:**
- [x] Total P/L, win rate, average win/loss
- [x] Total trades, wins, losses
- [x] Average trade duration
- [x] Best/worst trade
- [x] Profit factor
- [x] Win/loss streaks
- [x] Date range filter (today, this week, this month, this year, custom range)
- [ ] Account filter (filter stats by specific broker account)
- [x] Ticker/symbol filter
- [ ] Gross vs. Net P/L toggle
- [x] Equity curve chart on dashboard
- [ ] Daily P/L bar chart (last 30 days)
- [ ] Comparison to previous period (e.g., "up 15% vs last month")

### 2.4 Trade List Page
**Status:** Basic version complete

A comprehensive, filterable, sortable table of all trades.

**Requirements:**
- [x] Table displaying all trades with key columns
- [x] Filter by ticker, date range
- [x] Sort by date, ticker, P/L
- [x] Edit trade functionality
- [x] Delete trade functionality
- [ ] Bulk actions (delete multiple, tag multiple, export selected)
- [ ] Column customization (show/hide columns)
- [ ] Pagination or infinite scroll for large datasets
- [ ] Quick inline editing (click cell to edit)
- [ ] Trade detail side panel (click row to expand details without leaving list)
- [x] Filter by: setup type, tag, side (long/short), win/loss, source (manual/synced)
- [ ] Search bar for quick ticker lookup
- [ ] Export to CSV/Excel

### 2.5 Trade Entry & Editing
**Status:** Basic version complete

**Requirements:**
- [x] Manual trade entry form (ticker, entry/exit time & price, quantity, comments)
- [x] Manual P/L override option
- [x] Screenshot paste from clipboard with annotation tools
- [ ] Long/short side selector
- [ ] Commission/fees field
- [ ] Setup type / strategy tag (dropdown, user-defined)
- [ ] Mistake tags (e.g., "FOMO", "Oversize", "No stop loss", "Revenge trade")
- [ ] Emotional state tag (confident, fearful, greedy, neutral, tilted)
- [ ] Trade rating (1-5 stars for execution quality)
- [ ] Risk metrics: stop loss price, take profit target, planned R:R
- [ ] Multiple screenshot attachments per trade
- [ ] Trade notes with rich text (bold, italic, bullet points)

---

## 3. Advanced Analytics Page (Deep Dive)

A dedicated page for in-depth statistical analysis and performance breakdowns. This is the core value proposition - turning raw trade data into actionable insights.

### 3.1 Performance Metrics (50+ Reports)

**Profitability Metrics:**
- Total P/L (gross and net)
- Average winning trade / Average losing trade
- Average trade P/L
- Profit factor (gross profit / gross loss)
- Trade expectancy (expected value per trade)
- Return on investment (ROI)
- Payoff ratio (avg win / avg loss)

**Trade Counts:**
- Total trades
- Winning / Losing / Breakeven trades
- Win rate percentage
- Long wins vs. short wins breakdown

**Streak Analysis:**
- Max consecutive wins / losses
- Current streak
- Max consecutive winning days / losing days
- Average streak length

**Hold Time Analysis:**
- Average hold time (all trades)
- Average hold time (winners vs. losers)
- Average hold time (scratch/breakeven trades)
- P/L distribution by hold time ranges

**Daily Performance:**
- Total trading days
- Winning / Losing / Breakeven days
- Average daily P/L
- Best day / Worst day
- Average daily volume (contracts/shares)

**Risk Metrics:**
- Average planned R-multiple
- Average realized R-multiple
- Maximum drawdown (peak-to-trough)
- Maximum drawdown duration
- Sharpe ratio (if applicable)
- Risk of ruin estimate

**Cost Analysis:**
- Total commissions paid
- Total fees/swap
- Commission as % of gross P/L
- Net P/L after all costs

### 3.2 Visual Charts & Graphs

- **Equity Curve:** Cumulative P/L over time (line chart)
- **Daily P/L Bar Chart:** Green/red bars per trading day
- **Win Rate Over Time:** Rolling win rate (e.g., last 20 trades)
- **P/L Distribution Histogram:** Bell curve of trade outcomes
- **Performance by Ticker:** Bar chart of P/L per symbol
- **Performance by Day of Week:** Which days are most profitable
- **Performance by Time of Day:** Which hours produce best results (market session heatmap)
- **Performance by Trade Duration:** Short holds vs. long holds
- **Drawdown Chart:** Visualize drawdown periods
- **Monthly Performance Bar Chart:** Month-over-month comparison
- **R-Multiple Distribution:** Histogram of R-multiples achieved
- **Volume vs. P/L Scatter Plot:** Does sizing affect performance?

### 3.3 Breakdown & Filtering

All analytics should be filterable by:
- Date range (preset + custom)
- Ticker / symbol
- Account / broker
- Side (long / short)
- Setup type / strategy
- Tags (mistake tags, custom tags)
- Day of week
- Time of day range

### 3.4 Comparative Analysis

- Compare two time periods side by side
- Compare performance across different strategies/setups
- Compare long vs. short performance
- Before/after analysis (e.g., "performance since I started using stop losses")

---

## 4. Playbook / Strategy System

Inspired by Tradezella's Playbook feature. Lets traders define their strategies with specific rules and track how well they follow and execute each one.

### 4.1 Playbook Creation

- Name and describe each trading strategy/setup
- Define entry criteria (checklist of conditions)
- Define exit criteria (stop loss rules, profit target rules)
- Define position sizing rules
- Attach example screenshots of ideal setups
- Set risk parameters per playbook (max risk per trade, max daily loss)

### 4.2 Playbook Tracking

- Tag trades with the playbook/strategy used
- Track win rate per playbook
- Track P/L per playbook
- Track expectancy per playbook
- Track rule adherence (did you follow your own rules?)
- Identify which playbooks are profitable and which aren't
- Playbook-specific analytics dashboard

### 4.3 Rule Adherence Scoring

- After each trade, rate how well you followed the playbook rules
- Track adherence over time
- Correlate rule-following with profitability
- Alert when deviating from playbook rules frequently

---

## 5. Daily Journal & Notes

A structured journaling system that goes beyond individual trade comments.

### 5.1 Pre-Market Plan

- Morning journal template (customizable)
- Market outlook / bias notes
- Key levels to watch
- News/catalyst notes
- Daily goals and rules
- Max loss limit for the day
- Emotional check-in before trading

### 5.2 Post-Market Recap

- End-of-day reflection template
- What went well / what went poorly
- Lessons learned
- Link to specific trades from the day
- Rate overall day execution (1-5 stars)
- Emotional state throughout the day

### 5.3 Journal Features

- Rich text editor with formatting
- Attach images / screenshots
- Tag journal entries
- Search through past journal entries
- Calendar view of journal entries (separate from P/L calendar)

---

## 6. Suggested Additional Features

### 6.1 Trade Replay
Re-watch your trades play out tick-by-tick on a price chart.

- Replay any synced trade with historical price data
- Adjustable playback speed (0.5x, 1x, 2x, 5x, 10x)
- Overlay entry/exit points on chart
- Annotate specific moments during replay
- Tag mistakes or good decisions at specific timestamps
- Multi-timeframe chart support during replay
- **Data source:** Use free historical data APIs (Polygon.io, Alpha Vantage, or exchange data)

### 6.2 Zella Score Equivalent (Trader Score)
A composite performance rating that gamifies improvement.

- 0-100 score based on:
  - Consistency (low variance in daily P/L)
  - Win rate trends (improving or declining)
  - Risk management (following stop losses, R-multiple discipline)
  - Rule adherence (playbook compliance)
  - Journaling consistency (logging pre/post-market notes)
- Track score over time
- Breakdown of score components
- Milestones and badges for achievements

### 6.3 Risk Management Dashboard
Dedicated section focused on risk analysis.

- Real-time daily P/L tracker with max loss alerts
- Position sizing calculator
- Risk per trade as % of account
- Daily/weekly/monthly drawdown tracking
- Max drawdown alerts (configurable thresholds)
- Risk of ruin calculator
- Monte Carlo simulation (project future outcomes based on current stats)
- Account balance tracking over time

### 6.4 Accountability & Habit Tracker
Track daily trading habits and discipline.

- Customizable daily checklist:
  - Did I set a max loss for today?
  - Did I review my watchlist?
  - Did I follow my stop losses?
  - Did I journal pre-market?
  - Did I journal post-market?
  - Did I avoid revenge trading?
- Habit streak tracking
- Correlation between habits completed and daily P/L
- Weekly/monthly habit adherence percentage

### 6.5 AI-Powered Insights
Use AI/ML to surface patterns the trader might miss.

- Pattern detection: "You tend to lose money on Fridays" or "Your win rate drops after 3 consecutive wins"
- Behavioral alerts: "You're trading more aggressively than your baseline today"
- Setup analysis: "Your best setups have X, Y, Z characteristics"
- Optimal trade time suggestions based on historical performance
- Anomaly detection for unusual trading behavior
- Natural language trade summaries (weekly/monthly AI-generated reports)
- **Implementation:** Can use Claude API or local LLM for analysis

### 6.6 Social & Community Features

- **Mentor Mode / Spaces:** Share your journal (read-only) with a mentor or trading group
- **Leaderboards:** Opt-in anonymous leaderboards by win rate, consistency score, etc.
- **Trade sharing:** Share individual trades (with chart + notes) to a social feed
- **Groups:** Create or join trading communities within the platform
- **Copy insights:** See aggregated (anonymous) stats from top performers

### 6.7 Backtesting Engine
Test strategies against historical data without risking real money.

- Define entry/exit rules
- Run against historical price data
- Generate performance report for backtested strategy
- Compare backtested results to live results for the same strategy
- Save and iterate on backtested strategies

### 6.8 Notifications & Alerts

- Daily P/L limit reached (stop trading alert)
- Weekly performance summary email/push notification
- Consecutive loss alert ("You've lost 3 in a row, consider stepping away")
- Sync failure alerts
- Milestone notifications ("You just hit 60% win rate this month!")

### 6.9 Data Export & Reporting

- Export trades to CSV / Excel / PDF
- Generate formatted performance reports (PDF) for:
  - Tax preparation (Schedule D compatible)
  - Prop firm evaluations
  - Personal records
- Customizable report templates
- Scheduled report generation (weekly/monthly email)

### 6.10 Multi-Platform Support

- **Progressive Web App (PWA)** for mobile access
- **Dark mode / Light mode** toggle
- **Mobile-responsive** design for on-the-go trade logging
- Offline support with sync when back online

### 6.11 Prop Firm Tracking
Dedicated features for funded/prop firm traders.

- Track multiple prop firm accounts separately
- Prop firm rule tracking (max daily loss, max drawdown, profit targets)
- Progress bar toward profit target / evaluation goals
- Alert when approaching rule violations
- Support for popular prop firms: TopStep, Apex, FTMO, MyFundedFX

### 6.12 Webhook & Automation Integration

- Incoming webhooks (receive trades from TradingView alerts, custom scripts)
- Outgoing webhooks (trigger actions when trades are logged)
- Discord bot integration (post daily P/L to a Discord channel)
- Zapier/Make integration for custom workflows

---

## 7. Technical Architecture

### 7.1 Current Stack (Keep & Extend)
| Layer        | Technology                        |
|-------------|-----------------------------------|
| Frontend    | React 19 + Webpack 5              |
| Backend     | Node.js + Express 5               |
| Database    | MongoDB + Mongoose                |
| Auth        | bcrypt + express-session           |
| Encryption  | AES-256-GCM (for API credentials) |
| Templates   | Handlebars (server-side shells)    |

### 7.2 Recommended Additions
| Need                  | Technology                              |
|----------------------|----------------------------------------|
| Charts & Graphs      | Chart.js, Recharts, or Lightweight Charts (TradingView) |
| Real-time Updates     | WebSockets (Socket.io) for live sync   |
| Job Scheduling        | node-cron or Bull queue (background sync) |
| File Storage          | AWS S3 or Cloudinary (screenshots, move off base64) |
| Caching               | Redis (session store, API rate limiting) |
| Email                 | SendGrid or Resend (notifications, reports) |
| PDF Generation        | Puppeteer or jsPDF (export reports)    |
| AI/Insights           | Claude API or OpenAI API               |
| Search                | MongoDB Atlas Search or Elasticsearch  |
| Mobile                | PWA with service workers               |

### 7.3 Database Schema Extensions

**Trade Model (additions):**
```
side:            String (enum: 'long', 'short')
commission:      Number (default: 0)
fees:            Number (default: 0)
setupType:       String (references Playbook)
tags:            [String] (custom tags array)
mistakeTags:     [String] (predefined mistake categories)
emotionalState:  String (enum: 'confident', 'fearful', 'greedy', 'neutral', 'tilted')
tradeRating:     Number (1-5, execution quality rating)
stopLoss:        Number (planned stop loss price)
takeProfit:      Number (planned take profit price)
plannedRR:       Number (planned risk:reward ratio)
rMultiple:       Number (realized R-multiple)
playbook:        ObjectId (ref: 'Playbook')
ruleAdherence:   Number (0-100, how well rules were followed)
```

**New Models:**
```
Playbook: { name, description, entryCriteria, exitCriteria, sizingRules,
            riskParams, exampleScreenshots, owner, createdDate }

JournalEntry: { date, type (pre-market/post-market/general), content,
                attachments, tags, dayRating, emotionalLog, owner, createdDate }

HabitChecklist: { date, items: [{ label, completed }], owner }

BrokerAccount: { broker, nickname, credentials (encrypted), environment,
                 lastSyncTime, syncEnabled, owner }

Notification: { type, message, read, owner, createdDate }
```

---

## 8. Implementation Roadmap

### Phase 1: Foundation Enhancement (Current → 4 weeks)
1. Refine existing dashboard, calendar, and trade list
2. Add date range filtering across all views
3. Add trade side (long/short), commission/fees fields
4. Add tags and mistake tags to trades
5. Implement trade rating system
6. Improve trade list with pagination, search, column customization
7. Add CSV/Excel import capability
8. Move screenshots from base64 to file storage (S3/Cloudinary)

### Phase 2: Advanced Analytics (4-8 weeks)
1. Build comprehensive analytics page with 50+ metrics
2. Implement all charts (equity curve, distribution, breakdowns, etc.)
3. Add performance-by filters (ticker, day of week, time of day, duration)
4. Add comparative analysis (period vs. period)
5. Implement Gross vs. Net P/L toggle
6. Add data export (CSV, Excel, PDF)

### Phase 3: Journaling & Playbooks (8-12 weeks)
1. Build daily journal system (pre-market / post-market templates)
2. Implement Playbook CRUD and strategy tagging
3. Build playbook analytics dashboard
4. Add rule adherence tracking
5. Build habit/accountability tracker
6. Implement Trader Score system

### Phase 4: More Broker Integrations (12-16 weeks)
1. Interactive Brokers integration
2. MetaTrader 4/5 import
3. NinjaTrader integration
4. Webull / Robinhood integration
5. Crypto exchange integrations (Binance, Bybit)
6. Multi-account management UI

### Phase 5: Advanced Features (16-24 weeks)
1. Trade replay with historical charts
2. AI-powered insights and pattern detection
3. Risk management dashboard with alerts
4. Notification system (in-app + email)
5. Prop firm tracking module
6. Webhook integrations

### Phase 6: Social & Polish (24+ weeks)
1. Mentor mode / journal sharing
2. Community features
3. PWA / mobile optimization
4. Dark mode / theming
5. Backtesting engine
6. Discord bot integration

---

## 9. Competitive Advantages to Target

| vs. Tradezella                        | Our Advantage                              |
|--------------------------------------|--------------------------------------------|
| $29-49/month, no free trial          | Generous free tier or lower pricing         |
| No mobile app                        | PWA from day one                           |
| Limited to 38 brokers               | CSV import fallback + webhook intake        |
| Trade replay only on premium         | Include replay in base tier                 |
| No AI insights yet (coming soon)     | Ship AI-powered analysis early              |
| No webhook/automation support        | TradingView webhook + Discord integration   |
| No prop firm rule tracking           | Built-in prop firm evaluation tracker       |

---

## 10. Success Metrics

- **User Acquisition:** Monthly signups, trial-to-paid conversion rate
- **Engagement:** Daily active users, trades logged per user per week, journal entries per user
- **Retention:** 30/60/90 day retention rates, churn rate
- **Performance:** Page load time < 2s, sync latency < 5s, 99.9% uptime
- **Revenue:** MRR, ARPU, LTV, CAC payback period

---

## 11. Open Questions

1. **Pricing model:** What should the free tier include vs. paid tiers? How many tiers?
2. **Data storage:** Self-hosted MongoDB vs. MongoDB Atlas? AWS vs. other cloud?
3. **Historical data source:** Which provider for trade replay charts? (Polygon.io, Alpha Vantage, exchange feeds)
4. **AI provider:** Claude API vs. OpenAI vs. self-hosted model for insights?
5. **Branding:** Final product name, domain, design language?
6. **Legal:** Privacy policy, terms of service, data handling compliance (financial data)?
