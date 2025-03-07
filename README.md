This repository contains artifacts for the paper submitted to IFIP 2025.

# TCP BBR Behavior over a Shared Bottleneck

TCP BBR’s behavior has been explained by various theoretical models in particular that describe how it co-exists with other type of flows. However, as new protocol versions emerged, it is not always clear to what extent the high-level behavior described by these models applies to newer protocol versions. In this paper, we systematically evaluate the most influential steady-state and fluid models describing BBR’s coexistence with loss-based flows over shared bottleneck links. Our experiments, conducted on a new experimental platform (FABRIC), extend previous evaluations to additional network scenarios, enabling comparisons between the two models and including the recently introduced BBRv3.

This repository includes:

 - FABRIC testbed notebooks and descriptions for generating experiment data and implementing fluid and steady-state models for two different topologies, evaluating BBRv1, BBRv2, and BBRv3 against CUBIC, RENO, or other BBR flows.
 - BBRv1 and BBRv2 fluid model code with minor modifications. ([Original paper](https://dl.acm.org/doi/10.1145/3517745.3561420))  ([Original repository](https://github.com/simonschdev/imc22-bbr-fluid-model)) 
 - BBRv1 steady-state model implementation in Python. ([Original paper](https://dl.acm.org/doi/10.1145/3355369.3355604))
 - Figures from the submitted paper and the corresponding data used to generate them.

To run this experiment on [FABRIC](https://fabric-testbed.net), you should have a FABRIC account with keys configured, and be part of a FABRIC project. You will need to have set up SSH keys and understand how to use the Jupyter interface in FABRIC.


## Run my Experiment (Generating Experimental and Theoratical Data)

- For the experiments in Ware's topology (Figures 2,3, and 5), you can run `ware-topology-experiments.ipynb`. This notebook contains additional instructions that require careful attention. You can run BBRv1, BBRv2, and BBRv3 experiments against a single loss-based flow. Additionally, use `ware_model.py` in this notebook to run and plot the steady-state model.

- To run the fluid model for Figures 2, 3, and 5, follow the `run_fluid_model.ipynb` notebook to collect the necessary data. In this notebook, you will run the model using different configuration files for various network settings. The corresponding configuration files can be found in [modified_fluid_model/configs](modified_fluid_model/configs). The model will generate JSON files for each experiment and you can use them in the `ware-topology-experiments.ipynb` notebook. The collected fluid model data is provided in [data/fluid_model_data]( data/fluid_model_data).

- For the experiments in Scherrer's topology (Figures 4 and 6), run `scherrer_topology_experiment.ipynb` notebook. This notebook contains additional instructions that require careful attention. You can run BBRv1, BBRv2, and BBRv3 experiments against multiple loss-based or BBR flows. To run the fluid model for these figures, follow the `run_fluid_model.ipynb` notebook to collect the necessary data using the configuration file `model_validation_100Mbps_10ms.yaml`. After running the model, it will generate a .json file, which you can use to plot the fluid model results for the figures. Our generated JSON file is provided as `scherrer_topology_data.json`.

- Bonus: You can also reproduce additional figures from the ([Ware paper](https://dl.acm.org/doi/10.1145/3355369.3355604)) by following the`reproduce_ware_initial_figures.ipynb` notebook.

## Notes

- You can also run the fluid model easily on your computer. The provided FABRIC notebook is an alternative option.
  
- In the paper, we mentioned that running the fluid model for long durations consumes excessive RAM, making it infeasible. You can find proof of this in the excessive_memory_usage.log file, which shows increasing memory usage over time until all available memory is exhausted.
