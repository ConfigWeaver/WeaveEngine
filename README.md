# WeaveEngine

**WeaveEngine** is the configuration merge engine that powers [ConfigWeaver](https://github.com/ConfigWeaver). It provides a lightweight, modular system for deeply merging layered YAML configurations — including support for presets, schema validation, and hierarchical overrides.

---

## ✨ Features

- 🧩 **Deep Merge Logic** for YAML structures
- 🧱 **Hierarchical Overrides** (global → cluster → env → app → presets)
- 📦 **Preset Support** for reusable config layers
- ✅ **JSON Schema Validation** of final merged config
- ⚡ Built for GitOps workflows and Git-backed environments

---

## 📐 Merge Strategy

WeaveEngine performs a deep recursive merge of YAML files in a specific order of precedence:

1. `global.yaml`
2. `clusters/{cluster}.yaml`
3. `envs/{env}.yaml`
4. `apps/{app}.yaml`
5. One or more `presets/*.yaml`

Higher layers override keys from lower layers while preserving nested structure.

---

## 🛠️ Usage (Python Example)

```python
from weaveengine import merge_configs, validate_config

merged = merge_configs(
    global_path="values/global.yaml",
    cluster_path="values/clusters/prod.yaml",
    env_path="values/envs/prod.yaml",
    app_path="values/apps/my-app.yaml",
    presets=["values/presets/logging.yaml", "values/presets/monitoring.yaml"]
)

validate_config(merged, schema_path="schemas/my-app.schema.json")
