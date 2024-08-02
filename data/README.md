# Data Resources for FlyWire Visual Neuron Types

| File Name                                      | Description                                                                                                                                                                                                           |
|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `neuron_table.csv`                            | Metadata for all neurons in the FlyWire dataset v783. Includes cell ID, category (intrinsic/boundary/other), cell type, SOMA side, most synapses side, and % synapses in the optic lobes. |
| `ol_intrinsic_types.py`                        | OL intrinsic types grouped by type families                                                                                                                                                                           |
| `synapse_table.csv.gz`                         | Full synapse table (without thresholds) with compacted cell IDs                                                                                                                                                       |
| `synapse_table_compact_ids_map.csv.gz`         | Map from compacted cell IDs to full cell IDs (for the synapse table)                                                                                                                                                  |
| `type_to_type_connection_and_synapse_counts.csv` | Type-to-type connection and synapse counts for OL intrinsic and boundary types                                                                                                                                        |
| `left_vs_right_super_classes_boundary.csv`     | Comparing super class counts for OL boundary neurons L vs R                                                                                                                                                           |
| `left_vs_right_super_classes_intrinsic.csv`    | Comparing super class counts for OL intrinsic neurons L vs R                                                                                                                                                          |
| `left_vs_right_types_boundary.csv`             | Comparing cell type counts for OL boundary neurons L vs R                                                                                                                                                             |
| `left_vs_right_types_intrinsic.csv`            | Comparing cell type counts for OL intrinsic neurons L vs R                                                                                                                                                            |


## FlyWire Data Version
Cell IDs and synapse / connection counts refer to the FlyWire connectome version 783 (released in October 2023).

## Neuron categories
### Optic Lobe Intrinsic
Neurons with at least 95% of synapses in one optic lobe. There are few exceptions:
1. Neurons with no synapses are excluded even if (by morphology) we believe they belong to one of the optic lobe 
intrinsic cell types. Less than 2% of the cells in the dataset fall in this bucket.
2. Neurons with reconstruction errors are excluded. Less than 0.1% of the intrinsic cells.

### Optic Lobe Boundary
Neurons with at least 5% of synapses in any optic lobe, plus bilateral neurons with synapses in both optic lobes.
Neurons with reconstruction errors are excluded (less than 1% of the boundary cells).

### Cell types outside the optic lobes
For neurons not in the optic lobes, we use types from the primary FlyWire annotations resource
[Schlegel et al. 2023](https://www.biorxiv.org/content/10.1101/2023.06.27.546055v2).
If a neuron has multiple types assigned, we resolve to a primary type by prioritizing FlyWire types over Hemibrain types.

## Connection thresholds applied to the dataset
To account for potentially noisy synapse predictions, in our anelyses we have excluded 
connections with less than 5 synapses in the central brain
(this is consistent with the threshold used in other publications utilizing the FlyWire connectome) and we have
excluded connections with less than 2 synapses in the optic lobes (this is unique to our study, and is based on 
empirical evidence - the separation of types viewed as clusters of feature vectors counting connections with other 
types is maximized with threshold of 2+ synapses).

## Synapse table
Due to its large size, synapse table is compressed (with gzip) and further compacted by replacing the long FlyWire cell IDs (root IDs) with shorter IDs.
After un-compressing the files (```gunzip synapse_table.csv.gz; gunzip synapse_table_compact_ids_map.csv.gz```) the IDs in synapse table can be replaced back to FlyWire cell IDs using the map.