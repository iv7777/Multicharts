# Function Renaming Reference

## Old → New Function Names

### CMO Functions
- `MyCMODaily` → `CMO_Cur_D`
- `MyCMO60Min` → `CMO_Cur_1H`
- `MyCMO15Min` → `CMO_Cur_15M`
- `MyCMO5Min` → `CMO_Cur_5M`

### SMI Functions
- `MySMI60Min` → `SMI_Cur_1H`
- `MySMI15Min` → `SMI_Cur_15M`
- `MySMI5Min` → `SMI_Cur_5M`

### Stochastic Functions
- `MyStochasticDaily` → `Stochastic_Cur_D`
- `MyStochastic60Min` → `Stochastic_Cur_1H`
- `MyStochastic15Min` → `Stochastic_Cur_15M`
- `MyStochastic5Min` → `Stochastic_Cur_5M`

## Next Steps

### In MultiCharts
1. **Rename function files** in PowerLanguage Editor
2. **Update function names** inside each .Function file
3. **Recompile** MySignal strategy
4. **Verify** all functions resolve correctly

### Function File Renaming
```
OLD FILE NAME → NEW FILE NAME
MyCMODaily.Function → CMO_Cur_D.Function
MyCMO60Min.Function → CMO_Cur_1H.Function
MyCMO15Min.Function → CMO_Cur_15M.Function
MyCMO5Min.Function → CMO_Cur_5M.Function
MySMI60Min.Function → SMI_Cur_1H.Function
MySMI15Min.Function → SMI_Cur_15M.Function
MySMI5Min.Function → SMI_Cur_5M.Function
MyStochasticDaily.Function → Stochastic_Cur_D.Function
MyStochastic60Min.Function → Stochastic_Cur_1H.Function
MyStochastic15Min.Function → Stochastic_Cur_15M.Function
MyStochastic5Min.Function → Stochastic_Cur_5M.Function
```

## Status

✅ **MySignal.easylanguage** - All 23 function calls updated
✅ **CUSTOM_FUNCTIONS.md** - Documentation updated
⏳ **Function files** - Need to be renamed in MultiCharts
⏳ **Compilation** - Needs verification after function files are renamed
