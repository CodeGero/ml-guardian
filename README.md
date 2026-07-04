# ML Guardian — Audit Your ML Code

Catch common machine learning issues before they hit production.

## Quick Start

```yaml
- uses: CodeGero/ml-guardian@v1
  with:
    framework: all
```

## Detects
- Missing random seeds (non-reproducible results)
- Deprecated PyTorch/TensorFlow APIs
- In-place tensor ops (autograd errors)
- model.eval() without torch.no_grad()
- TF1-style code (Session, placeholder)
- pickle/joblib security risks
- Data leakage patterns (scaling before split)

## Premium
Custom rules per framework, training pipeline audit, data quality scoring — https://kryptorious.gumroad.com/l/jbvet

MIT License
