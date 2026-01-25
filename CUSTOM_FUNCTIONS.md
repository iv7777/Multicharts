# Custom Functions - Project Morpheus

## Overview
MySignal strategy uses **10 custom functions** following the naming pattern: `Indicator_Cur_Timeframe`

These functions calculate current bar values for higher timeframes (Daily, 1-Hour, 15-Minute, 5-Minute) that update in real-time on the 1-minute chart.

## Function List

### CMO (Chande Momentum Oscillator) Functions

| Function | Purpose | Usage Lines |
|----------|---------|-------------|
| `CMO_Cur_D(Length)` | Daily CMO current bar value | 494, 499 |
| `CMO_Cur_1H(Length)` | 1-Hour CMO current bar value | 517, 522 |
| `CMO_Cur_15M(Length)` | 15-Minute CMO current bar value | 540, 545 |
| `CMO_Cur_5M(Length)` | 5-Minute CMO current bar value | 563, 568 |

### SMI (Stochastic Momentum Index) Functions

| Function | Purpose | Usage Line |
|----------|---------|------------|
| `SMI_Cur_5M(Length1, Length2, Length3)` | 5-Minute SMI current bar value | 618 |
| `SMI_Cur_1H(Length1, Length2, Length3)` | 1-Hour SMI current bar value | 619 |
| `SMI_Cur_15M(Length1, Length2, Length3)` | 15-Minute SMI current bar value | 620 |

### Stochastic Functions

| Function | Purpose | Usage Line |
|----------|---------|------------|
| `Stochastic_Cur_D(Length, SmoothK, SmoothD, FastK, FastD, SlowK, SlowD)` | Daily Stochastic current bar values | 627 |
| `Stochastic_Cur_1H(Length, SmoothK, SmoothD, FastK, FastD, SlowK, SlowD)` | 1-Hour Stochastic current bar values | 628 |
| `Stochastic_Cur_15M(Length, SmoothK, SmoothD, FastK, FastD, SlowK, SlowD)` | 15-Minute Stochastic current bar values | 629 |
| `Stochastic_Cur_5M(Length, SmoothK, SmoothD, FastK, FastD, SlowK, SlowD)` | 5-Minute Stochastic current bar values | 630 |

## Why These Functions Are Needed

**Standard functions limitation**: Built-in functions like `CMO()`, `SMI()`, and `Stochastic()` only return values for **closed bars**. On the current bar of a higher timeframe, they return the previous closed bar's value.

**Custom functions solution**: These functions calculate indicator values using the **current price action** of the unclosed higher timeframe bar, enabling real-time decision making.

## Usage Examples

### CMO Usage
```easylanguage
{ Closed bar value }
SMA1_Slope_D = CMO(Len_SMA1) of Data2;

{ Current bar value }
SMA1_Slope_D_Cur = CMO_Cur_D(Len_SMA1);
```

### SMI Usage
```easylanguage
{ Closed bar value }
SMI_1H = SMI(Len_SMI1, Len_SMI2, Len_SMI3) of Data3;

{ Current bar value }
SMI_1H_Cur = SMI_Cur_1H(Len_SMI1, Len_SMI2, Len_SMI3);
```

### Stochastic Usage
```easylanguage
{ Closed bar values }
Temp_Return = Stochastic(High_D, Low_D, Close_D, Len_Stoch, 3, 3, 1, 
                         Stoch_FastK_D, Stoch_FastD_D, Stoch_SlowK_D, Stoch_SlowD_D) of Data2;

{ Current bar values }
Temp_Return = Stochastic_Cur_D(Len_Stoch, 3, 3, 
                               Stoch_FastK_D_Cur, Stoch_FastD_D_Cur, 
                               Stoch_SlowK_D_Cur, Stoch_SlowD_D_Cur);
```

## Function Files

These functions should be located at:
```
d:\Git-Repository\Multicharts\
  CMO_Cur_D.Function
  CMO_Cur_1H.Function
  CMO_Cur_15M.Function
  CMO_Cur_5M.Function
  SMI_Cur_5M.Function
  SMI_Cur_1H.Function
  SMI_Cur_15M.Function
  Stochastic_Cur_D.Function
  Stochastic_Cur_1H.Function
  Stochastic_Cur_15M.Function
  Stochastic_Cur_5M.Function
```

## Summary Table

| Category | Daily | 1-Hour | 15-Min | 5-Min |
|----------|-------|--------|--------|-------|
| **CMO** | CMO_Cur_D | CMO_Cur_1H | CMO_Cur_15M | CMO_Cur_5M |
| **SMI** | - | SMI_Cur_1H | SMI_Cur_15M | SMI_Cur_5M |
| **Stochastic** | Stochastic_Cur_D | Stochastic_Cur_1H | Stochastic_Cur_15M | Stochastic_Cur_5M |

**Total: 10 custom functions**

## Naming Convention

Following Project Morpheus standards: `Indicator_Cur_Timeframe`
- **Indicator**: CMO, SMI, Stochastic
- **Cur**: Current (unclosed) bar calculation
- **Timeframe**: D, 1H, 15M, 5M

This matches the variable naming pattern used throughout the strategy (e.g., `SMA1_Slope_D_Cur`).
