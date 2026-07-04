# ML Guardian — Audit Your ML Code

[![Marketplace](https://img.shields.io/badge/Marketplace-ml--guardian-purple)](https://github.com/marketplace/actions/ml-guardian)
[![Version](https://img.shields.io/badge/version-1.0.0-green)](https://github.com/CodeGero/ml-guardian/releases)

**Machine learning code has unique failure modes.** Missing seeds, deprecated APIs, data leakage, pickle exploits — this action catches them all.

---

## Quick Start

```yaml
- uses: CodeGero/ml-guardian@v1
  with:
    framework: all
```

## What It Detects

| Category | Issue | Framework |
|----------|-------|-----------|
| **Reproducibility** | Missing `random_state` / `np.random.seed` | All |
| **PyTorch** | `torch.sigmoid()` → use `torch.nn.functional` | PyTorch |
| **PyTorch** | In-place tensor ops breaking autograd | PyTorch |
| **PyTorch** | `model.eval()` without `torch.no_grad()` | PyTorch |
| **TensorFlow** | TF1 `Session`, `placeholder` → migrate to TF2 | TensorFlow |
| **sklearn** | `train_test_split` without `random_state` | sklearn |
| **Security** | `pickle.load()` / `joblib.load()` — RCE risk | All |
| **Data Leakage** | Scaling before train/test split | All |

## Full CI Config

```yaml
name: ML Quality
on: [pull_request]
jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: CodeGero/ml-guardian@v1
        with:
          framework: pytorch
          fail-on-error: 'true'
```

## Inputs

| Input | Default | What it does |
|-------|---------|-------------|
| `path` | `.` | Where to scan |
| `framework` | `all` | pytorch, tensorflow, sklearn, jax, or all |
| `fail-on-error` | `true` | Stop on critical issues |

## Premium

https://kryptorious.gumroad.com/l/jbvet — Custom rules, training pipeline audit, data quality scoring.

MIT License
