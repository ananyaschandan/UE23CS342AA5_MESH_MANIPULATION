# UE23CS342AA5_MESH_MANIPULATION

# Cloth Physics Simulation with Mesh Manipulation

A collection of real-time cloth simulation experiments built with Three.js, demonstrating various approaches to soft-body physics and mesh manipulation.

## Overview

This project explores different techniques for simulating cloth behavior and interactions, including pinning, piercing, and cutting mechanics. The simulations use particle-based physics with constraint solving to create realistic fabric dynamics.

## Simulations Included

### 1. **Cloth with Piercing Pin**
A blue cloth suspended at the top, interacting with a moving pin that can pierce through it. The pin consists of a spherical base and a sharp conical tip.

**Features:**
- Particle-based cloth physics (30×30 grid)
- Verlet integration for realistic motion
- Constraint satisfaction for fabric cohesion
- Pin collision detection (only with the base sphere)
- Wind effects for natural movement
- Dynamic camera rotation

**Variants:**
- Standard version with larger pin base (0.08 radius)
- Fine-tuned version with tiny pin base (0.015 radius) for more precise piercing

### 2. **Cloth Cutting Simulation**
A red cloth that gets sliced cleanly in half by a moving pin, with both halves falling independently under gravity.

**Features:**
- 25×40 cloth mesh for better vertical draping
- Selective constraint removal to simulate cutting
- Physical separation of cloth halves
- Smooth camera orbit with subtle oscillation
- Pin movement across the cloth surface

## Technical Approach

### Physics Engine

The simulations use a **Verlet integration** approach combined with **constraint-based dynamics**:

1. **Particles**: Each vertex in the cloth mesh is treated as a particle with position, previous position, and pinned state
2. **Constraints**: Springs connecting adjacent particles maintain cloth structure
   - Structural constraints (horizontal and vertical)
   - Diagonal constraints (shear resistance)
3. **Verlet Integration**: Position-based physics using `position = 2 × current - previous + acceleration`
4. **Constraint Solving**: Iterative relaxation (3 iterations per frame) to satisfy distance constraints

### Cutting Mechanism

The cloth cutting is achieved by:
- Identifying constraints that cross the cutting plane
- Removing these constraints from the physics system
- Physically separating particles on either side with a gap
- Storing grid coordinates (gridX, gridY) to track particle topology

This approach allows the cloth to realistically split into two independent pieces that continue to simulate separately.

## Alternative Approaches Explored

### 1. **Rigid Body Slicing**
Initially attempted using rigid body physics with mesh boolean operations to slice geometry. This approach was abandoned because:
- Poor performance with complex mesh operations
- Difficult to maintain real-time frame rates
- Rigid bodies don't capture the fluid, flexible nature of cloth

### 2. **Cloth Dropping onto Pin**
Experimented with dropping cloth onto a stationary pin from above. This was less effective because:
- Hard to control initial conditions for consistent piercing
- Gravity-based approach made it difficult to showcase the cutting mechanics clearly
- Moving pin through stationary cloth provided better visual demonstration

The final approach of moving the pin through hanging cloth proved most effective for demonstrating both the physics and the cutting mechanics.

## Configuration Parameters

Key tunable parameters in each simulation:

```javascript
clothWidth, clothHeight  // Grid resolution
spacing                  // Distance between particles
gravity                  // Downward acceleration
damping                  // Velocity dampening (0.99 = 1% energy loss)
constraint iterations    // Stiffness (more = stiffer cloth)
```

## How to Run

1. Copy the HTML, CSS, and JavaScript code for any simulation
2. Paste into [JSFiddle](https://jsfiddle.net/) or a local HTML file
3. The simulation will start automatically
4. Three.js is loaded from CDN (r128)

## Browser Compatibility

- Requires WebGL support
- Tested on modern browsers (Chrome, Firefox, Safari, Edge)
- Best performance on hardware-accelerated systems

## Future Enhancements

- Interactive cutting with mouse/touch input
- Multiple simultaneous cuts
- Fabric tearing under stress
- Self-collision detection
- Different fabric materials (silk, denim, etc.)
- Wind field visualization

## Technical Stack

- **Three.js r128**: 3D rendering and scene management
- **Vanilla JavaScript**: Physics simulation and logic
- **WebGL**: Hardware-accelerated graphics

  ---

## 👩‍💻 Contributors

This project was created collaboratively by:

- **Trishabalakrishna**
- **Varhss04**  
- **ananyaschandan**


---

## License
Open source - feel free to use and modify for your projects!
