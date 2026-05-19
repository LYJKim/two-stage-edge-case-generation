# Two-Stage Edge-Case Generation for Autonomous Driving

This repository contains experiments on generating autonomous-driving edge-case scenarios using diffusion-based image generation models.  
The project compares Text-to-Image, ControlNet, img2img, and Inpainting approaches, and proposes a **Two-Stage Edge-Case Generation** pipeline that separates global scene generation from local risk-factor insertion.

---

## Repository Name

Recommended repository name:

```text
two-stage-edge-case-generation
```

Alternative names:

```text
diffusion-edge-case-generation
controlnet-driving-scenario-generation
two-stage-driving-risk-generation
```

The recommended name is `two-stage-edge-case-generation` because the main contribution of this project is not simple image generation, but a two-stage generation strategy for autonomous-driving risk scenarios.

---

## Project Overview

Autonomous-driving systems require diverse and safety-critical scenarios for testing and validation.  
However, collecting real-world edge-case data is expensive, time-consuming, and often limited by the rarity of dangerous situations.

This project explores whether diffusion-based generative models can be used to create synthetic driving scenarios that contain challenging risk factors such as pedestrians, vehicles, occlusions, traffic lights, low visibility, and potential collision paths.

The experiments focus on the following generation methods:

- Text-to-Image generation
- ControlNet-based structure-conditioned generation
- img2img-based global scene modification
- Inpainting-based local object insertion
- Global-to-Local and Local-to-Global generation strategies
- A final Two-Stage Edge-Case Generation pipeline

---

## Main Idea

The final proposed direction is a **Two-Stage Edge-Case Generation** framework.

### Stage 1: Global Context Generation

The first stage generates or modifies the global driving context, such as:

- Road structure
- Weather conditions
- Lighting conditions
- Visibility
- Overall driving environment

Possible methods for this stage include Text-to-Image, img2img, and ControlNet.

### Stage 2: Local Risk-Factor Insertion

The second stage inserts local risk factors into specific regions of the generated or existing scene, such as:

- Pedestrians
- Vehicles
- Traffic lights
- Occluding objects
- Potential collision paths
- Close-distance interactions between road users

Possible methods for this stage include Inpainting, local editing, and mask-based image modification.

### Final Output

The final output is a synthetic autonomous-driving edge-case image in which both global driving context and local risk factors are combined.

---

## Repository Structure

The original uploaded files contain several notebooks and report PDFs.  
Before uploading to GitHub, it is recommended to rename files in English and remove unnecessary macOS metadata files.

Suggested structure:

```text
.
├── notebooks/
│   ├── controlnet_t2i.ipynb
│   ├── controlnet_experiments.ipynb
│   └── two_stage_generation.ipynb
│
├── reports/
│   ├── ldm_paper_review.pdf
│   ├── controlnet_paper_review.pdf
│   ├── controlnet_experiments.pdf
│   ├── two_stage_experiments.pdf
│   └── advanced_paper_review.pdf
│
├── README.md
└── .gitignore
```

---

## Notebooks

### `controlnet_t2i.ipynb`

This notebook compares basic Text-to-Image generation with ControlNet-based generation.  
It investigates the limitations of using ControlNet without meaningful structural conditions and analyzes how generated driving scenes differ from standard Text-to-Image outputs.

### `controlnet_experiments.ipynb`

This notebook contains ControlNet-based experiments using structural conditions such as depth maps and Canny edges.  
The main goal is to test whether road structure can be preserved while modifying scene attributes such as weather, lighting, vehicles, or pedestrians.

### `two_stage_generation.ipynb`

This notebook contains the core experiments for the two-stage generation strategy.  
It compares global modification and local editing approaches, and tests whether Inpainting can insert risk-related objects into specific regions of a driving scene.

---

## Reports and Reviews

### `ldm_paper_review.pdf`

A review of Latent Diffusion Models, focusing on why image generation is performed in latent space and how this improves high-resolution image synthesis.

### `controlnet_paper_review.pdf`

A review of ControlNet, focusing on how spatial conditions such as edge, depth, and pose maps can guide image generation.

### `controlnet_experiments.pdf`

A report summarizing experiments on ControlNet-based road-scene generation and modification.

### `two_stage_experiments.pdf`

A report summarizing the experiments that led to the proposed Two-Stage Edge-Case Generation pipeline.

### `advanced_paper_review.pdf`

A broader review of diffusion-based generative models and their potential use in autonomous-driving scenario generation.

---

## Experimental Questions

This project is organized around the following questions:

1. Can Text-to-Image models generate realistic autonomous-driving risk scenarios?
2. Can ControlNet preserve road structure while changing scene-level conditions?
3. Can img2img modify global driving context effectively?
4. Can Inpainting insert local risk factors into specific regions?
5. Is a single-stage generation process sufficient for autonomous-driving edge-case generation?
6. Why is a two-stage pipeline useful for separating global context and local risk insertion?

---

## Key Findings

- Text-to-Image generation can create visually plausible driving scenes, but it has limited control over object location and spatial relationships.
- ControlNet is useful for preserving structural information such as road layout, depth, and edge boundaries.
- img2img is effective for global scene transformation, such as changing weather or lighting conditions.
- Inpainting is more suitable for inserting local risk factors into designated areas.
- Generating global context and local risk factors in a single step is difficult to control reliably.
- A two-stage approach is more appropriate for autonomous-driving edge-case generation because it separates global scene formation from local risk-factor insertion.

---

## Environment

The experiments are based on Python and Hugging Face Diffusers.

Example installation:

```bash
pip install diffusers transformers accelerate safetensors opencv-python pillow numpy
```

Main libraries:

```text
Python
PyTorch
Diffusers
Transformers
Accelerate
Safetensors
OpenCV
Pillow
NumPy
```

Depending on the model used, GPU acceleration is strongly recommended.

---

## Example Workflow

```text
1. Prepare an input road-scene image.
2. Generate a depth map or Canny edge map as a structural condition.
3. Use ControlNet or img2img to modify the global scene context.
4. Define a mask region for local editing.
5. Use Inpainting to insert local risk factors.
6. Compare generated results and failure cases.
7. Derive the final Two-Stage Edge-Case Generation pipeline.
```

---

## GitHub Upload Notes

Some files in the original folder may exceed GitHub's standard file-size limit.  
Before uploading, it is recommended to clean the repository.

### Recommended cleanup

Remove macOS metadata files:

```bash
find . -name ".DS_Store" -delete
rm -rf __MACOSX
```

Clear notebook outputs to reduce file size:

```bash
jupyter nbconvert --clear-output --inplace "notebooks/two_stage_generation.ipynb"
jupyter nbconvert --clear-output --inplace "notebooks/controlnet_experiments.ipynb"
```

Use Git LFS for large PDF or notebook files if necessary:

```bash
git lfs install
git lfs track "*.pdf"
git lfs track "*.ipynb"
```

Recommended `.gitignore`:

```gitignore
.DS_Store
__MACOSX/
.ipynb_checkpoints/
__pycache__/
*.pyc
.env
```

---

## Suggested Future Work

- Build prompt templates for different risk-factor categories.
- Automate mask generation for pedestrians, vehicles, traffic lights, and occlusions.
- Combine ControlNet conditions with local Inpainting for more precise editing.
- Define evaluation metrics for generated risk scenarios.
- Use generated edge-case images for perception or trajectory-prediction model validation.
- Extend the framework from image generation to video or scenario-level simulation.

---

## Author

Yujin Kim
