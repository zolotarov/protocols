# KAPA HiFi PCR

**Reagents:**

| Component            | Volume (ul) |
| -------------------- | ----------- |
| KAPA HiFi Polymerase | 0.5         |
| 5X GC buffer         | 10          |
| 10 uM Forward Primer | 2.5         |
| 10 uM Reverse Primer | 2.5         |
| 10 mM dNTPs          | 1           |
| Template DNA (50 ng) | 1           |
| Nuclease-free water  | 32.5        |

**PCR Program:**

| Step                 | Cycles | Temp (C) | Time (s)   |  
| -------------------- | ------ | -------- | ---------- |  
| Initial denaturation | 1      | 98       | 30         |
|______________________|________|__________|____________|
| Denaturation         | 30     | 98       | 20         |  
| Annealing            | -      | 47       | 15         |  
| Extension            | -      | 72       | 15         |  
|______________________|________|__________|____________|
| Final extension      | 1      | 72       | 10 minutes |  
| Hold                 | 1      | 4        | Forever    |  

The extension time depends on the size of amplicon. For less than 1 kb, use 15 sec/kb, for longer use 30 sec/kb.
