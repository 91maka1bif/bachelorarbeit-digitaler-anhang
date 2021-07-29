# Digitaler Anhang

Digitaler Anhang für die Bachelorarbeit von Kazim Ali Mazhar ([91maka1bif@hft-stuttgart.de](mailto:91maka1bif@hft-stuttgart.de)) im Sommersemester 2021.

# Anmerkungen

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
    * Modell 1: [gat-ha.py:170](Code/Modell%201%20(AGDN+HA)/adaptive_graph_diffusion_networks_with_hop-wise_attention/ogbn-arxiv/src/gat-ha.py#L170)
    * Modell 2: [gat\gat.py:149](Code/Modell%202%20(GAT+CS)/CorrectAndSmooth/gat/gat.py#L149)
    * Modell 3: [gat_dgl\gat.py:183](Code/Modell%203%20(GAT+FLAG)/FLAG/ogb/nodeproppred/arxiv/gat_dgl/gat.py#L183)
* Die Logdateien, die vom Profiler erstellt wurden, sowie der Datensatz ([ogbn-arxiv](https://ogb.stanford.edu/docs/nodeprop/#ogbn-arxiv)) sind aufgrund der enormen Dateigrößen (~60 MB - 4,9 GB) nicht im Repository enthalten. Dank des Python-Moduls OGB wird jedoch der Datensatz beim Ausführen der Python-Skripte automatisch heruntergeladen.
* Am Ende der Trainingsschleife wird eine Datei `file.txt` gespeichert, welches die Grundlage für das Arbeitsblatt `Modell<Nummer>_Operator_Quelle1` in [A13_1_Operatoren.xlsx](Anhang/A13_1_Operatoren.xlsx), [A13_2_Operatoren.xlsx](Anhang/A13_2_Operatoren.xlsx) und [A13_3_Operatoren.xlsx](Anhang/A13_3_Operatoren.xlsx) bildet. Über Regex wurde diese Datei zuerst in eine CSV-Datei `file.csv`, dann in ein Excel-Format konvertiert.
* Die erstellten Logdateien bilden die Grundlage für die Arbeitsblätter 
    * `Modell<Nummer>_Operator_Quelle2` in [A13_1_Operatoren.xlsx](Anhang/A13_1_Operatoren.xlsx), [A13_2_Operatoren.xlsx](Anhang/A13_2_Operatoren.xlsx) und [A13_3_Operatoren.xlsx](Anhang/A13_3_Operatoren.xlsx) sowie
    * `Modell<Nummer>_Kernel_Quelle1` und `Modell<Nummer>_Kernel_Quelle2` in [A15_1_16_1_Kernels.xlsx](Anhang/A15_1_16_1_Kernels.xlsx), [A15_2_16_2_Kernels.xlsx](Anhang/A15_2_16_2_Kernels.xlsx) und [A15_3_16_3_Kernels.xlsx](Anhang/A15_3_16_3_Kernels.xlsx).