# Contributing to AI Train Traffic Control Simulator

Thank you for contributing to the AI Train Traffic Control Simulator project! This repository models section throughput optimization for Indian Railways using discrete-event simulation and predictive machine learning.

## Code of Conduct
We are committed to providing a welcoming, inclusive, and harassment-free environment for all contributors. Please treat everyone with respect and empathy.

## Development Workflow
1. Fork or branch from `main`.
2. Ensure you have Python 3.10+ installed.
3. Install dependencies: `pip install -r requirements.txt`.
4. Make your changes and test locally using Streamlit.
5. Create a descriptive pull request adhering to Conventional Commits.
\n
### Python Environment Setup
We recommend using a dedicated virtual environment:
```bash
python -m venv venv
# Windows:
.\venv\Scripts\activate
# Linux/macOS:
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```
\n
## Commit Message Convention
We enforce the Conventional Commits specification:
- `feat:` A new feature or capability.
- `fix:` A bug fix in simulation, AI, or UI.
- `docs:` Documentation changes only.
- `style:` Formatting, missing semi-colons, whitespace (no code change).
- `refactor:` Code restructuring without changing external behavior.
- `test:` Adding missing tests or correcting existing tests.
- `perf:` Performance optimizations in simulation loop or models.
\n
## Code Style & Formatting
- All code must conform to PEP 8 standards.
- Use explicit type hints for function arguments and return types.
- Format code using `black` (line length 100).
- Run `flake8` to detect syntax errors and undefined names.
- Ensure all docstrings follow Google style conventions.
\n