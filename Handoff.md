# gazebo-sim-tutorial-kr — Codex Handoff

## 1. 문서 목적

이 문서는 `gazebo-sim-tutorial-kr` 저장소를 로컬 Codex가 초기화하고, 이후 튜토리얼 문서와 예제 코드를 일관된 구조로 확장하기 위한 작업 지침서이다.

이 프로젝트의 핵심 목표는 **Ubuntu 24.04 LTS + ROS 2 Jazzy + Gazebo Harmonic 환경을 위한 한국어 Gazebo Sim 튜토리얼을 만들고, 동일한 GitHub 저장소에서 문서와 실행 가능한 예제 코드를 함께 관리하며, 문서 사이트를 GitHub Pages로 공개하는 것**이다.

Codex는 이 문서를 프로젝트의 기본 설계 명세로 취급한다. 구조 변경이 필요한 경우 임의로 크게 변경하지 말고, 기존 규칙과 호환성을 우선한다.

---

## 2. 프로젝트 목표

### 2.1 주요 목표

1. Gazebo Harmonic을 기준으로 한 체계적인 Gazebo Sim 튜토리얼을 작성한다.
2. Ubuntu 24.04 LTS + ROS 2 Jazzy + Gazebo Harmonic을 유일한 본편 지원 환경으로 한다.
3. 튜토리얼은 초급, 중급, 고급의 세 단계로 구성한다.
4. 설명 문서는 코드 자체를 제외하면 최대한 한국어로 작성한다.
5. 모든 문서는 Markdown으로 관리한다.
6. 튜토리얼에서 사용하는 이미지, GIF, 짧은 동영상 등 설명용 미디어는 모두 `docs/images/` 아래에 둔다.
7. 문서 사이트는 MkDocs 기반으로 생성하고 GitHub Pages로 공개한다.
8. 문서와 실행 가능한 예제 코드는 하나의 GitHub 저장소에서 함께 관리한다.
9. 각 예제는 가능한 한 실제로 실행 가능하고 재현 가능해야 한다.
10. 초급부터 고급까지 하나의 공통 로봇인 `tutorial_bot`을 점진적으로 발전시키는 방식으로 구성한다.

### 2.2 교육 목표

튜토리얼을 끝까지 학습한 사용자는 다음 능력을 갖추는 것을 목표로 한다.

- **초급:** Gazebo를 설치하고, SDF world와 URDF / Xacro robot을 만들고, 센서를 추가하며, ROS 2와 Gazebo를 연결할 수 있다.
- **중급:** ROS 2 Launch, TF, RViz, `ros_gz_bridge`, `gz_ros2_control`, Nav2 등을 포함한 실제 로봇 시뮬레이션 프로젝트를 구성할 수 있다.
- **고급:** Gazebo의 ECS 구조를 이해하고, C++ System Plugin, Gazebo Transport, headless simulation, 자동화 테스트 및 CI를 구성할 수 있다.

튜토리얼 전반에서 다음 기초를 필요한 시점에 함께 설명한다.

- SI 단위, 오른손 좌표계, ROS 좌표계 관례와 TF 구조
- simulation time, `/clock`, `use_sim_time`
- Gazebo Transport와 ROS 2 DDS의 차이, bridge 방향과 QoS
- inertia, collision, friction, sensor noise, update rate 등 시뮬레이션 정확성의 기초

---

## 3. 지원 환경 정책

### 3.1 기본 지원 조합

| Ubuntu | ROS 2 | Gazebo | Architecture | GPU | 지원 수준 |
|---|---|---|---|---|---|
| Ubuntu 24.04 LTS | Jazzy | Harmonic | amd64 | NVIDIA | 본편 지원 및 검증 환경 |

본편은 위 조합만 지원한다. ARM64, AMD / Intel GPU, WSL, 가상 머신 및 다른 운영체제는 지원이나 검증 대상으로 고려하지 않는다.

### 3.2 Future work

Ubuntu 22.04 LTS + ROS 2 Humble + Gazebo Fortress 튜토리얼은 Jazzy + Harmonic 본편이 모두 완료된 이후 별도 단계에서 진행한다. 본편을 작성하는 동안 Humble / Fortress용 문서 분기, 조건부 코드 또는 예제 복제를 만들지 않는다.

공개 로봇의 URDF / Xacro, 다양한 Gazebo world, Open-RMF multi-floor 시나리오를 모은 Asset Bank도 본편 완료 이후의 future work로 둔다. 본편 작업 중에는 Asset Bank의 구조나 자산을 미리 구현하지 않는다.

### 3.3 각 튜토리얼 페이지의 호환성 표시

가능하면 각 주요 문서 상단에 다음 정보를 제공한다.

```markdown
> **난이도:** 초급  
> **Gazebo:** Harmonic  
> **ROS 2:** Jazzy  
> **Ubuntu:** 24.04  
> **Architecture / GPU:** amd64 / NVIDIA  
> **선행 학습:** SDF 기본
```

특정 조합에서 제한 사항이 있으면 해당 위치에 경고 문구를 추가한다.

---

## 4. 기술 스택

### 문서

- Markdown
- MkDocs
- Material for MkDocs
- GitHub Pages
- GitHub Actions

### 시뮬레이션

- Gazebo Harmonic
- SDF
- Gazebo Transport
- Gazebo System Plugin
- Gazebo Fuel

### ROS 2

- ROS 2 Jazzy
- `ros_gz`
- `ros_gz_bridge`
- `gz_ros2_control`
- `robot_state_publisher`
- RViz
- Nav2

### 코드

- C++
- Python
- XML / SDF / URDF / Xacro
- YAML
- CMake
- ROS 2 `ament_cmake` / `ament_python`은 예제 특성에 따라 사용

---

## 5. 권장 저장소 구조

초기 저장소는 다음 구조를 기준으로 만든다.

```text
gazebo-sim-tutorial-kr/
├── README.md
├── Handoff.md
├── LICENSE
├── CONTRIBUTING.md
├── mkdocs.yml
├── requirements-docs.txt
│
├── docs/
│   ├── index.md
│   ├── roadmap.md
│   ├── compatibility.md
│   │
│   ├── getting-started/
│   │   ├── gazebo-harmonic.md
│   │   ├── installation-jazzy.md
│   │   └── troubleshooting.md
│   │
│   ├── beginner/
│   │   ├── index.md
│   │   ├── 01-gazebo-overview.md
│   │   ├── 02-gui-basics.md
│   │   ├── 03-sdf-basics.md
│   │   ├── 04-first-world.md
│   │   ├── 05-first-robot.md
│   │   ├── 06-joints.md
│   │   ├── 07-diff-drive.md
│   │   ├── 08-sensors.md
│   │   ├── 09-gazebo-fuel.md
│   │   ├── 10-ros-gz-bridge.md
│   │   └── project-tutorial-bot.md
│   │
│   ├── intermediate/
│   │   ├── index.md
│   │   ├── 01-advanced-sdf.md
│   │   ├── 02-urdf-xacro-sdf.md
│   │   ├── 03-ros2-launch.md
│   │   ├── 04-spawn-model.md
│   │   ├── 05-bridge-config.md
│   │   ├── 06-tf-joint-state-rviz.md
│   │   ├── 07-gz-ros2-control.md
│   │   ├── 08-advanced-sensors.md
│   │   ├── 09-multi-robot.md
│   │   ├── 10-nav2-integration.md
│   │   └── project-autonomous-bot.md
│   │
│   ├── advanced/
│   │   ├── index.md
│   │   ├── 01-gazebo-architecture.md
│   │   ├── 02-ecs.md
│   │   ├── 03-system-plugin.md
│   │   ├── 04-gazebo-transport.md
│   │   ├── 05-custom-interface.md
│   │   ├── 06-custom-sensor-actuator.md
│   │   ├── 07-physics.md
│   │   ├── 08-large-scale-simulation.md
│   │   ├── 09-logging-debugging.md
│   │   ├── 10-headless-simulation.md
│   │   ├── 11-automated-testing.md
│   │   ├── 12-github-actions-ci.md
│   │   ├── 13-classic-migration.md
│   │   └── project-production-sim-stack.md
│   │
│   ├── reference/
│   │   ├── commands.md
│   │   ├── terminology.md
│   │   ├── package-map.md
│   │   └── troubleshooting.md
│   │
│   └── images/
│       ├── getting-started/
│       ├── beginner/
│       ├── intermediate/
│       ├── advanced/
│       └── shared/
│
├── examples/
│   ├── gazebo/
│   │   ├── worlds/
│   │   ├── models/
│   │   └── sdf/
│   │
│   └── ros2_ws/
│       └── src/
│           ├── tutorial_bot_description/
│           ├── tutorial_bot_gazebo/
│           ├── tutorial_bot_bringup/
│           ├── tutorial_bot_control/
│           ├── tutorial_bot_plugins/
│           └── tutorial_bot_tests/
│
├── scripts/
│   ├── check_links.py
│   ├── check_examples.sh
│   └── setup_dev_env.sh
│
└── .github/
    └── workflows/
        ├── pages.yml
        └── test.yml
```

---

## 6. 디렉터리별 역할

### `docs/`

웹사이트에 표시되는 모든 Markdown 문서를 보관한다.

문서 사이트의 source of truth이다.

### `docs/images/`

Markdown에서 참조하는 모든 설명용 미디어 파일을 보관한다.

다음 파일 종류를 포함할 수 있다.

- PNG
- JPEG
- SVG
- WebP
- GIF
- 짧은 MP4/WebM

긴 동영상은 저장소 크기를 불필요하게 키울 수 있으므로 가능하면 외부 영상 호스팅을 사용하고 Markdown에서는 링크 또는 embed 형태로 참조한다.

이미지 및 미디어 파일을 `docs/`의 다른 위치에 흩어놓지 않는다.

### `examples/gazebo/`

ROS 2에 종속되지 않는 순수 Gazebo / SDF 예제를 보관한다.

예:

- 최소 world
- primitive model
- joint 예제
- sensor 예제
- standalone SDF model

### `examples/ros2_ws/`

ROS 2와 Gazebo가 함께 필요한 실행 가능한 workspace를 보관한다.

가능한 한 `tutorial_bot`을 공통 예제로 사용한다.

### `scripts/`

개발 환경 구성, 링크 검사, 예제 검증 등 반복 작업을 자동화한다.

### `.github/workflows/`

GitHub Pages 배포와 CI를 구성한다.

---

## 7. GitHub Pages 배포 구조

문서 source는 `docs/`이며, `mkdocs.yml`을 통해 정적 사이트를 생성한다.

기본 흐름은 다음과 같다.

```text
docs/*.md
   │
   ▼
MkDocs
   │
   ▼
Static Site
   │
   ▼
GitHub Actions
   │
   ▼
GitHub Pages
```

빌드 결과물인 `site/` 디렉터리는 저장소에서 직접 관리하지 않는다.

GitHub Actions가 매 배포 시 문서를 빌드하고 Pages artifact로 배포하도록 한다.

Project Pages 형태를 기본으로 가정한다.

```text
https://<username>.github.io/gazebo-sim-tutorial-kr/
```

---

## 8. 튜토리얼 전체 교육 구조

튜토리얼은 다음 세 단계로 나눈다.

```text
Beginner
   │
   ▼
Intermediate
   │
   ▼
Advanced
```

각 단계는 독립적인 예제 모음이 아니라, 하나의 `tutorial_bot`을 계속 발전시키는 형태로 연결한다.

```text
초급
tutorial_bot
2-wheel + DiffDrive + LiDAR + Camera
           │
           ▼
중급
tutorial_bot
TF + ros2_control + RViz + Nav2
           │
           ▼
고급
tutorial_bot
Custom Plugin + Tests + CI + Advanced Simulation
```

---

# 9. 초급 튜토리얼

## 목표

초급을 끝낸 사용자는 다음을 할 수 있어야 한다.

- Gazebo Harmonic 실행
- Gazebo GUI 기본 사용
- SDF 구조 이해
- SDF world와 URDF / Xacro robot 작성
- joint와 DiffDrive 구성
- Camera / LiDAR / IMU 등의 센서 추가
- Gazebo Transport topic 확인
- Gazebo와 ROS 2 topic 연결

C++ 프로그래밍은 초급의 필수 요구 사항으로 두지 않는다.

---

## 9.1 Gazebo 개요

다룰 내용:

- Gazebo Sim이란 무엇인가
- Gazebo Classic과 현재 Gazebo의 용어 차이
- Gazebo Harmonic
- Server와 GUI
- Gazebo Transport
- ROS 2와 Gazebo의 관계
- `gz` CLI 개요

주요 명령:

```bash
gz sim
gz topic
gz service
gz model
```

---

## 9.2 Gazebo GUI 기초

다룰 내용:

- Gazebo 실행
- Play / Pause
- Simulation Step
- 카메라 이동
- Entity 선택
- Translate / Rotate
- Entity Tree
- Component Inspector

---

## 9.3 SDF 기초

다룰 내용:

- SDF란 무엇인가
- `<sdf>`
- `<world>`
- `<model>`
- `<link>`
- `<visual>`
- `<collision>`
- `<pose>`

최소한의 SDF 파일을 직접 작성한다.

---

## 9.4 첫 World 만들기

다룰 내용:

- Ground Plane
- Light
- Box
- Sphere
- Cylinder
- Static model
- World 저장
- 직접 만든 world 실행

---

## 9.5 URDF / Xacro로 첫 Robot 만들기

다룰 내용:

- URDF와 Xacro의 역할
- Robot model
- Link
- Collision
- Visual
- Mass
- Inertia 기초

URDF / Xacro를 원본으로 `tutorial_bot`의 base model을 만든다.

---

## 9.6 Joint

다룰 내용:

- Revolute joint
- Fixed joint
- Joint axis
- Joint limit

`tutorial_bot`에 좌우 바퀴를 추가한다.

---

## 9.7 DiffDrive

다룰 내용:

- Differential Drive 구조
- Gazebo DiffDrive System
- `cmd_vel`
- Odometry
- Gazebo topic을 이용한 수동 제어

---

## 9.8 Sensor

다룰 내용:

- Camera
- LiDAR
- IMU
- Contact Sensor
- update rate
- sensor topic 확인

`tutorial_bot`에 LiDAR와 Camera를 추가한다.

---

## 9.9 Gazebo Fuel

다룰 내용:

- Gazebo Fuel이 무엇인가
- 모델 검색
- Fuel model include
- URI
- resource path

---

## 9.10 ROS 2와 연결

다룰 내용:

- Gazebo Transport와 ROS 2 topic의 차이
- `ros_gz_bridge`
- ROS → Gazebo
- Gazebo → ROS
- `/clock`
- `/cmd_vel`
- `/scan`
- `/imu`
- image topic

---

## 9.11 초급 프로젝트

### Project 1 — `tutorial_bot`

최종 목표:

```text
tutorial_bot
├── Differential Drive
├── LiDAR
├── Camera
└── IMU
```

데이터 흐름:

```text
ROS 2
   │
   │ /cmd_vel
   ▼
ros_gz_bridge
   │
   ▼
Gazebo
   │
   ├── DiffDrive
   ├── LiDAR
   ├── Camera
   └── IMU
```

완료 조건:

- Gazebo에서 로봇이 정상 spawn된다.
- ROS 2에서 `/cmd_vel`을 보내 로봇을 움직일 수 있다.
- ROS 2에서 최소 LiDAR와 IMU 데이터를 받을 수 있다.
- 가능하면 Camera 데이터도 확인한다.

---

# 10. 중급 튜토리얼

## 목표

중급을 끝낸 사용자는 실제 ROS 2 프로젝트 형태의 Gazebo simulation stack을 구성할 수 있어야 한다.

---

## 10.1 Advanced SDF

다룰 내용:

- Frame
- Relative Pose
- Nested Model
- Include
- Model URI
- Mesh
- Material
- Collision geometry
- Inertia
- Friction
- Joint limit
- Physics parameters

---

## 10.2 URDF / Xacro / SDF

다룰 내용:

- URDF와 SDF의 차이
- Xacro의 역할
- ROS `robot_description`
- Gazebo에서의 model description
- `tutorial_bot`은 URDF / Xacro를 robot description의 source of truth로 사용
- SDF는 world와 Gazebo 고유 기능에 사용하고, 로봇 모델의 중복 원본으로 관리하지 않음
- Gazebo 전용 설정을 URDF / Xacro와 연결하는 방법

---

## 10.3 ROS 2 Launch

최종적으로 다음 한 줄로 simulation을 실행하는 구조를 만든다.

```bash
ros2 launch tutorial_bot_bringup simulation.launch.py
```

실행 대상 예:

```text
simulation.launch.py
├── Gazebo
├── Robot Spawn
├── robot_state_publisher
├── ros_gz_bridge
├── ros2_control
└── RViz
```

---

## 10.4 Robot Spawn

다룰 내용:

- SDF 또는 robot description으로 model spawn
- ROS 2에서 Gazebo entity 생성
- namespace
- spawn pose

---

## 10.5 ros_gz_bridge 심화

다룰 내용:

- YAML configuration
- ROS_TO_GZ
- GZ_TO_ROS
- BIDIRECTIONAL
- namespace
- remapping
- QoS
- 여러 topic 일괄 설정

예제 설정은 다음 위치에 둔다.

```text
tutorial_bot_bringup/
└── config/
    └── bridge.yaml
```

---

## 10.6 TF / Joint State / RViz

다룰 내용:

```text
map
└── odom
    └── base_link
        ├── left_wheel_link
        ├── right_wheel_link
        ├── lidar_link
        └── camera_link
```

- `robot_state_publisher`
- Joint State
- TF tree
- Gazebo와 RViz의 역할 차이
- Sensor visualization

---

## 10.7 gz_ros2_control

다룰 내용:

- `ros2_control`
- `controller_manager`
- Hardware interface 개념
- Position interface
- Velocity interface
- Effort interface
- `joint_state_broadcaster`
- `joint_trajectory_controller`
- controller YAML
- Gazebo와 ros2_control 연결

---

## 10.8 Sensor 심화

다룰 내용:

- Noise
- Update Rate
- FOV
- Resolution
- Camera intrinsic
- Depth Camera
- PointCloud
- IMU noise
- LiDAR parameter

---

## 10.9 Multi Robot

다룰 내용:

```text
/world
├── robot1
│   ├── /robot1/cmd_vel
│   └── /robot1/scan
└── robot2
    ├── /robot2/cmd_vel
    └── /robot2/scan
```

- Namespace
- Topic remapping
- TF namespace
- 여러 robot spawn
- resource 공유

---

## 10.10 Nav2 Integration

Gazebo에서 Nav2 전체 기능을 설명하는 것이 아니라, **Nav2가 Gazebo simulation에서 동작하기 위해 필요한 입력과 데이터 흐름**을 중심으로 설명한다.

```text
Gazebo
├── LiDAR
├── Odometry
└── TF
     │
     ▼
    Nav2
     │
     │ /cmd_vel
     ▼
tutorial_bot
```

다룰 내용:

- Odometry
- TF
- LaserScan
- `/cmd_vel`
- map / odom / base_link frame
- 최소 Nav2 실행 예제

---

## 10.11 중급 프로젝트

### Project 2 — Autonomous `tutorial_bot`

목표:

```text
URDF / Xacro
     │
     ▼
tutorial_bot
     │
     ├── ros2_control
     ├── TF
     ├── LiDAR
     └── Odometry
            │
            ▼
           Nav2
```

완료 조건:

- 하나의 ROS 2 launch 명령으로 전체 simulation이 시작된다.
- Gazebo와 RViz가 정상적으로 연동된다.
- TF tree가 올바르게 생성된다.
- controller가 정상 실행된다.
- Nav2를 통해 간단한 goal 이동이 가능하다.

---

# 11. 고급 튜토리얼

## 목표

고급을 끝낸 사용자는 Gazebo 자체의 동작을 확장하고 simulation을 자동 검증할 수 있어야 한다.

C++ 사용을 기본으로 한다.

---

## 11.1 Gazebo Architecture

다룰 내용:

```text
gz sim
├── Server
│   ├── Physics
│   ├── Sensors
│   └── System Plugins
└── GUI
    ├── Rendering
    └── GUI Plugins
```

- Server / GUI 분리
- Simulation update loop
- Transport
- Plugin architecture

---

## 11.2 Entity Component System

다룰 내용:

- Entity
- Component
- System
- EntityComponentManager
- Component query
- Update cycle

---

## 11.3 C++ System Plugin

기본 형태:

```cpp
class MySystem
  : public gz::sim::System,
    public gz::sim::ISystemConfigure,
    public gz::sim::ISystemPreUpdate
{
};
```

다룰 내용:

- Configure
- PreUpdate
- Update
- PostUpdate
- Plugin registration
- SDF에서 plugin load
- CMake 구성

예제 후보:

- Custom velocity controller
- Force application plugin
- Battery simulation
- Collision event detector

코드는 다음 패키지에 위치시킨다.

```text
examples/ros2_ws/src/tutorial_bot_plugins/
```

---

## 11.4 Gazebo Transport

다룰 내용:

- `gz::transport::Node`
- Publisher
- Subscriber
- Topic
- Request / Reply
- Service
- Message
- topic introspection
- transport debugging

---

## 11.5 Custom ROS ↔ Gazebo Interface

다룰 내용:

- Gazebo message
- ROS message
- custom bridge가 필요한 상황
- 메시지 변환 구조
- namespace / topic 설계

---

## 11.6 Custom Sensor / Actuator

예제 후보:

- Custom Sensor
- Motor dynamics
- Battery model
- Wheel slip
- Custom actuator
- Aerodynamic effect
- Hydrodynamic effect

모든 내용을 한 번에 구현할 필요는 없다.

대표 예제를 하나 이상 완성하고 나머지는 확장 과제로 둘 수 있다.

---

## 11.7 Physics

다룰 내용:

- Simulation step size
- Real Time Factor
- Solver
- Contact
- Collision
- Friction
- Joint constraint
- Numerical stability
- 정확도와 성능의 trade-off

---

## 11.8 Large-scale Simulation

다룰 내용:

- Headless mode
- Multi robot
- Large world
- Resource loading
- 성능 측정
- simulation update rate
- 필요 시 distributed simulation 개념

---

## 11.9 Logging / Debugging

다룰 내용:

- verbose log
- topic inspection
- component inspection
- resource path 문제
- plugin loading 문제
- physics debugging
- simulation record / replay

---

## 11.10 Headless Simulation

GUI 없이 server만 실행하는 예제를 만든다.

목표:

```text
Gazebo Server
     │
     ├── Robot
     ├── Sensors
     └── Plugins
```

CI에서 사용할 수 있어야 한다.

---

## 11.11 Automated Testing

예제 테스트 흐름:

```text
Start Gazebo Headless
        │
        ▼
Spawn tutorial_bot
        │
        ▼
Publish /cmd_vel
        │
        ▼
Observe odometry
        │
        ▼
Assert expected movement
        │
        ▼
PASS / FAIL
```

테스트 코드는 다음 위치를 우선한다.

```text
examples/ros2_ws/src/tutorial_bot_tests/
```

---

## 11.12 GitHub Actions CI

CI 목표:

```text
Push / Pull Request
        │
        ▼
Build ROS 2 workspace
        │
        ▼
Run static checks
        │
        ▼
Start headless Gazebo
        │
        ▼
Run simulation test
        │
        ▼
PASS / FAIL
```

문서 CI와 코드 CI를 분리할 수 있다.

예:

```text
.github/workflows/
├── pages.yml
└── test.yml
```

---

## 11.13 Gazebo Classic → Harmonic Migration

부록 성격으로 작성한다.

다룰 내용:

- Gazebo Classic과 Gazebo Harmonic의 개념 차이
- `gazebo_ros_pkgs` 중심 구조와 `ros_gz` 중심 구조 비교
- Classic plugin과 Gazebo System 차이
- 자주 등장하는 명령어 / 패키지 이름 변화
- 기존 프로젝트 migration 시 체크리스트

이 장을 프로젝트의 핵심 시작점으로 사용하지 않는다.

---

## 11.14 고급 프로젝트

### Project 3 — Production-style Simulation Stack

최종 목표:

```text
tutorial_bot
├── Custom Gazebo System Plugin
├── ros2_control
├── Sensors
├── ros_gz
├── Headless Simulation
├── Automated Tests
└── GitHub Actions CI
```

완료 조건:

- Custom System Plugin이 실제 simulation에서 동작한다.
- headless simulation을 실행할 수 있다.
- 최소 하나의 simulation integration test가 존재한다.
- GitHub Actions에서 build와 test가 자동 실행된다.

---

# 12. `tutorial_bot` 설계 원칙

각 장마다 새로운 로봇을 만들지 않는다.

가능한 한 동일한 `tutorial_bot`을 계속 발전시킨다.

## 초급 상태

```text
tutorial_bot
├── base_link
├── left_wheel
├── right_wheel
├── lidar
├── camera
└── imu
```

## 중급 상태

추가:

```text
tutorial_bot
├── ros2_control
├── TF
├── controller config
├── bridge config
└── Nav2 integration
```

## 고급 상태

추가:

```text
tutorial_bot
├── custom system plugin
├── automated tests
└── CI support
```

기능이 누적될수록 예제가 지나치게 복잡해질 경우 chapter별 snapshot을 둘 수 있다.

예:

```text
examples/snapshots/
├── beginner-final/
├── intermediate-final/
└── advanced-final/
```

단, 기본적으로는 중복 코드를 만들지 않는 방향을 우선한다.

---

# 13. ROS 2 패키지 역할

## `tutorial_bot_description`

담당:

- URDF / Xacro
- Mesh
- RViz config
- robot model resource

권장 구조:

```text
tutorial_bot_description/
├── CMakeLists.txt
├── package.xml
├── urdf/
├── meshes/
└── rviz/
```

---

## `tutorial_bot_gazebo`

담당:

- Gazebo world
- Gazebo model
- Gazebo-specific configuration
- spawn 관련 리소스

권장 구조:

```text
tutorial_bot_gazebo/
├── CMakeLists.txt
├── package.xml
├── worlds/
├── models/
└── config/
```

---

## `tutorial_bot_bringup`

담당:

- ROS 2 Launch
- bridge config
- 전체 simulation orchestration

권장 구조:

```text
tutorial_bot_bringup/
├── CMakeLists.txt
├── package.xml
├── launch/
└── config/
```

---

## `tutorial_bot_control`

담당:

- ros2_control
- controller YAML
- control 관련 launch / config

---

## `tutorial_bot_plugins`

담당:

- Advanced level C++ Gazebo plugins
- custom transport examples

---

## `tutorial_bot_tests`

담당:

- launch test
- integration test
- simulation behavior test

---

# 14. Markdown 작성 규칙

## 14.1 언어

설명 문장은 가능한 한 한국어로 작성한다.

영문이 더 정확하거나 널리 사용되는 기술 용어는 다음 형태를 선호한다.

```text
엔티티(Entity)
컴포넌트(Component)
시스템(System)
실시간 계수(Real Time Factor)
```

처음 등장할 때만 한국어와 영어를 함께 쓰고, 이후에는 문맥에 따라 자연스러운 표현을 사용한다.

ROS 2 package, topic, service, CLI, API 이름을 억지로 번역하지 않는다.

예:

```text
ros_gz_bridge
/cmd_vel
gz topic
EntityComponentManager
```

---

## 14.2 파일명

문서 파일명은 영문 소문자 kebab-case를 사용한다.

```text
ros-gz-bridge.md
headless-simulation.md
gz-ros2-control.md
```

ROS 2 package 이름은 snake_case를 사용한다.

```text
tutorial_bot_bringup
tutorial_bot_description
```

---

## 14.3 각 튜토리얼의 권장 형식

가능하면 모든 장을 다음 구조로 작성한다.

````markdown
# 제목

> **난이도:** ...
> **Gazebo:** Harmonic
> **ROS 2:** Jazzy
> **선행 학습:** ...

## 학습 목표

이 장을 마치면 다음을 할 수 있다.

- ...
- ...

## 배경 지식

...

## 실습

### 1. ...

...

## 실행

```bash
...
```

## 결과 확인

...

## 동작 원리

...

## 자주 발생하는 문제

...

## 정리

...

## 다음 단계

...
````

---

# 15. 코드 작성 규칙

1. 튜토리얼의 모든 핵심 코드는 실제 파일로 저장한다.
2. Markdown에만 존재하고 repository에는 없는 긴 코드를 만들지 않는다.
3. Markdown에는 설명에 필요한 핵심 부분만 인용하고 전체 파일 경로를 함께 안내한다.
4. 모든 명령은 가능한 한 그대로 복사해서 실행할 수 있어야 한다.
5. 코드 예제는 불필요한 추상화를 피한다.
6. 초급에서는 이해하기 쉬운 최소 구현을 우선한다.
7. 중급부터 실제 package 구조를 사용한다.
8. 고급 코드에는 필요한 경우 주석을 추가하되 과도한 주석은 피한다.
9. `tutorial_bot`의 robot description은 URDF / Xacro를 우선하며 별도의 SDF 로봇 원본을 중복 관리하지 않는다.
10. 실행하지 않은 코드를 정상 동작한다고 단정하지 않는다.

---

# 16. 이미지 및 미디어 규칙

모든 Markdown용 미디어는 다음 아래에 둔다.

```text
docs/images/
```

권장 구조:

```text
docs/images/
├── getting-started/
├── beginner/
├── intermediate/
├── advanced/
└── shared/
```

파일명은 내용을 알 수 있도록 작성한다.

좋은 예:

```text
beginner/diff-drive-topic-flow.svg
intermediate/tf-tree-tutorial-bot.svg
advanced/gazebo-ecs-overview.svg
```

피해야 할 예:

```text
image1.png
screen2.png
test.png
```

스크린샷보다 SVG나 다이어그램이 더 명확한 개념은 가능하면 직접 만든 SVG를 사용한다.

이미지에 들어가는 설명 텍스트도 가능한 한 한국어로 작성한다.

---

# 17. 문서와 코드 연결 규칙

각 실습 문서에서는 해당 예제 파일의 repository 경로를 명확하게 표시한다.

예:

```markdown
이번 장에서 사용하는 world 파일:

`examples/gazebo/worlds/first_world.sdf`
```

중급 이후 ROS 2 예제:

```markdown
Launch 파일:

`examples/ros2_ws/src/tutorial_bot_bringup/launch/simulation.launch.py`
```

문서와 예제 코드의 경로가 어긋나지 않도록 CI 또는 검사 스크립트를 추가하는 것을 권장한다.

---

# 18. MkDocs 구성 방향

`mkdocs.yml`은 다음 역할을 담당한다.

- 사이트 제목
- 한국어 UI
- Material theme
- navigation
- code highlighting
- admonition
- tabs
- 필요한 경우 Mermaid 지원

초기 navigation 개념:

```yaml
site_name: gazebo-sim-tutorial-kr

nav:
  - 홈: index.md
  - 시작하기:
      - Gazebo Harmonic: getting-started/gazebo-harmonic.md
      - Jazzy 설치: getting-started/installation-jazzy.md

  - 초급:
      - 개요: beginner/index.md
      - Gazebo 개요: beginner/01-gazebo-overview.md
      - GUI 기초: beginner/02-gui-basics.md
      - SDF 기초: beginner/03-sdf-basics.md

  - 중급:
      - 개요: intermediate/index.md

  - 고급:
      - 개요: advanced/index.md

  - 참고:
      - 호환성: compatibility.md
      - 명령어: reference/commands.md
      - 용어: reference/terminology.md
```

초기 작업에서 모든 빈 문서를 navigation에 억지로 넣을 필요는 없다.

실제 콘텐츠가 생성될 때 단계적으로 추가할 수 있다.

---

# 19. CI 정책

## 문서 CI

최소 목표:

- MkDocs build 성공 여부 검사
- 깨진 내부 링크 검사
- 잘못된 이미지 경로 검사

## 코드 CI

최소 목표:

- ROS 2 workspace build
- package dependency 검사
- 가능한 범위의 unit / integration test

고급 단계:

- Headless Gazebo 실행
- `tutorial_bot` spawn
- `/cmd_vel` 입력
- Odometry 또는 pose 변화 검증

---

# 20. 초기 구현 우선순위

Codex는 처음부터 모든 튜토리얼 내용을 생성하려 하지 않는다.

다음 순서로 repository 기반을 먼저 만든다.

## Phase 1 — Repository Skeleton

생성:

```text
README.md
Handoff.md
LICENSE
CONTRIBUTING.md
mkdocs.yml
requirements-docs.txt
docs/
examples/
scripts/
.github/workflows/
```

목표:

- `mkdocs serve` 실행 가능
- 기본 홈 페이지 표시
- GitHub Pages workflow 준비

---

## Phase 2 — Getting Started

우선 작성:

```text
docs/index.md
docs/compatibility.md
docs/getting-started/gazebo-harmonic.md
docs/getting-started/installation-jazzy.md
docs/getting-started/troubleshooting.md
```

---

## Phase 3 — Beginner

초급 튜토리얼과 순수 SDF 예제를 먼저 완성한다.

최종 결과:

```text
tutorial_bot
├── wheels
├── DiffDrive
├── LiDAR
├── Camera
└── IMU
```

ROS 2 bridge까지 정상 동작하도록 한다.

---

## Phase 4 — Intermediate

ROS 2 workspace 구조를 본격적으로 완성한다.

목표:

```bash
ros2 launch tutorial_bot_bringup simulation.launch.py
```

한 줄로 전체 simulation을 실행한다.

---

## Phase 5 — Advanced

다음을 추가한다.

- C++ System Plugin
- Gazebo Transport
- Headless simulation
- Integration test
- GitHub Actions CI

---

## Future work — 본편 완료 이후

Phase 1부터 Phase 5까지의 Jazzy + Harmonic 튜토리얼이 모두 완료된 이후에만 다음 작업을 시작한다.

- Ubuntu 22.04 LTS + ROS 2 Humble + Gazebo Fortress 별도 튜토리얼
- 공개 wheeled / legged / humanoid URDF / Xacro와 world를 위한 Asset Bank
- Open-RMF 기반 multi-floor 및 multi-robot 예제

Future work는 본편의 완료 조건에 포함하지 않는다.

---

# 21. 초기 Codex 작업 요청

새 repository에서 이 문서를 전달받은 Codex는 우선 다음 작업을 수행한다.

1. 이 문서의 구조에 맞추어 repository skeleton을 생성한다.
2. MkDocs + Material for MkDocs 환경을 구성한다.
3. `docs/index.md`를 작성한다.
4. `docs/compatibility.md` 기본 문서를 작성한다.
5. 초급 / 중급 / 고급 각각의 `index.md`를 생성한다.
6. `docs/images/`의 카테고리 디렉터리를 생성한다.
7. `examples/gazebo/`와 `examples/ros2_ws/src/` 구조를 생성한다.
8. 각 ROS 2 package 디렉터리는 실제 구현을 시작하기 전 최소 README 또는 placeholder만 두되, 빌드 대상 package로 만들 필요가 없으면 빈 `package.xml`을 임의 생성하지 않는다.
9. `mkdocs.yml`에 현재 존재하는 문서만 navigation으로 연결한다.
10. GitHub Pages용 `.github/workflows/pages.yml`을 구성한다.
11. repository root의 `README.md`에서 웹 튜토리얼과 코드 예제의 목적을 설명한다.
12. 이후 초급 콘텐츠부터 순서대로 구현한다.

---

# 22. Codex 작업 시 금지 사항

다음 행동은 피한다.

- Jazzy + Harmonic 본편이 끝나기 전에 Humble / Fortress 문서나 Asset Bank를 구현
- 설명용 이미지를 `docs/images/` 밖에 무분별하게 저장
- 실행 확인이 되지 않은 명령을 검증된 것처럼 작성
- Gazebo Classic 명령과 Gazebo Harmonic 명령을 혼용
- `ign gazebo`, `gazebo`, `gz sim` 등의 세대별 명령을 설명 없이 섞어서 사용
- ROS 1 예제를 ROS 2 문서에 포함
- 초급 단계부터 불필요한 C++ plugin 구현을 요구
- chapter별로 서로 다른 robot model을 무분별하게 생성
- 빌드 결과물 `site/`, `build/`, `install/`, `log/`를 Git에 포함
- 대용량 영상 파일을 저장소에 무분별하게 commit
- 문서에 사용되지 않는 placeholder 이미지 대량 생성
- MkDocs navigation에 아직 존재하지 않는 파일을 등록하여 build를 깨뜨림

---

# 23. `.gitignore` 기본 대상

최소한 다음 항목은 제외한다.

```gitignore
# MkDocs
site/

# ROS 2 / colcon
build/
install/
log/

# Python
__pycache__/
*.pyc
.venv/

# IDE
.vscode/
.idea/

# OS
.DS_Store
```

`.vscode/` 설정을 프로젝트에서 의도적으로 공유하려면 해당 항목은 추후 조정할 수 있다.

---

# 24. 완료 기준

이 프로젝트의 초기 기반 작업은 다음 조건을 만족하면 완료된 것으로 본다.

## Repository

- [ ] 권장 디렉터리 구조가 생성되어 있다.
- [ ] `README.md`가 존재한다.
- [ ] `Handoff.md`가 존재한다.
- [ ] `.gitignore`가 존재한다.
- [ ] `CONTRIBUTING.md`가 존재한다.

## Documentation

- [ ] `mkdocs.yml`이 존재한다.
- [ ] `mkdocs build`가 성공한다.
- [ ] 한국어 홈 페이지가 표시된다.
- [ ] 초급 / 중급 / 고급 navigation 구조가 존재한다.
- [ ] Jazzy + Harmonic 및 amd64 + NVIDIA 지원 정책이 문서화되어 있다.
- [ ] 모든 로컬 미디어는 `docs/images/` 아래에 있다.

## GitHub Pages

- [ ] GitHub Actions에서 문서 build가 가능하다.
- [ ] Pages 배포 workflow가 존재한다.
- [ ] `site/` 빌드 결과물을 Git에서 직접 관리하지 않는다.

## Examples

- [ ] `examples/gazebo/` 구조가 존재한다.
- [ ] `examples/ros2_ws/src/` 구조가 존재한다.
- [ ] `tutorial_bot`을 공통 예제로 사용하는 방향이 유지된다.

## Quality

- [ ] 설명은 가능한 한 한국어다.
- [ ] 코드와 명령어는 복사하여 사용할 수 있는 형태다.
- [ ] Gazebo Classic과 Gazebo Harmonic의 내용이 명확히 구분된다.
- [ ] `tutorial_bot`의 robot description은 URDF / Xacro를 우선한다.

---

# 25. 최종 방향 요약

이 프로젝트는 단순히 Gazebo 명령어를 나열하는 문서가 아니다.

최종적으로 다음 학습 흐름을 제공해야 한다.

```text
처음 Gazebo를 접함
        │
        ▼
SDF World / URDF·Xacro Robot 작성
        │
        ▼
Sensor와 DiffDrive 사용
        │
        ▼
ROS 2와 Gazebo 연결
        │
        ▼
ROS 2 Launch / TF / ros2_control
        │
        ▼
Nav2 기반 Robot Simulation
        │
        ▼
Gazebo System Plugin 개발
        │
        ▼
Headless Simulation / Test / CI
```

Repository 자체가 튜토리얼의 원본이면서 실행 가능한 예제 코드 저장소가 되고, GitHub Pages는 `docs/`를 사람이 읽기 좋은 웹사이트 형태로 제공한다.

핵심 원칙은 다음 네 가지다.

1. **한국어 중심**
2. **실행 가능한 예제**
3. **Jazzy + Harmonic 단일 기준과 URDF / Xacro 우선**
4. **초급부터 고급까지 하나의 `tutorial_bot`을 점진적으로 발전**

이 원칙을 유지하면서 작은 단위로 구현하고, 각 단계가 실제로 빌드 및 실행되는 상태를 유지한다.
