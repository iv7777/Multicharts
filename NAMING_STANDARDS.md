# Project Morpheus Naming Standards

## Timeframe Suffixes
- `_1M` = 1-minute
- `_5M` = 5-minute  
- `_15M` = 15-minute
- `_1H` = 1-hour
- `_D` = Daily

## Variable Prefixes
### Boolean Flags
- `Is` = State/condition (IsBullPhase_D)
- `Has` = Occurrence (Has_GapDown)
- `Can` = Permission (Can_GoLong)

### Numeric
- `Count_` = Counter variable
- `Num_` = Number/index  
- `Threshold_` = Fixed threshold
- `Coeff_` = Calculation coefficient
- `Limit_` = Calculated limit
- `Len_` = Length parameter

### Price/Market Data
- `High_`, `Low_`, `Open_`, `Close_`
- `Range_`, `Volume_`

PROJECT: Multi-Timeframe Trading Strategy - "Project Morpheus"

TECHNICAL SETUP:
- Platform: MultiCharts 64-bit [version]
- Language: PowerLanguage (EasyLanguage variant)
- Primary Execution: 1-minute bars (Data1)
- Data Series:
  * Data1: 1-minute (current chart, execution timeframe)
  * Data2: Daily (trend filter)
  * Data3: 60-minute (intermediate trend)
  * Data4: 15-minute (entry refinement)
  * Data5: 5-minute (fine-tuning)

NAMING CONVENTIONS (Project Morpheus Standards):
- Timeframe suffixes: _1M, _5M, _15M, _1H, _D
- Current bar suffix: _Cur (e.g., SMA1_1H_Cur)
- Boolean flags: Is/Has/Can prefixes
- Counters: Count_ prefix
- Thresholds: Threshold_ prefix
- Coefficients: Coeff_ prefix
- Calculated limits: Limit_ prefix
- See attached NAMING_STANDARDS.md for full details

CODE ORGANIZATION:
- Section headers with clear separation
- Comments explaining complex logic
- Functions for repeated calculations
- See attached strategy code for current architecture

POWERLANGUAGE SPECIFICS TO REMEMBER:
- Begin/End blocks (not braces)
- Semicolon required at end of statements
- Arrays are 1-indexed
- "of DataX" syntax for multi-data access
- BarStatus: 0=historical, 1=updating, 2=closed
- Functions return single value only
- No recursion allowed
- Case-insensitive but capitalize keywords

WHEN HELPING ME:
1. Always validate PowerLanguage syntax compatibility
2. Follow Project Morpheus naming standards
3. Maintain existing code architecture unless I request changes
4. Add section comments when creating new code blocks
5. Flag any potential look-ahead bias or BarStatus issues
6. Suggest testing approaches for changes
7. Balance readability with performance

RESPONSE FORMAT:
- Brief summary (what does this do?)
- Complete, compilable code
- Key changes/additions explained
- Testing recommendations
- Any warnings or considerations

MY PREFERENCES:
- Verbose comments for complex logic
- Descriptive variable names (not Value1, Value2)
- Explicit over implicit
- Explain trade-offs when there are multiple approaches
```

**📄 STRATEGY_CODE.txt**
```
[Your complete refactored strategy code]
```

**📄 CUSTOM_FUNCTIONS.txt**
```
List of custom functions used:
- MyCMODaily(Length)
- MyCMO60Min(Length)  
- MyCMO15Min(Length)
- MyCMO5Min(Length)
- MySMI60Min(Len1, Len2, Len3)
- MySMI15Min(Len1, Len2, Len3)
- MySMI5Min(Len1, Len2, Len3)
- MyStochasticDaily(...)
- MyStochastic60Min(...)
- MyStochastic15Min(...)
- MyStochastic5Min(...)

[Include function code if you want Claude to reference it]