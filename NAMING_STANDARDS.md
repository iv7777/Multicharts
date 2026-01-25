# Project Morpheus - Naming Standards

## Timeframe Suffixes

All multi-timeframe variables use consistent suffixes:

- `_1M` = 1-minute (current chart - Data1)
- `_5M` = 5-minute (Data5)
- `_15M` = 15-minute (Data4)
- `_1H` = 1-hour (Data3)
- `_D` = Daily (Data2)

## Current Bar Suffix

- `_Cur` = Current bar calculation (vs historical closed bar)

**Example**: `SMA1_1H` = closed 1-hour bar, `SMA1_1H_Cur` = current updating 1-hour bar

## Variable Prefixes

### Boolean Flags

- `Is` = State/condition
  - Examples: `IsBullPhase_D`, `IsStrongBull_1H`, `Is_SMAStranded`
- `Has` = Occurrence/event
  - Examples: `Has_GapDown`, `Has_OSSupport_15M`, `Has_SharpDecline_D`
- `Can` = Permission/capability
  - Examples: `Can_GoLong`, `Can_TrendLong`, `Can_CounterLong`

### Numeric Variables

- `Count_` = Counter variable (incremental)
  - Examples: `Count_AboveSMA1_1M`, `Count_CloseHigher`
- `Num_` = Number/index (specific value or bar number)
  - Examples: `Num_KDCrossUp_15M`, `Num_HighBar`, `Num_StartupBar`
- `Threshold_` = Fixed threshold value
  - Examples: `Threshold_Stoch_OB`, `Threshold_PanicDecline`
- `Coeff_` = Calculation coefficient (multiplier)
  - Examples: `Coeff_MaxDistSMA12`, `Coeff_MinDevSMA14_D`
- `Limit_` = Calculated limit (derived from coefficient)
  - Examples: `Limit_MaxDistSMA12_1M`, `Limit_MinDevSMA14_D`
- `Len_` = Length parameter for indicators
  - Examples: `Len_SMA1`, `Len_Stoch`, `Len_SMI1`

### Price/Market Data

- `High_`, `Low_`, `Open_`, `Close_` = OHLC data
  - Examples: `High_RecentDay`, `Low_Cycle_1M`, `Close_D`
- `Range_` = Price range
  - Examples: `Range_RecentDay`, `Avg_PriceRange`
- `Volume_` = Volume data
  - Examples: `Volume_D`, `Volume_Avg_1H`

### Indicator Components

Pattern: `Indicator_Component_Timeframe[_Cur]`

**SMA Examples**:
- `SMA1_1H` = SMA(21) on 1-hour closed bar
- `SMA2_15M_Cur` = SMA(50) on current 15-minute bar
- `SMA1_Slope_D` = Slope of SMA1 on Daily
- `SMA1_SlopeMA_1H` = Smoothed slope of SMA1 on 1-hour
- `SMA1_SlopeROC_15M` = Rate of change of SMA1 slope on 15-minute

**Stochastic Examples**:
- `Stoch_SlowK_15M` = Stochastic SlowK on 15-minute
- `Stoch_SlowD_1H_Cur` = Stochastic SlowD on current 1-hour bar

**SMI Examples**:
- `SMI_1H` = Stochastic Momentum Index on 1-hour
- `SMI_15M_Cur` = SMI on current 15-minute bar

### Entry/Exit Variables

- `Entry_` = Entry signal variables
  - Examples: `Entry_Technical`, `Entry_Timeframe`, `Entry_GapDown`
- `Exit_` = Exit management
  - Examples: `Exit_Strategy_ID`
- `Flag_` = Control flags
  - Examples: `Flag_PrintSMA14Dev`, `Flag_NoEODBuy`

### Data Proxies

To avoid repeated `BarStatus(X)` calls, use data proxy variables:

```
Open_D = Open of Data2
High_D = High of Data2
Low_D = Low of Data2
Close_D = Close of Data2
Volume_D = Volume of Data2
CurrentBar_D = CurrentBar of Data2
BarStatus_D = BarStatus(2)
```

## Naming Pattern Examples

### Good Examples ✅
```
IsBullPhase_D           // Boolean state on Daily
Can_TrendLong           // Permission for trend-following long
Has_SharpDecline_D      // Occurrence flag on Daily
Count_AboveSMA1_1M      // Counter on 1-minute
Num_KDCrossUp_15M       // Bar number of cross on 15-minute
SMA1_Slope_1H_Cur       // Current slope on 1-hour
Threshold_PanicDecline  // Fixed threshold
Limit_MaxDist_D         // Calculated limit on Daily
```

### Bad Examples ❌
```
Value1, Value2          // Not descriptive
BullPhase               // Missing timeframe suffix
SMA_1H                  // Missing number (SMA1, SMA2, etc.)
CrossBar                // Missing timeframe and indicator
MaxDist                 // Missing timeframe
```

## Code Organization Principles

### Section Headers
Use clear section headers with separators:
```
{ ============================================
  SECTION X: DESCRIPTIVE NAME
  ============================================ }
```

### Variable Grouping
Group related variables with comment headers:
```
{ System & Control }
{ Thresholds & Limits }
{ Phase Detection Flags }
{ SMA Values - 1 Minute }
```

### Comments
- Use inline comments for complex logic
- Explain WHY, not just WHAT
- Document assumptions and edge cases

### Consistency
- Always use the same pattern for similar variables across timeframes
- If you have `SMA1_1M`, also use `SMA1_5M`, `SMA1_15M`, `SMA1_1H`, `SMA1_D`
- Keep indicator component order consistent: `Indicator_Component_Timeframe[_Cur]`

## PowerLanguage Specifics

- **Case Insensitive**: PowerLanguage is case-insensitive, but capitalize keywords for readability
- **Descriptive Over Terse**: Use `Count_AboveSMA1_1M` instead of `Cnt1M`
- **No Reserved Words**: Avoid `Value1`, `Value2` except for temporary calculations
- **Explicit Over Implicit**: `Close_D` is clearer than `Close of Data2` in logic