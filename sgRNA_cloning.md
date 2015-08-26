# Golden Gate sgRNA cloning protocol

## Introduction

This protocol is adapted from Konermann et al., 2014. from Zhang lab. The original protocol is [here](http://sam.genome-engineering.org/static/SAM%20sgRNA%20spacer%20cloning%20protocol.pdf).

It is used to clone a pair of compatible oligos into sgRNA(MS2) cloning backbone (addgene #61424).

## Materials

* Sense sgRNA oligo (100 μM)
* Antisense sgRNA oligo (100 μM)
* T4 PNK (NEB)
* 10X T4 ligase buffer (NEB)
* T7 ligase (NEB)
* 2X T7 ligase buffer (NEB)
* BSA (20 mg/ml) (NEB)
* BpiI restriction enzyme (**Fermentas!** Note: Replaces BbsI) 
* sgRNA(MS2) cloning backbone vector (addgene #61424)

## Procedure

### Oligo anneal

1. Mix the following components in a PCR tube:

	| **Component**        | **Amount (ul)** |
	|----------------------|-----------------|
	| Sense oligo          | 1               |
	| Antisense oligo      | 1               |
	| 10X T4 ligase buffer | 1               |
	| 10X T4 PNK           | 0.5             |
	| H2O                  | 6.5             |
	| **Total**            | **10**          |

2. Anneal oligos in a thermocycler with the following conditions:

	| Temperature (C) | Time (min) |
	|-----------------|------------|
	| 37              | 30         |
	| 95              | 5          |

	Ramp down to 25C.

3. Dilute the annealing reaction by adding 90 ul of PCR clean H2O
4. Mix the following components for the Golden Gate reaction:

	| **Component**                          | **Amount (ul)** |
	|----------------------------------------|-----------------|
	| T7 ligase                              | 0.125           |
	| 2X T7 ligase buffer                    | 12.5            |
	| BSA                                    | 0.125           |
	| BbsI restriction enzyme                | 1               |
	| Diluted anneal reaction                | 1               |
	| sgRNA(MS2) cloning backbone (25 ng/ul) | 1               |
	| H2O                                    | 9.25            |
	| **Total**                              | **25**          |

5. Run the following program on a thermocycler:

	| Temperature (C) | Time (min) |
	|-----------------|------------|
	| 37              | 5          |
	| 20              | 5          |

	Repeat for 15 cycles total
6. Transform 2 ul of Golden Gate reaction into chemically competent DH5α cells. 
7. Plate on Ampicillin plates. Grow at 37°C overnight. 2-3 colonies per sgRNA should be sufficient.

