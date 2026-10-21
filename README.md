# Polyhedra Sampler — OEIS A000944

**https://guillochon.github.io/polyhedra-sampler/**

[A000944](https://oeis.org/A000944) counts polyhedra by number of vertices: 1, 2, 7, 34, 257, 2606, 32300, … for
n = 4, 5, 6, … By Steinitz's theorem these are the 3-connected planar graphs, up to isomorphism. The page draws a
random sample of distinct polyhedra for every n from 4 to 40, in WebGL. A new sample takes under 100 ms; each
polyhedron's shape is computed as its row scrolls into view. The OEIS lists the counts up to n = 18; those for
n = 19 to 40 are new, computed by formula in
[oeis-results/A000944](https://github.com/guillochon/oeis-results/tree/main/A000944).

- **Triangles only.** The "Restrict faces to triangles" toggle switches to [A000109](https://oeis.org/A000109),
  the simplicial polyhedra (triangulations of the sphere): 1, 1, 2, 5, 14, 50, 233, … for n = 4, 5, 6, … The OEIS
  lists them up to n = 24; the counts for n = 25 to 40 are new, from the same computation. Link to this view with
  [`#triangles`](https://guillochon.github.io/polyhedra-sampler/#triangles). Relatives there are one edge flip or
  one edge contraction apart.
- **Colours.** One scale for both: faces by number of sides, corners by degree, each half of an edge by the corner it
  leaves. Duality swaps faces and corners, so a polyhedron and its dual trade colours.
- **Relatives.** Hover or tap a polyhedron to mark the others in the sample that are its dual, or one edge deletion
  or edge contraction away (same n, or n − 1 and n + 1).
- **Motion.** Every polyhedron spins slowly; the one under the pointer turns to face it.

## How it works

Everything runs in the browser, in one file (`index.html`).

- **Sampling.** Random points on a sphere give a random triangulation (their convex hull); random edge flips mix it
  further, then edges are deleted in random order while the graph stays 3-connected, down to a random edge count
  between 3n/2 and 3n − 6. Every polyhedron can arise, but not with equal probability.
- **Distinctness.** Each graph is reduced to a canonical code (Weinberg's method on its unique planar embedding);
  the number of starting points giving the least code is its symmetry count. Sampling reproduces A000944 exactly
  for n = 4..7 (1, 2, 7, 34 classes).
- **Geometry.** Each polyhedron is drawn in canonical form (Koebe–Andreev–Thurston): every edge touches the unit
  sphere and the touching points are centred on the origin, so symmetric graphs look symmetric. It is computed
  exactly from the primal–dual circle pattern (Newton's method on the circle radii, a convex problem), then laid out
  in the plane, mapped back to the sphere and centred by a Möbius transformation.

Made by James Guillochon with Claude. The source lives in the oeis-sniper project (`viz/A000944/`); this repo holds
the published copy.
