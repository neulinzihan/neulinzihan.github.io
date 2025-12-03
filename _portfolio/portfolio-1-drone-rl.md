---
title: "Drone Coverage Optimization with Reinforcement Learning"
excerpt: "Q-learning-based multi-drone placement for disaster response coverage<br/><img src='/images/500x300.png'>"
collection: portfolio
---

## Overview

Designed and implemented a reinforcement learning system for optimizing drone placement in disaster response scenarios, achieving 100% area coverage with minimal resources.

## Key Achievements

- Developed Q-learning-based drone placement policy achieving **100% area coverage with only 4 drones**
- Outperformed PPO and MCTS baselines in coverage efficiency
- Implemented **A\* pathfinding** for emergency responder navigation
- Built global environment mapping module for real-time 2D map construction
- Verified convergence over **20,000+ training episodes** across multiple grid sizes

## Technical Stack

- **Languages**: Python
- **Algorithms**: Q-Learning, A* Pathfinding, SLAM-inspired mapping
- **Tools**: NumPy, Matplotlib, OpenAI Gym

## System Architecture

*[Add architecture diagram here]*

## Results

| Method | Drones Required | Coverage | Overlap |
|--------|----------------|----------|---------|
| Q-Learning (Ours) | 4 | 100% | Minimal |
| PPO | 6 | 98% | Moderate |
| MCTS | 5 | 95% | High |

## Links

- [GitHub Repository](#) *(add link if public)*
- [Project Report](/files/paper1.pdf) *(add if available)*
