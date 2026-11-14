# Environment Setup Notes

These notes record the environment used for the LunarLander experiments on Windows.

## Recorded local setup

- Operating system: Windows
- Python: 3.10.11 in virtual environment `.venv310`
- Virtual environment directory: `.venv310`
- SWIG: 4.3.1
- NumPy: 1.26.4
- pygame: 2.1.3
- box2d-py: 2.3.5
- Gym: 0.26.2 (editable installation was used for compatibility tests)
- Gymnasium with Box2D extra
- Stable-Baselines3 installed

Visual Studio C++ Build Tools and the C++ workload were installed to support native extension compilation. The Box2D Python package built successfully and imports for `gym`, `Box2D`, `pygame`, and `numpy` were verified.

## Recommended clean setup

Create and activate a Python 3.10 virtual environment:

```powershell
py -3.10 -m venv .venv310
.\.venv310\Scripts\Activate.ps1
python -m pip install --upgrade pip
```

Install the runtime packages:

```powershell
python -m pip install -r requirements.txt
```

Verify the key imports and environment:

```powershell
python -c "import gymnasium, stable_baselines3, numpy; print('Imports OK')"
python -c "import gymnasium as gym; env=gym.make('LunarLander-v3'); print(env.observation_space, env.action_space); env.close()"
```

## Important versioning note

The historical setup notes do not contain a complete `pip freeze` output. Therefore, this document is not a complete lockfile and cannot guarantee bit-for-bit reproduction. Generate and commit the actual environment snapshot from the experiment machine:

```powershell
python -m pip freeze > requirements-lock.txt
python --version
```

Also record OS version, CPU, compiler toolchain, Gymnasium version, Stable-Baselines3 version, and the exact source commit used for each run.
