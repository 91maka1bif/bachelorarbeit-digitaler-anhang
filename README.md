# Digitaler Anhang

Digitaler Anhang für die Bachelorarbeit von Kazim Ali Mazhar (@91maka1bif) im Sommersemester 2021.

# Anmerkungen

* Die Logdateien, die vom Profiler erstellt wurden, sowie der Datensatz ([ogbn-arxiv](https://ogb.stanford.edu/docs/nodeprop/#ogbn-arxiv)) sind aufgrund der enormen Dateigrößen (~100 MB - 4 GB) nicht im Repository enthalten.
* Die Modelle entstammen dem [OGB-Leaderboard für diesen Datensatz](https://ogb.stanford.edu/docs/leader_nodeprop/#ogbn-arxiv). Im Folgenden die URLs zu den Repositories:
    * [Modell 1: Adaptive Graph Diffusion Networks with Hop-wise Attention](https://github.com/skepsun/adaptive_graph_diffusion_networks_with_hop-wise_attention)
    * [Modell 2: Correct and Smooth](https://github.com/CUAI/CorrectAndSmooth)
    * [Modell 3: Free Large-scale Adversarial Augmentation on Graphs](https://github.com/devnkong/FLAG)
* Um die Aufzeichnung durch den Profiler zu ermöglichen, musste folgender Code vor der Trainingsschleife der einzelnen Modelle eingefügt werden:
```python
    with profiler.profile(
        activities=[
            profiler.ProfilerActivity.CPU,
            profiler.ProfilerActivity.CUDA,
        ],
        schedule=profiler.schedule(
            wait=2,
            warmup=2,
            active=6,
            repeat=1),
        with_stack=True,
        profile_memory=True,
        record_shapes=True,
        with_flops=True,
        on_trace_ready=profiler.tensorboard_trace_handler('./log')
    ) as p:
```
* Im Einzelnen ist der Profiler-Code in folgenden Python-Skripten zu finden:
    * Modell 1: [gat-ha.py:170](https://gitlab.rz.hft-stuttgart.de/91maka1bif/bachelorarbeit-digitaler-anhang/-/blob/master/Code/Modell%201%20(AGDN+HA)/adaptive_graph_diffusion_networks_with_hop-wise_attention/ogbn-arxiv/src/gat-ha.py#L170)
    * Modell 2: [gat\gat.py:149](https://gitlab.rz.hft-stuttgart.de/91maka1bif/bachelorarbeit-digitaler-anhang/-/blob/master/Code/Modell%202%20(GAT+CS)/CorrectAndSmooth/gat/gat.py#L149)
    * Modell 3: [gat_dgl\gat.py:183](https://gitlab.rz.hft-stuttgart.de/91maka1bif/bachelorarbeit-digitaler-anhang/-/blob/master/Code/Modell%203%20(GAT+FLAG)/FLAG/ogb/nodeproppred/arxiv/gat_dgl/gat.py#L183)