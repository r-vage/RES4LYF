# Changelog

All notable changes to this fork of RES4LYF will be documented in this file.

## [Unreleased]

### Fixed
- Applied PR #223: Fixed CUDA device mismatch errors in `beta/rk_method_beta.py`
  - Added `comfy.model_management` import
  - Modified two `__call__` methods to ensure all tensors are moved to same device before computation
  - Prevents "Expected all tensors to be on the same device, but got mat1 is on cpu, different from other tensors on cuda:0" errors
  - Credits: @1506086927

- Applied PR #218: Added `beta57` scheduler registration in `__init__.py`
  - Fixes scheduler mismatch errors with KSampler
  - Addresses issue #161 with return type mismatch between linked nodes
  - Credits: @jeremymeyers

- Applied PR #211: Fixed return type mismatch errors with defensive scheduler handling
  - Modified `helper.py` and `legacy/helper.py` to defensively read scheduler names from comfy.samplers
  - Added import-time patch in `res4lyf.py` to ensure beta57 is visible to node definitions
  - Prevents scheduler mismatch errors when nodes are defined at import time
  - Credits: @jeremymeyers

- Applied PR #205: Fixed batch size mismatch for Ultimate SD Upscale tiling
  - Added `_broadcast_batch_dimension()` static method in `flux/layers.py`
  - Modified `flux/model.py` to use per-condition latent slice (x_cond) instead of full batch
  - Expanded text tensors to match image batch size when using tiled processing
  - Prevents RuntimeError when using Ultimate SD Upscale or Face Detailer with tiling
  - Credits: @EricRollei

- Applied PR #195: Updated requirements.txt
  - Removed specific numpy version requirement (>=1.26.4)
  - Allows ComfyUI to manage numpy version compatibility
  - Prevents conflicts with other packages requiring different numpy versions
  - Credits: @wzgrx

## Notes

### Community PRs Applied
- These changes were backported from pending pull requests to ClownsharkBatwing/RES4LYF
- PR #223: https://github.com/ClownsharkBatwing/RES4LYF/pull/223
- PR #218: https://github.com/ClownsharkBatwing/RES4LYF/pull/218
- PR #211: https://github.com/ClownsharkBatwing/RES4LYF/pull/211
- PR #205: https://github.com/ClownsharkBatwing/RES4LYF/pull/205
- PR #195: https://github.com/ClownsharkBatwing/RES4LYF/pull/195
