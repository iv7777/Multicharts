# Strategy Architecture

## Main Components
1. SMA Calculations (Section 3)
2. Oscillators & Indicators (Section 4-6)
3. Phase Detection (Section 15)
4. Entry Logic (Section 18-20)
5. Order Execution (Section 21)

## Data Flow
1. Calculate all SMAs across timeframes
2. Calculate slopes and smoothing
3. Determine bull/bear phases
4. Check permissions (Can_GoLong, Can_GoShort)
5. Evaluate entry conditions
6. Execute orders if conditions met

## Key Design Decisions
- [Document important architectural choices]
- [Why certain approaches were chosen]
- [Known limitations or trade-offs]
```

---

## **Comparison: Project vs. Template**

| Aspect | With Project | Without Project (Template) |
|--------|--------------|----------------------------|
| **Setup effort** | High initially, but one-time | Low each time, but repeated |
| **Context persistence** | ✅ Automatic | ❌ Must re-paste every session |
| **Code reference** | ✅ Upload once, always available | ❌ Must re-paste or describe |
| **Knowledge building** | ✅ Accumulates over sessions | ❌ Starts fresh each time |
| **Consistency** | ✅ Always uses same standards | ⚠️ Can drift if template not updated |
| **Flexibility** | ⚠️ Need to update project settings | ✅ Can adjust per session |
| **Collaboration** | ✅ Share project link | ⚠️ Must share template separately |
| **Best for** | ✅ Ongoing development | ✅ One-off questions |

---

## **Recommended Hybrid Approach**

### **Use Projects For:**
✅ Your main strategy development (Project Morpheus)
✅ Long-term refactoring work
✅ Complex multi-session tasks
✅ When you want Claude to remember context
✅ Team collaboration (others can join project)

### **Use Templates For:**
✅ Quick one-off questions ("How do I...")
✅ Learning new PowerLanguage features
✅ Testing ideas outside main strategy
✅ When helping others (paste template into their chat)
✅ Public forums/sharing (can't share project access)

### **Combine Both:**
```
Project: "MultiCharts - Project Morpheus"
├── Custom Instructions (core context that never changes)
├── Uploaded Files (code, standards, architecture)
└── Each conversation can add session-specific context

Session Template (paste when needed for specific tasks):
"Today's focus: [Debugging entry logic]
Specific issue: [Entry_Technical not firing on 15M reversal]
Context: [Lines 892-945 in uploaded strategy code]
What I've tried: [Added print statements, values look correct]
Please help: [Find why condition evaluates to False]"
```

---

## **Practical Example: Your Workflow**

### **Without Projects** (Current):
```
Day 1: [Paste full context] "Help me refactor SMA calculations"
Day 2: [Re-paste context] "Now help with phase detection"  
Day 3: [Re-paste context] "Debug entry logic"
Day 4: [Re-paste context] "Optimize performance"
         ↑ Tedious and error-prone
```

### **With Projects** (Better):
```
Setup: Create project, upload code & standards [15 minutes one-time]

Day 1: "Help me refactor SMA calculations" 
       ↳ Claude knows your code, standards, style
       
Day 2: "Now help with phase detection"
       ↳ Claude remembers yesterday's refactoring
       
Day 3: "Debug entry logic"  
       ↳ Claude knows your architecture
       
Day 4: "Optimize performance"
       ↳ Claude has full context automatically
```

---

## **How to Structure Conversations in Your Project**

### **Start New Chat For:**
- ✅ Distinct phases (Development → Testing → Optimization)
- ✅ Different strategy components (Entry logic vs. Exit logic)
- ✅ Major architectural changes
- ✅ When previous chat gets very long (>50 messages)

### **Continue Same Chat For:**
- ✅ Iterating on same code section
- ✅ Related bug fixes
- ✅ Follow-up questions on previous responses
- ✅ Gradual refinement of one feature

### **Use Chat Titles Like:**
- "Phase 1: Naming Refactor"
- "Debug: Entry_Technical not firing"
- "Optimize: SMA calculations"
- "Add Feature: 5M timeframe support"

---

## **Setting Up Your Project RIGHT NOW**

**Quick Setup (10 minutes):**

1. **Create Project**
   - Name: "MultiCharts - Project Morpheus"
   
2. **Add Custom Instructions** (paste above template)

3. **Upload Files:**
   - Your refactored strategy code (from earlier)
   - Copy the naming standards into a .md file
   
4. **Start First Chat:**
```
   "I've set up this project for ongoing development of my multi-timeframe 
   strategy. The refactored code is uploaded. I'm ready to continue with 
   the next phase: [your next task]"