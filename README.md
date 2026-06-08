# NCSA_Delta_Gateway_Tutorials

Tutorials and Jupyter notebook workflows for running **Lattice Microbes** and **whole-cell** simulations on the **NCSA Delta Science Gateway** (GPU-backed Jupyter, shared workspace on NFS).

## Tutorial with Videos: [Link](https://minimalcell4d.web.illinois.edu/home/tutorials/)

## Contents

| Folder | Topic |
|--------|--------|
| [`CME/`](CME/) | Chemical master equation (CME) tutorials, GIP, bimolecule examples, and supporting figures |
| [`RDME/`](RDME/) | Reaction–diffusion (RDME) tutorials, 4DWCM analysis examples, and supporting data |
| [`4D Whole Cell/`](4D%20Whole%20Cell/) | **4D Whole-Cell Model (4DWCM)** for the minimal cell — setup, logs, job control on the gateway |

> The **setup steps below are the same for every tutorial** in this repository. Each tutorial’s own README only covers content that is specific to that tutorial.

---

## Getting started on the QCB Delta Gateway

You will access [NCSA Delta](https://docs.ncsa.illinois.edu/systems/delta/en/latest/quick_start.html) through the **QCB Delta Gateway**. The gateway runs a long-lived **JupyterHub** service on a Delta service node — you only need a single SSH command on your laptop to tunnel into it. No manual `srun`, no two-terminal setup.

### 1. Log in to the gateway

Open a terminal on your laptop and run:

```bash
ssh -L 8000:dt-svc-bbkw01.hsn.cm.delta.internal.ncsa.edu:8000 USERNAME@login.delta.ncsa.illinois.edu
```

> [!WARNING]
> ***Replace*** `USERNAME` with your Delta username (e.g. `alfiaparvez`).

What this command does:

- Logs you into the Delta login node (`login.delta.ncsa.illinois.edu`).
- Opens an SSH tunnel: **local `127.0.0.1:8000` → Delta service node `dt-svc-bbkw01:8000`**, where the gateway’s JupyterHub service is running.

You will be prompted for your **NCSA password** and **two-factor authentication (2FA)**. Once you’re in, **leave the terminal open** — closing it tears down the tunnel.

### 2. Open the gateway in your browser

Once the SSH tunnel is up, open this URL in any browser on your laptop:

```
https://dt-svc-bbkw01.delta.ncsa.illinois.edu:8000/hub/org/
```

Click on the QCB Gateway tab. You should see the **JupyterHub login page** for the QCB Delta Gateway.Click on CI Logon and sign in with your Delta credentials and you’ll land in the gateway’s notebook interface.

> [!NOTE]
> Your browser will likely warn about a **self-signed certificate** the first time (the cert is issued to the internal Delta service node, not `localhost`). It is safe to proceed — the traffic is end-to-end encrypted inside your SSH tunnel.

> [!NOTE]
> If port `8000` is busy on your laptop, replace **the first** `8000` (the local port) — for example `-L 8765:dt-svc-bbkw01...:8000` — and visit `https://localhost:8765/hub/login` instead. The remote port (`8000`) and service node (`dt-svc-bbkw01...`) must stay as given.

### 3. Set the Jupyter kernel to `LM 2.5`

Before opening or running any tutorial notebook, make sure the kernel is set to **`LM 2.5`** — this is the conda environment with Lattice Microbes (`lm`, `jLM`), CUDA-enabled solvers, and all dependencies pre-installed.

- **When opening a notebook:** if a kernel-selection dialog appears, choose **`LM 2.5`** (also shown as `LM 2.5 (Python 3.7)` / `lm_2.5_dev`).
- **When creating a new notebook:** in the JupyterHub Launcher, click the **`LM 2.5`** tile (not the default `Python 3` tile).
- **To change the kernel of an open notebook:** menu bar → `Kernel` → `Change Kernel…` → select **`LM 2.5`**.

You can confirm the kernel is correct by checking the **top-right of the notebook** — it should display `LM 2.5` (or `lm_2.5_dev`).

> [!WARNING]
> If you run a tutorial cell with the wrong kernel (e.g. plain `Python 3`), you will see `ModuleNotFoundError: No module named 'lm'` or similar. Switch the kernel as above and re-run.

### 4. Clone the tutorials inside JupyterHub

You don’t need to drop back to a terminal — you can pull the tutorials in directly from a notebook cell.

**Option A — from a Jupyter notebook cell** (recommended)

`File` → `New` → `Notebook` → pick the **`LM 2.5`** kernel → in the **first cell** run:

```python
!git clone https://github.com/alfia14/NCSA_Delta_Gateway_Tutorials.git
```

The leading `!` runs the command in a shell. After it finishes, refresh the JupyterHub file browser on the left — you’ll see a new `NCSA_Delta_Gateway_Tutorials/` folder with **CME**, **RDME**, and **4D Whole Cell** subdirectories.

> [!NOTE]
> If the folder already exists from a previous session, either:
> - `cd NCSA_Delta_Gateway_Tutorials && git pull` to update it, **or**
> - `!rm -rf NCSA_Delta_Gateway_Tutorials` and re-clone.

**Option B — from the JupyterHub terminal**

`File` → `New` → `Terminal`, then:

```bash
git clone https://github.com/alfia14/NCSA_Delta_Gateway_Tutorials.git
```

Then go back to the file browser and open notebooks from there.

### 5. Open and run a tutorial

In the JupyterHub file browser on the left, open one of the tutorial folders (e.g. `NCSA_Delta_Gateway_Tutorials/CME/`) and follow that folder’s `README.md`.

For each tutorial notebook:

- **Open the `.ipynb`** file.
- Confirm the kernel is **`LM 2.5`** (top-right of the notebook).
- Run cells **top to bottom** with `Shift + Enter`.
- Output (progress lines, plots, final figures) appears **inline** as cells finish.

> [!TIP]
> Long simulations (e.g. 4D whole-cell runs) print progress live to the cell output — Python is run unbuffered, so you can watch the simulation advance in real time, like `tail -f` on a log file. **Don’t close the browser tab** while a cell is running or you’ll lose the live stream (the job itself keeps going on Delta).

That’s it — you’re now executing GPU-accelerated minimal-cell simulations on **NCSA Delta**, from your laptop browser, through the QCB Delta Gateway.

---

## `4D Whole Cell/` — what is 4DWCM?

**4DWCM** is the **4D Whole-Cell Model** for the genetically minimal cell **JCVI-syn3A**. The “**4D**” means **three spatial dimensions plus time**: the simulation tracks **where** things are in the cell **and** how they **evolve** over **biological time** (seconds of cell time, which can map to long wall-clock runs on GPUs).

The model **couples** several layers that are usually separate:

| Piece | Role |
|--------|------|
| **RDME** | Spatial stochastic chemistry and diffusion on a 3D lattice (Lattice Microbes on GPU) |
| **CME** | Global stochastic processes (e.g. transcription-related chemistry) |
| **ODE** | Deterministic metabolism / fast limit where appropriate |
| **Brownian dynamics** | Large-scale chromosome and DNA–protein mechanics (e.g. LAMMPS/Kokkos on GPU) |

Together, these give a **spatiotemporal** “whole cell” picture instead of only well-mixed or only spatial or only metabolic modeling in isolation.

### Where the whole-cell tutorial lives in this repository

After cloning, the **4D whole cell** material is at:

```
NCSA_Delta_Gateway_Tutorials/4D Whole Cell/
```

| What | |
|------|---|
| **Entry notebook** | [`Tutorial_4dwcm_gateway.ipynb`](4D%20Whole%20Cell/Tutorial_4dwcm_gateway.ipynb) — paths, environment, logs, `nohup`/`tail`, and job control |
| **Model code (not in this repo)** | Clone [Minimal_Cell_4DWCM](https://github.com/Luthey-Schulten-Lab/Minimal_Cell_4DWCM) separately. On the **Delta gateway**, the tutorial assumes a layout like `/home/user/workspace/Minimal_Cell_4DWCM` and an **LM 2.5** kernel with `/Software` tools. |

**Upstream code and papers**

- **Code:** [Luthey-Schulten-Lab/Minimal_Cell_4DWCM](https://github.com/Luthey-Schulten-Lab/Minimal_Cell_4DWCM)
- **Overview site:** [4D Minimal Cell](https://minimalcell4d.web.illinois.edu/home/)
- **Primary paper (example):** [Thornburg *et al.*, *Cell* 2026 — bringing the minimal cell to life in 4D](https://www.cell.com/cell/fulltext/S0092-8674(26)00174-1)

**Typical gateway needs:** Jupyter with a **Lattice Microbes**–compatible kernel (e.g. **LM 2.5**), access to **GPUs** (simulation is heavy), and a persistent clone of the model under the gateway workspace so `Data/` and `logs/` survive across sessions.
