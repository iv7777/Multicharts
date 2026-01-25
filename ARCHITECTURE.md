# Project Morpheus - Strategy Architecture

## Overview

The strategy is organized into 23 distinct sections, each handling specific aspects of calculation, analysis, and execution. The code follows a strict top-down flow from data initialization through execution.

## Section Breakdown

### Initialization & Setup (Sections 1-2)
- **Section 1**: Variable naming standards (documented in header)
- **Section 2**: Initialization & constants
  - Startup bar calculation
  - Data proxy initialization for all timeframes

### Calculations (Sections 3-8)
- **Section 3**: SMA calculations across all 5 timeframes
  - Historical values (closed bars)
  - Current values (`_Cur` suffix for updating bars)
- **Section 4**: Basic parameters & indicators
  - Price normalization factor
  - Stochastic oscillator
  - Dynamic limits based on coefficients
- **Section 5**: High/Low/Open tracking within higher timeframe bars
- **Section 6**: Oscillators & momentum
  - Momentum indicator
  - Volatility percentage
  - SMI (Stochastic Momentum Index)
  - Volume analysis
  - Chaikin Oscillator
- **Section 7**: SMA slopes & smoothing
  - CMO-based slope calculations
  - LinearReg smoothing (SlopeMA)
  - Rate of change (SlopeROC)
  - All 5 timeframes
- **Section 8**: Multi-timeframe calculations
  - Recent day range tracking
  - Higher timeframe SMI
  - Higher timeframe Stochastic
  - SMA stranded detection

### Analysis (Sections 9-17)
- **Section 9**: Bar counters
  - Consecutive bars above/under SMAs
  - Slope direction counters
  - Close higher counters
- **Section 10**: Cross detection
  - Stochastic K/D crosses
  - SMI threshold crosses
  - Oversold/Overbought crosses
- **Section 11**: Support & resistance
  - SMA level identification
- **Section 12**: Swing high/low calculation
  - Recent swing detection
  - Low after high tracking
- **Section 13**: Cycle high/low tracking
  - Dynamic cycle boundaries per timeframe
- **Section 14**: Dynamic distance calculation
  - Ratio-based limit adjustments
- **Section 15**: Phase detection
  - Bull/Bear phase determination
  - Strong Bull/Bear identification
  - Multi-timeframe phase aggregation
- **Section 16**: Long/Short permission logic
  - **Can_TrendLong/Can_TrendShort**: Trend-following permissions
  - **Can_CounterLong/Can_CounterShort**: Counter-trend permissions
  - **Can_GoLong/Can_GoShort**: Composite permissions
- **Section 17**: Condition flags
  - Oversold support detection
  - Quick oversold conditions
  - Bullish reversal patterns
  - Sandwich patterns
  - Sharp decline detection (counter-trend trigger)

### Entry Logic (Sections 18-20)
- **Section 18**: Entry - Trend Following (ID 100-199)
  - ID 101: SMA Deviation entry
  - ID 103: Extreme Oversold entry
  - Higher timeframe confirmation logic
  - Tight support detection
- **Section 19**: Entry - Mean Reversion (ID 200-299)
  - ID 201: Daily Panic Bounce (counter-trend)
  - Multi-timeframe reversal confirmation
- **Section 20**: Entry - Breakout (ID 300-399)
  - Reserved for future breakout strategies
- **Section 20.1**: Entry - Special Logic (ID 900+)
  - ID 901: Gap Down recovery
  - End of day buy rules

### Exit & Execution (Sections 21-23)
- **Section 21**: Dynamic Exit Manager
  - Volatility-based exit switching
  - Trend collapse detection
  - Automatic Exit_Strategy_ID updates
- **Section 22**: Exit Strategy Library & Execution
  - **Exit Type 1**: Standard trailing stop (trend trades)
  - **Exit Type 2**: Time-based exit (scalp trades)
  - **Exit Type 3**: Profit target + breakeven (mean reversion)
  - Global safety stop management
- **Section 23**: Entry Execution Engine
  - Trade count management
  - Time restrictions
  - Entry interval enforcement
  - Order placement

## Data Flow

```
┌─────────────────────────────────────────────────────────────┐
│ 1. DATA INITIALIZATION (Sections 2-3)                      │
│    • Load OHLCV for all 5 timeframes                       │
│    • Calculate SMAs (21, 50, 150, 200)                     │
│    • Create current bar estimates (_Cur variables)         │
└────────────────┬────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. INDICATOR CALCULATIONS (Sections 4-8)                   │
│    • Oscillators: Stochastic, SMI, Momentum                │
│    • Slopes: CMO-based with smoothing                      │
│    • Volume: Chaikin, averages                             │
│    • Volatility: Price range percentage                    │
└────────────────┬────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. PATTERN DETECTION (Sections 9-14)                       │
│    • Count bars above/below SMAs                           │
│    • Detect crosses (K/D, SMI thresholds)                  │
│    • Identify swings and cycles                            │
│    • Calculate dynamic limits                              │
└────────────────┬────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. PHASE & PERMISSION (Sections 15-17)                     │
│    • Determine Bull/Bear phases per timeframe              │
│    • Set Can_TrendLong/Can_TrendShort                      │
│    • Detect counter-trend triggers (Has_SharpDecline_D)    │
│    • Set Can_CounterLong/Can_CounterShort                  │
│    • Combine into Can_GoLong/Can_GoShort                   │
└────────────────┬────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. ENTRY EVALUATION (Sections 18-20)                       │
│    • Check trend-following setups (if Can_TrendLong)       │
│    • Check mean reversion setups (if Can_CounterLong)      │
│    • Check special conditions (gaps, EOD)                  │
│    • Set Entry_Technical ID and Exit_Strategy_ID           │
└────────────────┬────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────┐
│ 6. DYNAMIC EXIT MANAGEMENT (Section 21)                    │
│    • Monitor open positions                                │
│    • Switch exit strategies based on conditions            │
│    • Update Exit_Strategy_ID if needed                     │
└────────────────┬────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────┐
│ 7. EXIT EXECUTION (Section 22)                             │
│    • Route to appropriate exit strategy                    │
│    • Manage trailing stops, targets, time exits            │
│    • Place exit orders                                     │
└────────────────┬────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────┐
│ 8. ENTRY EXECUTION (Section 23)                            │
│    • Enforce trade limits and time restrictions            │
│    • Calculate position size                               │
│    • Place entry orders                                    │
│    • Update trade counters                                 │
└─────────────────────────────────────────────────────────────┘
```

## Key Design Decisions

### 1. Multi-Timeframe Architecture
**Decision**: Use 5 separate data series (1M, 5M, 15M, 1H, Daily)  
**Rationale**: Allows precise control over each timeframe's calculations and avoids look-ahead bias  
**Trade-off**: More complex code, but cleaner logic and better testability

### 2. Data Proxy Pattern
**Decision**: Create proxy variables (e.g., `Close_D`, `BarStatus_D`) instead of inline `of Data2` calls  
**Rationale**: Improves readability, reduces errors, makes refactoring easier  
**Trade-off**: More variable declarations, but significantly cleaner code

### 3. Current Bar Calculations
**Decision**: Maintain both closed bar and current bar (`_Cur`) versions of indicators  
**Rationale**: Enables real-time decision making while preserving historical accuracy  
**Implementation**: Manual calculation using formula: `(ClosedValue * Length - OldestBar + CurrentPrice) / Length`

### 4. Dual-Mode Permission System
**Decision**: Separate `Can_TrendLong` and `Can_CounterLong` instead of single `Can_GoLong`  
**Rationale**: Allows simultaneous trend-following and counter-trend strategies  
**Trade-off**: More complex permission logic, but enables sophisticated multi-strategy approach

### 5. Entry ID Ranges
**Decision**: Organize entries by strategy type (100s=Trend, 200s=MeanRev, 300s=Breakout, 900s=Special)  
**Rationale**: Easy to identify strategy type from trade logs  
**Trade-off**: None - pure organizational benefit

### 6. Dynamic Exit Management
**Decision**: Allow exit strategy switching mid-trade based on market conditions  
**Rationale**: Adapts to changing volatility and trend strength  
**Example**: Switch from trailing stop to quick target if volatility spikes

### 7. Coefficient-Based Limits
**Decision**: Define coefficients (e.g., `Coeff_MaxDist_D = 20`) and calculate limits dynamically  
**Rationale**: Easy to adjust thresholds across all timeframes proportionally  
**Implementation**: `Limit_MaxDist_D = Coeff_MaxDist_D / 1000 * SMA1_D`

## Known Limitations

### 1. PowerLanguage Constraints
- No recursion allowed
- Single return value from functions
- Limited array functionality (1-indexed, fixed size)
- No object-oriented programming

### 2. Performance Considerations
- 5 data series = 5x calculation overhead
- Slope calculations (CMO + LinearReg) are computationally expensive
- Current bar calculations add overhead on every tick

### 3. Look-Ahead Bias Prevention
- Must carefully check `BarStatus` before using current bar values
- Custom functions (MyCMO, MySMI, MyStochastic) required for accurate current bar calculations
- Cannot use future data in historical backtesting

### 4. Strategy Limitations
- Long-only by default (short logic present but disabled)
- Requires liquid instruments (designed for stocks/ETFs)
- Assumes regular trading hours (09:30-15:45)
- Not suitable for overnight positions (exits at EOD)

## Extension Points

### Adding New Entry Strategies
1. Choose appropriate ID range (200s for mean reversion, 300s for breakout)
2. Add condition flags in Section 17
3. Implement entry logic in appropriate section (18-20)
4. Set `Entry_Technical` and `Exit_Strategy_ID`

### Adding New Exit Strategies
1. Add new `Exit_Strategy_ID` value (4, 5, etc.)
2. Implement logic in Section 22
3. Update Dynamic Exit Manager (Section 21) if needed

### Adding New Timeframes
1. Add data series in MultiCharts
2. Create data proxy variables
3. Add SMA calculations
4. Add slope calculations
5. Add Stochastic/SMI calculations
6. Update phase detection
7. Add to permission logic

## Testing Recommendations

### Unit Testing Approach
- Test each section independently
- Use print statements to verify calculations
- Compare closed bar vs current bar values
- Validate cross detection logic

### Integration Testing
- Backtest on known market conditions
- Verify no look-ahead bias (compare real-time vs historical)
- Test edge cases (market open, close, gaps)
- Validate multi-timeframe synchronization

### Performance Testing
- Monitor calculation time per bar
- Profile expensive sections (slopes, oscillators)
- Optimize if execution time > 50ms per bar