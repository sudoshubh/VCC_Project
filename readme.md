# VCC Project Technical Documentation

## Project Overview
This project demonstrates intelligent auto-scaling of cloud resources for a hospital system using Reinforcement Learning (RL). It simulates realistic hospital workloads, compares traditional threshold-based auto-scaling with a PPO-based RL agent, and evaluates cost and SLA violations.

## Components

### 1. Hospital Workload Simulator
- Generates realistic CPU load patterns for a hospital (busy mornings, quiet nights, emergency spikes).
- Output: DataFrame with hourly CPU load, day, hour, and emergency spike indicator.

### 2. ThresholdScaler (Baseline)
- Simulates AWS-like auto-scaling with:
  - Scale-out at CPU > 70% (with 3-hour VM spin-up delay)
  - Scale-in at CPU < 30%
  - Cooldown period (2 hours)
  - SLA violation if effective CPU > 70%
- Outputs: VM count, SLA violations, cost, and plots.

### 3. RL Environment (HospitalCloudEnv)
- Custom Gymnasium environment for RL agent.
- State: [cpu_load, current_vms, hour_of_day, trend]
- Actions: 0=hold, 1=scale_out, 2=scale_in
- Reward: Penalizes SLA violations and excessive VMs, rewards efficient scaling.

### 4. RL Agent (PPO)
- Uses Stable-Baselines3 PPO agent.
- Trained to minimize SLA violations and cost.
- Training progress and evaluation plotted.

### 5. Evaluation & Comparison
- Compares RL agent vs threshold scaler on:
  - SLA violations
  - Total VM hours
  - Average VMs running
  - Estimated cost
- Visualizes results with multiple plots.

## Sequence Diagram

![Sequence Diagram](sequence_diagram.png)

## Architecture
- **Simulator** generates workload → **ThresholdScaler** and **RL Agent** both receive same workload.
- **ThresholdScaler** applies rule-based scaling, **RL Agent** learns optimal scaling.
- Both output results for comparison.

## Cloud Integration
- The simulation mimics AWS EC2 auto-scaling logic (spin-up delay, cost per VM hour).
- Can be extended to interact with real AWS via `boto3`.

## Results Summary
- RL agent achieves fewer SLA violations and lower cost compared to threshold-based scaler.
- All results visualized and saved as PNGs for reporting.

## Files
- `VCC project 2 (1).ipynb`: Main notebook with all code, plots, and results.
- `VCC_Final_Report.docx`: Detailed report (see original for formatted content).
- `VCC_Presentation.pptx`: Project presentation slides.

## How to Run
1. Install dependencies (see first cell in notebook).
2. Run all cells in order.
3. Review generated plots and final results table.

## References
- [Stable-Baselines3](https://stable-baselines3.readthedocs.io/)
- [Gymnasium](https://gymnasium.farama.org/)
- [AWS Auto Scaling](https://aws.amazon.com/autoscaling/)

---

*For detailed results and analysis, see the notebook and the attached report/presentation.*
