# Closed Chain Inverse Kinematics

An inverse kinematics solver that supports closed chains and dynamic reconfiguration based on damped least squares error minimization techniques. Inspired in part by [Marty Vona's MSim research work](https://www2.ccs.neu.edu/research/gpc/MSim/MSim-info.html) and using techniques outlined in this [2009 paper by Samuel Buss](https://math.ucsd.edu/~sbuss/ResearchWeb/ikmethods/iksurvey.pdf). Developed with some aid and advice from [Marty Vona](https://www2.ccs.neu.edu/research/gpc/vona.html).

## Model License Information

Robitics models used in the project are for demonstration purposes only and subject to the lincenses of their respective projects.

[ATHLETE](https://github.com/gkjohnson/urdf-loaders/)

[Robonaut](https://github.com/gkjohnson/nasa-urdf-robots)

# Use

## Simple 2 DoF System

```js
import { Solve, Joint, Link, Goal, DOF } from 'closed-chain-ik';

// Create links and joints
const link1 = new Link();

const joint1 = new Joint();
joint.setDoF( DOF.EZ );
joint.setPosition( 0, 1, 0 );
joint.setDoFValues( Math.PI / 4 );

const link2 = new Link();

const joint2 = new Joint();
joint.setDoF( DOF.EX );
joint.setPosition( 0, 1, 0 );
joint.setDoFValues( Math.PI / 4 );

const link3 = new Link();
link3.setPosition( 0, 1, 0 );

// Create the goal
const goal = new Goal();
link.getWorldPosition( goal.position );
link.getWorldQuaternion( goal.quaternion );

// Create structure
link1.addChild( joint1 );
joint1.addChild( link2 );
link2.addChild( joint2 );
joint2.addChild( link3 );

goal.makeClosure( link3 );

// create solver
const solver = new Solver( [ link1, goal ] );

// ...

// move the goal around and solve
solver.solve();
```

## Using a WebWorker Solver

```js
import { WorkerSolve, Joint, Link, Goal, DOF } from 'closed-chain-ik';

// ... instiate kinematic system...

const solver = new WorkerSolver( [ link1, goal ] );

// ...

// move the goal around and solve asynchronously
solver.solve();
```

# API

## Functions

TODO

## Constants

### DOF

Enumerated fields representing different degrees of freedom for Joints.

```js
// Translation DoF
DOF.X, DOF.Y, DOF.Z,

// Euler Rotation DoF
DOF.EX, DOF.EY, DOF.EZ,
```

### DOF_NAMES

An array of strings representing the names of the above degrees of freedom.

### SOLVE_STATUS

Enumerated fields representing the state of a solve result.

```js
// Error for all goals are within the threshold.
SOLVE_STATUS.CONVERGED,

// Error for the goals has begun to diverge.
SOLVE_STATUS.DIVERGED,

// Resulting angles has not changed significantly enough to reach the stall threshold.
SOLVE_STATUS.STALLED,

// The solve has reached the maximum number of allowed iterations.
SOLVE_STATUS.TIMEOUT,
```

### SOLVE_STATUS_NAMES

An array of strings representing the names of the above solve statuses.

## Frame

TODO

## Joint

_extends [Frame](#Frame)_

TODO

## Link

_extends [Frame](#Frame)_

TODO

## Goal

_extends [Joint](#Joint)_

TODO

## Solver

TODO

## WorkerSolver

TODO
