# 360-Degree Threat Detection - Visual Guide

## System Overview

```
                    FULL 360° COVERAGE
                    
                          N
                          ↑
                          
              ╔═══════════════════════╗
              ║    Detection Zone     ║
              ║   (50-300 studs)      ║
         W ←  ║                       ║  → E
              ║         YOU           ║
              ║          ●            ║
              ║    Primary FOV        ║
              ╚═══════════════════════╝
                          
                          ↓
                          S
```

---

## How Indicators Appear

### Scenario 1: Single Threat Behind You
```
        YOUR SCREEN VIEW
   ┌─────────────────────────┐
   │                         │
   │                         │
   │          ▼ ⚠️          │  ← Orange arrow indicator
   │          ●              │     pointing down (threat behind)
   │    (Screen Center)      │
   │                         │
   │    [Your View/FOV]      │
   │                         │
   └─────────────────────────┘

Real World:
         YOU
          ▲ (Looking forward)
          │
          ●
          
        THREAT
          ● (Behind you)
```

### Scenario 2: Multiple Threats
```
        YOUR SCREEN VIEW
   ┌─────────────────────────┐
   │         ▲ ⚠️            │  ← Threat above/front
   │                         │
   │  ◄ ⚠️  ●  ► ⚠️         │  ← Threats on sides
   │   (Screen Center)       │
   │                         │
   │         ▼ ⚠️            │  ← Threat below/behind
   │                         │
   └─────────────────────────┘

Real World:
    THREAT (Front-Left)
       ●
        ╲
         ╲
   THREAT ● ───── YOU ───── ● THREAT
  (Left)        (▲)       (Right)
                 │
                 │
               THREAT
              (Behind)
```

### Scenario 3: Surrounded
```
        YOUR SCREEN VIEW
   ┌─────────────────────────┐
   │    ▲           ▲         │
   │  ⚠️             ⚠️      │
   │                         │
   │ ◄   ●           ► ⚠️   │
   │⚠️  (You)               │
   │                         │
   │    ▼   ⚠️    ▼         │
   │  ⚠️             ⚠️      │
   └─────────────────────────┘

Multiple threats detected in all directions!
Time to find cover or reposition!
```

---

## Detection Zones

```
                 MAX DISTANCE (300 studs)
        ┌─────────────────────────────────┐
        │                                 │
        │      FOV (Primary Aimbot)       │
        │            ╱───╲                │
        │           ╱     ╲               │
        │          ╱   ●   ╲              │ ← Detection
        │         ╱  (YOU)  ╲             │   Zone
        │        └───────────┘            │
        │                                 │
        │  ← Threats here show arrows    │
        │                                 │
        └─────────────────────────────────┘
                 MIN DISTANCE (50 studs)
        
Legend:
  ╱───╲  = Your primary FOV (aimbot active here)
  ● = Your position
  Outside FOV = 360° threat detection active
```

---

## Indicator Positioning

```
Indicators form a circle around screen center:

                    Indicator
                        ↑
                       ⚠️
                        │
                        │ 120px (default)
                        │
        ⚠️ ─────────── ● ─────────── ⚠️
     (Left)      (Center)      (Right)
                        │
                        │
                       ⚠️
                        ↓
                   Indicator

Radius = THREAT_INDICATOR_DISTANCE (configurable)
```

---

## Arrow Direction Logic

```
Arrows always point TOWARD the threat:

Example 1 - Threat Behind:
    YOU (facing →)          Arrow on screen points ↓
     →  ●                   (toward back of player)
        
        ●  THREAT
        
        
Example 2 - Threat to Right:
    YOU (facing ↑)          Arrow on screen points →
     ↑  ●    →  ● THREAT    (toward right side)
     
     
Example 3 - Threat Front-Left:
  THREAT                    Arrow on screen points ↖
    ●  ↘                    (toward front-left)
        ╲
         ● YOU (facing ↑)
         ↑
```

---

## Detection Range Visualization

```
Close Range (50-150 studs):
┌─────────┐
│   ●     │  ← Small detection area
└─────────┘
Fast targets, close combat


Medium Range (50-300 studs) [DEFAULT]:
┌───────────────┐
│               │
│      ●        │  ← Balanced for most scenarios
│               │
└───────────────┘


Long Range (100-500 studs):
┌─────────────────────────┐
│                         │
│                         │
│          ●              │  ← Large area, open combat
│                         │
│                         │
└─────────────────────────┘
```

---

## Real Combat Scenarios

### Scenario A: Flanker Approaching

```
Frame 1: Flanker outside FOV
   YOUR VIEW          THREAT
   ╱───╲              ●
  ╱  ●  ╲           ↙
 ╱   ↑   ╲         Moving toward you
└─────────┘
                    Indicator: ⚠️ → (Right side)


Frame 2: Flanker getting closer
   YOUR VIEW      THREAT
   ╱───╲          ●
  ╱  ●  ╲       ↙
 ╱   ↑   ╲     Closer
└─────────┘
                Indicator: ⚠️ → (Still right)


Frame 3: Flanker enters FOV
   YOUR VIEW
   ╱───╲
  ╱  ●●╲  ← THREAT NOW VISIBLE
 ╱   ↑  ╲
└───────┘
            Indicator: (Removed - in FOV now)
            Aimbot can now target them
```

### Scenario B: Being Flanked During Combat

```
Step 1: Fighting enemy in front
   ╱───╲
  ╱  ●●╲  ← Fighting this one
 ╱   ↑  ╲
└───────┘

      ●  ← NEW THREAT (behind)
      
Screen shows: ⚠️ ▼ (below center)
Action: Finish fight quickly or reposition!


Step 2: More threats appear
      ●  ← Front enemy
   ╱───╲
  ╱  ●  ╲
 ╱   ↑   ╲
└─────────┘
      ●  ← Behind
   ●     ● ← Sides

Screen shows: ⚠️ on multiple sides
Action: FIND COVER IMMEDIATELY!
```

---

## Indicator Color Coding

```
Current Implementation:
🟠 Orange = Active threat outside FOV
   Color: RGB(255, 165, 0)
   Meaning: Player detected, alive, in range

Future Enhancements:
🔴 Red = Critical threat (very close)
🟡 Yellow = Moderate threat (medium range)
🟢 Green = Distant threat (far range)
```

---

## Performance Impact Visualization

```
FRAME TIME BREAKDOWN (60 FPS scenario):

Without 360° Detection:
├────────┤ Aimbot: 0.8ms
└────────┘ Total: 0.8ms/frame


With 360° Detection:
├────────┤ Aimbot: 0.8ms
│ Threat scan every 0.2s (not every frame!)
└────────┘ Total: ~0.8ms/frame average
           ~0.85ms/frame during scan

Impact: <5% additional load
```

---

## System Flow Diagram

```
START
  │
  ├─→ Every 0.2 seconds:
  │     │
  │     ├─→ Get all players
  │     │
  │     ├─→ For each player:
  │     │     │
  │     │     ├─→ Calculate distance
  │     │     │
  │     │     ├─→ Is in range? (50-300 studs)
  │     │     │     │
  │     │     │     ├─ NO → Skip this player
  │     │     │     │
  │     │     │     └─ YES → Check if outside FOV
  │     │     │              │
  │     │     │              ├─ In FOV → Skip (visible)
  │     │     │              │
  │     │     │              └─ Outside FOV → THREAT!
  │     │     │                   │
  │     │     │                   ├─→ Calculate angle
  │     │     │                   │
  │     │     │                   ├─→ Create/update indicator
  │     │     │                   │
  │     │     │                   └─→ Position arrow
  │     │     │
  │     │     └─→ Next player
  │     │
  │     └─→ Remove indicators for threats no longer active
  │
  └─→ Repeat
```

---

## Configuration Examples

### For Close-Range Combat (Tight Spaces)
```lua
THREAT_MIN_DISTANCE = 30
THREAT_MAX_DISTANCE = 150
THREAT_SCAN_INTERVAL = 0.15  -- More frequent

Visualization:
┌─────────┐
│    ●    │  Small, fast detection
└─────────┘
```

### For Open-Area Combat (Large Maps)
```lua
THREAT_MIN_DISTANCE = 100
THREAT_MAX_DISTANCE = 500
THREAT_SCAN_INTERVAL = 0.3   -- Less CPU usage

Visualization:
┌─────────────────────────┐
│          ●              │  Large, efficient detection
└─────────────────────────┘
```

### For Balanced/Default Settings
```lua
THREAT_MIN_DISTANCE = 50
THREAT_MAX_DISTANCE = 300
THREAT_SCAN_INTERVAL = 0.2

Visualization:
┌───────────────┐
│      ●        │  Optimal for most scenarios
└───────────────┘
```

---

## Tips for Reading Indicators

### Quick Reference
```
Arrow Position    Threat Direction    Action
─────────────────────────────────────────────
    ↑ Above      Front/Above         Keep watching
    
    → Right      Your right side     Turn right
    
    ↓ Below      Behind you          Turn around!
    
    ← Left       Your left side      Turn left
    
    ↗ Up-Right   Front-right         Minor adjust
    
    ↘ Down-Right Behind-right        Turn 135°
    
    ↙ Down-Left  Behind-left         Turn 135°
    
    ↖ Up-Left    Front-left          Minor adjust
```

### Priority System
```
Number of Indicators    Threat Level    Recommended Action
─────────────────────────────────────────────────────────
       1                 Low            Monitor, adjust position
       
     2-3                Medium          Be cautious, check flanks
     
     4-5                 High           Find cover, reposition
     
      6+               Critical         IMMEDIATE ACTION REQUIRED!
```

---

## Troubleshooting Visually

### Problem: No Indicators Showing

```
Check 1: Is feature enabled?
   ┌─────────────────────┐
   │ 360° Detection: ON  │ ✅
   └─────────────────────┘

Check 2: Are threats in range?
   Too Close (< 50)     Perfect (50-300)     Too Far (> 300)
        ●                     ●                    ●
         ╲                    │                   ╱
          ╲                   │                  ╱
           ● YOU              ● YOU             ● YOU
   
Check 3: Are threats in FOV?
   ╱───╲
  ╱  ●●╲  ← If here, no indicator (already visible)
 ╱   ↑  ╲
└───────┘
```

### Problem: Too Many Indicators

```
Solution: Reduce detection range

Before (max=300):            After (max=150):
┌───────────────┐           ┌─────────┐
│  ●   ●   ●    │           │    ●    │
│ ●     ●     ● │    →      │    ●    │
│  ●   ●   ●    │           └─────────┘
└───────────────┘           Fewer indicators
Many threats                Focus on closest
```

---

## Integration with Aimbot

```
COMBINED SYSTEM OPERATION:

           360° Threat Detection
                  │
    ┌─────────────┼─────────────┐
    │             │             │
  Behind        Sides         Front
    │             │             │
    │             │         ┌───┴───┐
    │             │         │  FOV  │
    └─────────────┴─────────┤Aimbot │
                  │         │Active │
              Indicators    └───────┘
              (Orange ⚠️)   (Targeting)

Working Together:
• Aimbot handles threats in FOV
• 360° detection warns about others
• Seamless coverage of all directions
```

---

**Visual guide complete! 🎯**

For detailed technical information, see [THREAT_DETECTION_GUIDE.md](./THREAT_DETECTION_GUIDE.md)
