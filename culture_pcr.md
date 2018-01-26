# Culture PCR

1. Aliquot 2 ul of bacteria culture in PCR tubes and lyse in a thermocycler at 99 °C for 15 minutes.
2. Prepare the PCR master mix during lysis:

Master mix for 1 reaction (23 ul total):

| Reagent        | Volume (ul) |
| -------------- | ----------- |
| DFS-Taq        | 0.25        |
| Buffer         | 2.5         |
| dNTPs          | 0.5         |
| Forward primer | 1.25        |
| Reverse primer | 1.25        |
| Water          | 17.25       |

3. If running a PCR to check for sgRNA, use the reverse oligo and U6 forward primer
5. Run the following PCR amplification program (1 min/kb extension time):

| Step                   | Cycles   | Temp (C)   | Time (s)     |  
| ---------------------- | -------- | ---------- | ------------ |  
| Initial denaturation   | 1        | 94         | 2 min        |  
| ______________________ | ________ | __________ | ____________ |  
| Denaturation           | 25       | 94         | 10           |  
| Annealing              | -        | 47         | 20           |  
| Extension              | -        | 72         | 20           |  
| ______________________ | ________ | __________ | ____________ |  
| Final extension        | 1        | 72         | 5 minutes    |  
| Hold                   | 1        | 4          | Forever      |  
