# pytorch3d-Wheel

Custom **PyTorch3D** Wheel für CUDA 12.8 + Blackwell GPU (sm_120).

Optimiert für **HuggingFace ZeroGPU** und **PSHuman** auf Blackwell Hardware.

## 🎯 Specs

| Komponente | Version |
|---|---|
| **Python** | 3.10 |
| **PyTorch** | 2.11.0 + cu128 |
| **CUDA** | 12.8 |
| **GPU Arch** | 7.0, 7.5, 8.0, 8.6, 9.0, **12.0 (Blackwell)** |
| **PyTorch3D** | main (konfigurierbar) |

## 🚀 Workflow

Der GitHub Actions Workflow (`build_pytorch3d.yml`) baut das Wheel automatisch.

**Manuell triggern:**
1. GitHub → **Actions** → *Build pytorch3d Wheel*
2. **Run workflow** → Optional: pytorch3d ref eingeben (Branch/Tag/Commit)
3. **Run** → 30–60 Min. warten

**Release:**
Nach erfolgreichem Build wird ein GitHub Release mit dem Wheel erstellt.

## 📦 Installation

Die `.whl`-URL aus dem Release kopieren und in `requirements.txt` eintragen:

```
https://github.com/Painter3000/pytorch3d-Wheel/releases/download/pytorch3d-torch2.11.0-cu128/pytorch3d-XXX-cp310-cp310-linux_x86_64.whl
```

Dann wie gewohnt installieren:
```bash
pip install -r requirements.txt
```

## ⚙️ Build-Details

- ✅ `--no-build-isolation` → exakt torch 2.11.0, kein Downgrade
- ✅ `--index-url cu128` → CUDA-Wheel, nicht CPU
- ✅ `FORCE_CUDA=1` → Kompilierung ohne physische GPU
- ✅ `sm_120` enthalten → Blackwell RTX PRO 6000 unterstützt

## 🔗 Verwendung in PSHuman

Ersetze in PSHuman `requirements.txt`:
```diff
- # disabled_blackwell_incompatible: pytorch3d==0.7.8+pt2.1.0cu121
+ https://github.com/Painter3000/pytorch3d-Wheel/releases/download/pytorch3d-torch2.11.0-cu128/pytorch3d-XXX-cp310-cp310-linux_x86_64.whl
```

---

**Status:** ⏳ Build ausstehend

Weitere Blocker (torch_scatter, nvdiffrast) folgen demselben Prozess.
