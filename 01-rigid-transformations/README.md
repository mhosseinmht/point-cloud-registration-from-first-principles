# Introduction

In this chapter, we briefly introduce some fundamental concepts needed to understand point cloud registration. We first explain what a point cloud is and how 3D data can be represented. Then, we discuss rigid transformations and their mathematical representation using rotation and translation. Finally, we introduce the point cloud registration problem and explain how rigid transformations are used to align two point clouds.

# Point Cloud

A point cloud is a collection of discrete 3D data points in space that together represent the external surface geometry of an object, building, or landscape. Every individual point is defined by Cartesian coordinates (X, Y, Z). The points can also store extra data like RGB color values, laser intensity, surface normals, or timestamps, namely "attributes".  Common formats to store a point cloud data include PLY, PCD, LAS, LAZ, E57, and OBJ. Some well-known sensors with the output data in the form of point clouds are: LiDAR Scanners, Radars, and RGB-D / Depth Cameras.

# Rigid Transformations

A rigid transformation is a geometric transformation that preserves distances, angles, and shapes (rigid). It is a combination of translation and rotation. In other words, when a figure undergoes a rigid transformation, it is translated and/or rotated without changing its orignial size or shape. This concept is shown in Fig. 1.

<p align="center">
  <img src="figures/rigid_transformation.png" width="600">
</p>

<p align="center">
  <em>Figure 1: Rigid transformation = translation + rotation.</em>
</p>

For a 3D point $\mathbf{p}$, the transformed point $\mathbf{p}'$ is

$$
\mathbf{p}' = R\mathbf{p} + \mathbf{t}
$$

where

- $R \in \mathbb{R}^{3 \times 3}$ is the rotation matrix,
- $\mathbf{t} \in \mathbb{R}^{3}$ is the translation vector.

The rotation matrix satisfies

```math
R^T R = I
```

and

```math
\det(R) = 1
```

Therefore,

```math
R \in SO(3)
```

Using homogeneous coordinates, the rigid transformation can be written as

```math
T =
\begin{bmatrix}
R & \mathbf{t} \\
\mathbf{0}^T & 1
\end{bmatrix}
```

where $T \in SE(3)$.

# Point Cloud Registration

The concept of rigid transformation is fundamental to point cloud registration. To match (register) a point cloud $P_j$ with another point cloud $P_i$, the goal is to find the rotation and translation that best align the corresponding regions of the two point clouds. This concept is illustrated in Fig. 2.

<p align="center">
  <img src="figures/pointcloud-registration.png" width="500">
</p>

<p align="center">
  <em>Figure 2: Point cloud registration. Two initially misaligned point clouds are aligned by estimating the rigid transformation between them.</em>
</p>

One common approach to solving this problem is to identify corresponding points between the two point clouds and then estimate the rigid transformation that minimizes the alignment error between these correspondences.

Therefore, in the next chapter, we will discuss some common strategies for finding point correspondences.
