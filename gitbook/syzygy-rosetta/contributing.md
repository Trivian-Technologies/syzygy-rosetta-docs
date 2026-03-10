# Contributing

Thank you for your interest in contributing to Syzygy Rosetta and Trivian Technologies.

Rosetta is in active MVP development. We welcome contributions from engineers, researchers, and builders who care about making AI governance infrastructure better.

---

## Ways to Contribute

### Report Issues
If you find a bug, unexpected behavior, or a gap in the documentation:

1. Check existing issues on [GitHub](https://github.com/Trivian-Technologies/syzygy-rosetta-originbase/issues) to see if it has already been reported
2. Open a new issue with a clear title, description, steps to reproduce, and expected vs actual behavior

### Suggest Improvements
Have an idea for a new feature, policy rule, or architectural improvement? Open a GitHub issue tagged `enhancement` with your proposal. Describe the problem it solves and your suggested approach.

### Submit a Pull Request
For code contributions:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Make your changes
4. Write or update tests as appropriate
5. Ensure all existing tests pass
6. Submit a pull request with a clear description of what you changed and why

### Improve Documentation
Documentation contributions are always welcome. If something is unclear, incorrect, or missing — open a PR directly against the `syzygy-rosetta-docs` repository.

---

## Contribution Guidelines

### Scope
The core Rosetta evaluation logic (`reflex.py`, policy engine, risk scoring) is under active development. Before making changes to core logic, open an issue first to discuss the approach.

Do not:
- Rewrite core Rosetta logic without prior discussion
- Introduce new architecture without approval
- Change the `/evaluate` API contract without opening a proposal issue first

### Code Style
- Python 3.10+
- Follow PEP8 conventions
- Document all functions with docstrings
- Keep functions focused — single responsibility

### Commit Messages
Use clear, descriptive commit messages:
```
feat: add confidence decay threshold configuration
fix: correct risk score calculation for authority tags
docs: update deployment guide with production notes
```

### Testing
All contributions to the evaluation pipeline must include test coverage. Document your test cases and expected outputs.

---

## Development Setup

```bash
# Clone the repo
git clone https://github.com/Trivian-Technologies/syzygy-rosetta-originbase.git
cd syzygy-rosetta-originbase

# Install dependencies
pip install -r requirements.txt

# Run the API locally
uvicorn app:app --host 0.0.0.0 --port 8000 --reload

# Run tests
python -m pytest
```

---

## Repository Map

| Repository | Purpose |
|---|---|
| [syzygy-rosetta-originbase](https://github.com/Trivian-Technologies/syzygy-rosetta-originbase) | Core codebase — reflex engine, API, policy logic |
| [syzygy-rosetta-sandbox](https://github.com/Trivian-Technologies/syzygy-rosetta-sandbox) | Multi-agent testing and simulation environment |
| [syzygy-rosetta-sdk](https://github.com/Trivian-Technologies/syzygy-rosetta-sdk) | SDK development (Python, JavaScript — Phase 4) |
| [syzygy-rosetta-docs](https://github.com/Trivian-Technologies/syzygy-rosetta-docs) | This documentation |
| [Trivian-Infrastructure](https://github.com/Trivian-Technologies/Trivian-Infrastructure) | Future infrastructure builds (Lattice Engine, Gaian Interface) |

---

## Code of Conduct

We maintain a professional, respectful environment. Contributions are reviewed on technical merit. Disrespectful or harmful behavior will result in removal from the project.

---

## Contact

For questions about contributing or to discuss a larger proposal before opening a PR:

- **GitHub Issues:** [github.com/Trivian-Technologies](https://github.com/Trivian-Technologies)
- **Email:** se@trivianinstitute.org

---

*Trivian Technologies — Building governance infrastructure for AI systems.*
