# Deep Learning Directions — When Robots Understand Surfaces

Eight reconstruction methods from the infographic *When Robots Understand Surfaces: Deep Learning Is Reinventing 3D Geometry for Autonomous Systems*.

**Ten curated GitHub repositories per method.** Official paper code first, then close cousins and shared hubs a robot team actually clones.

Pipeline this section feeds: **See surfaces → represent them (mesh / implicit / Gaussians) → act in the world.**

Toy GIFs for each idea live in [`examples/`](../examples/README.md). Run `python examples/generate_gifs.py` to rebuild them.

---

## 1. MeshSplatting — Differentiable triangulation

Optimize **connected triangles** instead of free Gaussians so the robot exports a mesh into collision checkers, grasp planners, and game engines.

Simple example in the GIF: scattered 2D points grow into a Delaunay triangle mesh — the same connectivity idea MeshSplatting enforces in 3D with restricted Delaunay triangulation.

- [meshsplatting/mesh-splatting](https://github.com/meshsplatting/mesh-splatting) — Official MeshSplatting (CVPR 2026): opaque meshes via restricted Delaunay triangulation
- [trianglesplatting/triangle-splatting](https://github.com/trianglesplatting/triangle-splatting) — Triangle Splatting for real-time radiance-field meshes (3DV 2026)
- [trianglesplatting2/triangle-splatting2](https://github.com/trianglesplatting2/triangle-splatting2) — Triangle Splatting+: opaque-triangle differentiable rendering
- [Anttwo/MILo](https://github.com/Anttwo/MILo) — Mesh-In-the-Loop Gaussian Splatting (SIGGRAPH Asia 2025)
- [Anttwo/SuGaR](https://github.com/Anttwo/SuGaR) — Surface-aligned Gaussians with extractable meshes (CVPR 2024)
- [SonSang/dmesh](https://github.com/SonSang/dmesh) — DMesh: differentiable general triangle meshes (NeurIPS 2024)
- [hbb1/2d-gaussian-splatting](https://github.com/hbb1/2d-gaussian-splatting) — 2DGS: flat Gaussian surfels and TSDF meshes (SIGGRAPH 2024)
- [AutonomousVision/gaussian-opacity-fields](https://github.com/AutonomousVision/gaussian-opacity-fields) — GOF: opacity fields + tetrahedral mesh extraction
- [NVlabs/nvdiffrec](https://github.com/NVlabs/nvdiffrec) — Differentiable marching tetrahedra mesh reconstruction
- [graphdeco-inria/gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting) — Original 3DGS baseline the mesh methods extend

---

## 2. 4Deform — Neural shape interpolation

Fill **time between sparse scans** so a deforming part, a walking person, or a grasped object becomes a continuous 4D surface.

Simple example in the GIF: a circle SDF lerps into a rounded square — topology-tolerant interpolation without needing a shared mesh.

- [Sangluisme/4Deform](https://github.com/Sangluisme/4Deform) — Official 4Deform (CVPR 2025): neural surface deformation from point clouds
- [Isabella98Liu/DG-Mesh](https://github.com/Isabella98Liu/DG-Mesh) — Dynamic Gaussian Mesh from monocular video (ICLR 2025)
- [albertpumarola/D-NeRF](https://github.com/albertpumarola/D-NeRF) — D-NeRF: canonical + deformation field for dynamic scenes
- [JonathonLuiten/Dynamic3DGaussians](https://github.com/JonathonLuiten/Dynamic3DGaussians) — Dynamic 3D Gaussians with explicit tracking
- [ingra14m/Deformable-3D-Gaussians](https://github.com/ingra14m/Deformable-3D-Gaussians) — Deformable 3DGS for monocular dynamics
- [hustvl/4DGaussians](https://github.com/hustvl/4DGaussians) — 4DGS: spacetime Gaussian primitives (CVPR 2024)
- [fudan-zvg/4d-gaussian-splatting](https://github.com/fudan-zvg/4d-gaussian-splatting) — Real-time 4D Gaussian splatting
- [wcwac/MaGS](https://github.com/wcwac/MaGS) — Mesh-adsorbed Gaussians that deform with the surface
- [hustvl/Dynamic-2DGS](https://github.com/hustvl/Dynamic-2DGS) — Dynamic 2D Gaussians for deforming objects (ACM MM 2025)
- [facebookresearch/pytorch3d](https://github.com/facebookresearch/pytorch3d) — Differentiable mesh ops used to prototype interpolation

---

## 3. SALS — Neural implicit surfaces

Represent the world as a **continuous field** (line-segment attributes, SDF, occupancy), then extract a watertight mesh a planner can use.

Simple example in the GIF: a 2D signed-distance field whose zero contour is the surface the robot would contact.

- [rsy6318/SALS](https://github.com/rsy6318/SALS) — Official SALS (ICLR 2025): Shape as Line Segments implicit surfaces
- [Totoro97/NeuS](https://github.com/Totoro97/NeuS) — NeuS: SDF volume rendering for multi-view surfaces (NeurIPS 2021)
- [19reborn/NeuS2](https://github.com/19reborn/NeuS2) — NeuS2: hash-grid NeuS, minutes instead of hours (ICCV 2023)
- [NVlabs/neuralangelo](https://github.com/NVlabs/neuralangelo) — Neuralangelo: high-fidelity hash-grid surfaces (CVPR 2023)
- [lioryariv/volsdf](https://github.com/lioryariv/volsdf) — VolSDF: volume rendering of implicit surfaces
- [autonomousvision/monosdf](https://github.com/autonomousvision/monosdf) — MonoSDF: monocular geometric cues for implicit surfaces
- [autonomousvision/sdfstudio](https://github.com/autonomousvision/sdfstudio) — Unified NeuS / VolSDF / MonoSDF / UniSurf toolbox
- [autonomousvision/unisurf](https://github.com/autonomousvision/unisurf) — UNISURF: implicit surfaces + radiance fields (ICCV 2021)
- [facebookresearch/iSDF](https://github.com/facebookresearch/iSDF) — Real-time neural SDF built for robot perception (RSS 2022)
- [NVlabs/instant-ngp](https://github.com/NVlabs/instant-ngp) — Instant-NGP hash encoding used by NeuS2 and Neuralangelo

---

## 4. MAtCha Gaussians — Gaussian + mesh

Keep splat rendering quality while **binding primitives to charts / a mesh** so the same model can be rendered *and* collided against.

Simple example in the GIF: elliptical Gaussian surfels riding on a deforming polyline — appearance stuck to geometry.

- [Anttwo/MAtCha](https://github.com/Anttwo/MAtCha) — Official MAtCha Gaussians (CVPR 2025 Spotlight): mesh as an atlas of charts + 2D Gaussian surfels
- [Anttwo/MILo](https://github.com/Anttwo/MILo) — Differentiable mesh extracted from Gaussians every training step
- [Anttwo/SuGaR](https://github.com/Anttwo/SuGaR) — Gaussians aligned to a surface, then meshed
- [wcwac/MaGS](https://github.com/wcwac/MaGS) — Mesh-adsorbed Gaussian Splatting (ICCV 2025 Highlight)
- [hbb1/2d-gaussian-splatting](https://github.com/hbb1/2d-gaussian-splatting) — Surfels that sit on the surface instead of floating in volume
- [AutonomousVision/gaussian-opacity-fields](https://github.com/AutonomousVision/gaussian-opacity-fields) — Opacity-field meshing from 3DGS
- [meshsplatting/mesh-splatting](https://github.com/meshsplatting/mesh-splatting) — Opaque connected triangles from a splat-style pipeline
- [zju3dv/PGSR](https://github.com/zju3dv/PGSR) — Planar-based Gaussian surface reconstruction
- [hwanhuh/mesh2gaussian](https://github.com/hwanhuh/mesh2gaussian) — CUDA mesh → Gaussian converter for hybrid pipelines
- [graphdeco-inria/gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting) — 3DGS appearance backbone

---

## 5. DN-Splatter — Depth / normal-guided surface

Regularize Gaussians with **monocular or sensor depth and normals** so textureless bins, walls, and metal parts still reconstruct.

Simple example in the GIF: a bump's depth map and RGB-coded normals moving together — the two cues DN-Splatter adds to 3DGS.

- [maturk/dn-splatter](https://github.com/maturk/dn-splatter) — Official DN-Splatter (WACV 2025): depth + normal priors and mesh export
- [XuqianRen/AGS_Mesh](https://github.com/XuqianRen/AGS_Mesh) — AGS-Mesh: filtered depth/normals and octree isosurfaces
- [hbb1/2d-gaussian-splatting](https://github.com/hbb1/2d-gaussian-splatting) — Geometry-accurate 2D Gaussian surfels
- [zju3dv/PGSR](https://github.com/zju3dv/PGSR) — Planar Gaussian Splatting for high-fidelity surfaces
- [DepthAnything/Depth-Anything-V2](https://github.com/DepthAnything/Depth-Anything-V2) — Strong monocular depth prior used by DN-style pipelines
- [baegwangbin/surface_normal_uncertainty](https://github.com/baegwangbin/surface_normal_uncertainty) — Learned surface normals with uncertainty
- [StableNormal/StableNormal](https://github.com/StableNormal/StableNormal) — Stable monocular normal estimator for indoor/outdoor scenes
- [NVlabs/FoundationStereo](https://github.com/NVlabs/FoundationStereo) — Foundation stereo depth for robot RGB pairs
- [autonomousvision/monosdf](https://github.com/autonomousvision/monosdf) — Depth + normal cues inside an implicit surface
- [graphdeco-inria/gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting) — Unregularized 3DGS baseline

---

## 6. MaGS — Dynamic neural mesh

Keep Gaussians **adsorbed to a mesh** so the model can render *and* deform under physics, SMPL, or a teleop command.

Simple example in the GIF: the same surfels from card 4 riding a waving surface — renderable appearance glued to a simulatable mesh.

- [wcwac/MaGS](https://github.com/wcwac/MaGS) — Official MaGS (ICCV 2025 Highlight): mesh-adsorbed dynamic Gaussians
- [Isabella98Liu/DG-Mesh](https://github.com/Isabella98Liu/DG-Mesh) — Time-consistent dynamic meshes from monocular video
- [zju3dv/street_gaussians](https://github.com/zju3dv/street_gaussians) — Street Gaussians for dynamic outdoor scenes (ECCV 2024)
- [ingra14m/Deformable-3D-Gaussians](https://github.com/ingra14m/Deformable-3D-Gaussians) — Deformation-field 3DGS
- [JonathonLuiten/Dynamic3DGaussians](https://github.com/JonathonLuiten/Dynamic3DGaussians) — Tracked dynamic 3D Gaussians
- [hustvl/4DGaussians](https://github.com/hustvl/4DGaussians) — 4DGS spacetime representation (CVPR 2024)
- [hustvl/Dynamic-2DGS](https://github.com/hustvl/Dynamic-2DGS) — Dynamic 2D Gaussians for object meshes
- [albertpumarola/D-NeRF](https://github.com/albertpumarola/D-NeRF) — Canonical dynamic NeRF prior
- [Sangluisme/4Deform](https://github.com/Sangluisme/4Deform) — Neural surface interpolation used as a motion prior
- [graphdeco-inria/gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting) — Static 3DGS starting point

---

## 7. SurfaceSplat — Neural surface + splatting

Let an **SDF hold global geometry** while Gaussians hold appearance, then refine each with the other.

Simple example in the GIF: depth/normal cues (card 5) plus splat ellipses (card 4) — hybrid geometry + appearance.

- [aim-uofa/SurfaceSplat](https://github.com/aim-uofa/SurfaceSplat) — Official SurfaceSplat (ICCV 2025): SDF ↔ 3DGS co-training
- [hebing-sjtu/SurfSplat](https://github.com/hebing-sjtu/SurfSplat) — SurfSplat: feed-forward 2DGS with surface continuity (ICLR 2026)
- [hbb1/2d-gaussian-splatting](https://github.com/hbb1/2d-gaussian-splatting) — 2DGS surface-aligned primitives
- [Anttwo/SuGaR](https://github.com/Anttwo/SuGaR) — Surface-aligned 3DGS and mesh baking
- [maturk/dn-splatter](https://github.com/maturk/dn-splatter) — Depth/normal-guided splat surfaces
- [zju3dv/PGSR](https://github.com/zju3dv/PGSR) — Planar-based Gaussian surface reconstruction
- [Anttwo/MILo](https://github.com/Anttwo/MILo) — Mesh extracted inside the splat training loop
- [Totoro97/NeuS](https://github.com/Totoro97/NeuS) — SDF side of the hybrid
- [rsy6318/SALS](https://github.com/rsy6318/SALS) — Alternative implicit surface representation
- [graphdeco-inria/gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting) — Splat side of the hybrid

---

## 8. Neural Disparity Refinement — Learned depth interpolation

Turn **noisy stereo, SfM, or LiDAR depths** into dense maps the other seven methods can train on.

Simple example in the GIF: a noisy disparity map sharpens into a clean surface — the job of a refinement network before meshing.

- [CVLAB-Unibo/neural-disparity-refinement](https://github.com/CVLAB-Unibo/neural-disparity-refinement) — Official Neural Disparity Refinement (3DV 2021 / TPAMI 2024)
- [princeton-vl/RAFT-Stereo](https://github.com/princeton-vl/RAFT-Stereo) — RAFT-Stereo iterative matching
- [NVlabs/FoundationStereo](https://github.com/NVlabs/FoundationStereo) — Foundation model for stereo depth
- [gangweiX/IGEV](https://github.com/gangweiX/IGEV) — IGEV-Stereo iterative geometry encoding
- [autonomousvision/unimatch](https://github.com/autonomousvision/unimatch) — UniMatch unified matching for stereo and flow
- [megvii-research/CREStereo](https://github.com/megvii-research/CREStereo) — CREStereo hierarchical refinement
- [DepthAnything/Depth-Anything-V2](https://github.com/DepthAnything/Depth-Anything-V2) — Monocular depth to densify incomplete scans
- [nianticlabs/monodepth2](https://github.com/nianticlabs/monodepth2) — Self-supervised monocular depth baseline
- [princeton-vl/RAFT](https://github.com/princeton-vl/RAFT) — Optical-flow ancestor of RAFT-Stereo
- [colmap/colmap](https://github.com/colmap/colmap) — SfM/MVS depths that NDR is designed to refine
