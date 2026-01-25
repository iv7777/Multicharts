# Project Morpheus - Multi-Timeframe Trading Strategy

A sophisticated PowerLanguage trading strategy for MultiCharts that combines trend-following and counter-trend (mean reversion) approaches across multiple timeframes.

## Overview

**Platform**: MultiCharts 64-bit  
**Language**: PowerLanguage (EasyLanguage variant)  
**Primary Execution**: 1-minute bars (Data1)

## Strategy Features

### Dual-Mode Trading
- **Trend Following** (Entry IDs 100-199): Trades with the dominant trend using multi-timeframe confirmation
- **Mean Reversion** (Entry IDs 200-299): Captures violent bounces after panic selling conditions
- **Breakout** (Entry IDs 300-399): Reserved for future breakout strategies

### Multi-Timeframe Analysis
The strategy analyzes 5 timeframes simultaneously:
- **Data1**: 1-minute (execution timeframe)
- **Data2**: Daily (primary trend filter)
- **Data3**: 1-hour (intermediate trend)
- **Data4**: 15-minute (entry refinement)
- **Data5**: 5-minute (fine-tuning)

### Dynamic Exit Management
- **Exit Strategy 1**: Standard trailing stop (trend-following trades)
- **Exit Strategy 2**: Time-based exit (scalping)
- **Exit Strategy 3**: Profit target + breakeven (mean reversion)
- Automatic exit strategy switching based on market conditions (volatility spikes, trend reversals)

## Key Components

### Entry Strategies
- **ID 101**: Trend Follow - SMA Deviation (primary trend-following setup)
- **ID 103**: Trend Follow - Extreme Oversold (strong trend with pullback)
- **ID 201**: Mean Reversion - Daily Panic Bounce (counter-trend on sharp declines)
- **ID 901**: Special - Gap Down Recovery

### Technical Indicators
- Simple Moving Averages (21, 50, 150, 200 periods)
- Stochastic Oscillator (14-period)
- Stochastic Momentum Index (SMI)
- CMO-based slope calculations
- Volume analysis (Chaikin Oscillator)

### Risk Management
- Position sizing based on risk per trade
- Percentage-based stops (default 1.5%)
- Trailing stops with activation threshold
- Maximum daily trade limits
- Minimum time interval between entries

## Configuration

### Key Inputs
```
Input_AllowLong = True
Input_AllowShort = False
Input_AllowMeanReversion = True
Input_RiskPerTrade = 500
Input_StopPct = 0.015
Input_MaxTrades = 10
Threshold_PanicDecline = 0.06  // 6% for counter-trend triggers
```

### Trading Hours
- Start: 09:30
- End: 15:45
- Minimum entry interval: 5 minutes

## Architecture

See [ARCHITECTURE.md](ARCHITECTURE.md) for detailed component breakdown and data flow.

## Naming Standards

See [NAMING_STANDARDS.md](NAMING_STANDARDS.md) for variable naming conventions and code organization principles.

## Custom Functions Required

The strategy uses custom functions for multi-timeframe calculations:
- `MyCMODaily`, `MyCMO60Min`, `MyCMO15Min`, `MyCMO5Min` - CMO calculations
- `MySMI60Min`, `MySMI15Min`, `MySMI5Min` - SMI calculations  
- `MyStochasticDaily`, `MyStochastic60Min`, `MyStochastic15Min`, `MyStochastic5Min` - Stochastic calculations

## Development Notes

### PowerLanguage Specifics
- Uses `Begin/End` blocks (not braces)
- Semicolon required at end of statements
- Arrays are 1-indexed
- `of DataX` syntax for multi-data access
- BarStatus: 0=historical, 1=updating, 2=closed

### Code Organization
- Sectioned with clear headers (Sections 1-23)
- Data proxy variables to avoid direct `BarStatus(X)` calls
- Descriptive variable names following Project Morpheus standards
- Extensive inline comments for complex logic

## Version History

- **Latest**: Added counter-trend (mean reversion) capability with Entry ID 201
- Refactored permission logic to separate trend-following from counter-trend
- Implemented dynamic exit management system
- Added multi-timeframe slope calculations
