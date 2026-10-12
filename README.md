# Board Game Robot Arm

A self-designed 4-DOF robot arm that plays board games against a human, using a camera to see the board and its own inverse kinematics to move the pieces. Chess first, other games as plug-in modules.

> 🚧 Work in progress (Winter 2026/27). Current phase: **Phase 1 – Arm**

<!-- TODO: replace with a GIF of the arm making a move -->
![Demo](media/demo.gif)

## What it does

- [ ] Moves chess pieces to any square using analytically derived inverse kinematics
- [ ] Detects the human's move with an overhead camera (ArUco calibration + occupancy change)
- [ ] Plays complete games against Stockfish, including captures, castling and promotion
- [ ] Waits until no hand is above the board before moving (MediaPipe Hands)
- [ ] Checks every placement with the camera and corrects it
- [ ] Runs a second game on the same platform without changing arm or vision code

## Results

| Metric | Target | Measured |
| --- | --- | --- |
| Placement accuracy | ±3 mm | – |
| Move detection rate | > 98 % (200 moves) | – |
| Grasp success rate | – | – |
| Time per robot move | – | – |

## System architecture

<!-- TODO: architecture diagram (media/architecture.png) -->

Game modules (chess, ...) only see the board state and return a move as a list of actions. Vision, motion planning and servo control are game-agnostic.

## Hardware

- 5× Feetech STS3215 serial bus servos (4 joints + gripper), 12 V
- 3D-printed links (PETG), designed in Fusion 360 – STEP files in [`cad/`](cad/)
- USB camera on an overhead mount, ArUco markers on the board corners

## Repository structure

```
cad/        STEP exports of all parts
docs/       kinematics derivation, measurement logs, design decisions
src/arm/    servo interface, inverse kinematics, trajectories
src/vision/ calibration, board and hand detection
src/games/  game modules (chess, ...)
tests/      unit tests (e.g. forward(inverse(x)) == x)
media/      images and GIFs for this README
```

## Getting started

<!-- TODO: installation and usage once Phase 1 is done -->

## Roadmap

1. **Arm** – design, build, inverse kinematics, pick & place by board coordinates
2. **Play** – camera calibration, move detection, Stockfish, first complete game
3. **Robustness** – ROS 2 nodes, hand detection, placement correction, measurements
4. **Extension** – second game, video, documentation

## License

MIT – see [LICENSE](LICENSE)
