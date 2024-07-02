# Data Resources for FlyWire Visual Neuron Types

## FlyWire Data Version
Cell IDs and synapse / connection counts refer to the FlyWire connectome version 783 (released in October 2023).

## Connections included in the dataset
To account for potentially noisy synapse predictions, we have included connections with 5 or more synapses for the general case.
This is consistent with the threshold used in other publications utilizing the FlyWire connectome. For connections in the 
optic lobes we applied a threshold of 2+ synapses. This is unique to our work, and is based on empirical evidence - the separation 
of types viewed as clusters of feature vectors counting connections with other types is maximized with threshold 2.

## Neurons included in the dataset
### Optic Lobe Intrinsic
Neurons with 95 percent or more synapses in one optic lobe. There are few exceptions:
1. Neurons with no synapses are excluded even if (by morphology) we believe they belong to one of the optic lobe 
intrinsic cell types. Less than 2% of the cells.
2. Neurons with reconstruction errors are excluded. Less than 0.1% of the intrinsic cells.

### Optic Lobe Boundary
Neurons with >0 but <5 percent of synapses in any optic lobe, and bilateral neurons with synapses in both optic lobes.
Neurons with reconstruction errors are excluded. Less than 1% of the boundary cells.

### Cell types outside the optic lobes
For neurons not in the optic lobes, we use types from the primary FlyWire annotations resource
[Schlegel et al. 2023](https://www.biorxiv.org/content/10.1101/2023.06.27.546055v2).
If a neuron has multiple types assigned, we resolve to a primary type by prioritizing FlyWire types over Hemibrain types.
