<div align="center">

# 🧪 pytest_exploration

**Short guide on pytest features, explored through small runnable snippets.**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)
![pytest-dependency](https://img.shields.io/badge/plugin-pytest--dependency-blue?style=flat-square)
![pytest-html](https://img.shields.io/badge/plugin-pytest--html-orange?style=flat-square)
![Cheat sheet](https://img.shields.io/badge/cheat%20sheet-PDF-red?style=flat-square&logo=adobeacrobatreader&logoColor=white)
![Status](https://img.shields.io/badge/status-superseded-orange?style=flat-square)

</div>

> 📦 **Superseded.** This repository is no longer updated. Its newer version, with more organised examples, lives at [KKoshy/pytest-practice](https://github.com/KKoshy/pytest-practice).

The commands and explanation for the snippets are included in the pdf file.

`pytest_cheat_sheet.pdf`

## Repository Structure

| File | What it demonstrates |
| --- | --- |
| [`test_example_func.py`](test_example_func.py) | Test functions; a function prefixed with `_` is not collected |
| [`test_example_class.py`](test_example_class.py) | Test methods inside a `Test*` class |
| [`test_fixture.py`](test_fixture.py) | Module-scoped fixtures |
| [`conftest.py`](conftest.py) | Shared session fixtures, the `--poles` command line option and the `pytest_generate_tests` hook |
| [`test_markers.py`](test_markers.py) | Custom markers (`model_3`, `model_s`) registered in `pytest.ini` |
| [`test_parametrize.py`](test_parametrize.py) | `@pytest.mark.parametrize` with multiple arguments |
| [`test_parametrize_ids.py`](test_parametrize_ids.py) | Explicit test ids with `ids=[...]` |
| [`test_parametrize_custom_ids.py`](test_parametrize_custom_ids.py) | Generating ids with a function |
| [`test_parametrize_indirect.py`](test_parametrize_indirect.py) | `indirect` parametrization through fixtures |
| [`test_generate_test_hook.py`](test_generate_test_hook.py) | Dynamic parametrization with `pytest_generate_tests` |
| [`test_dependency.py`](test_dependency.py) | Test dependencies with `pytest-dependency` |
| [`test_dependency_with_parametrize_static.py`](test_dependency_with_parametrize_static.py) | Dependencies between parametrized tests (static) |
| [`test_dependency_with_parametrize_dynamic.py`](test_dependency_with_parametrize_dynamic.py) | Dependencies between parametrized tests (generated) |
| [`pytest_cheat_sheet.pdf`](pytest_cheat_sheet.pdf) | Commands and explanations for all of the above |
| [`parametrize_example.html`](parametrize_example.html) / [`parametrize_ids.xml`](parametrize_ids.xml) | Sample HTML and JUnit XML reports |

## Getting Started

```bash
git clone https://github.com/KKoshy/pytest-exploration.git
cd pytest-exploration
pip install pytest pytest-dependency pytest-html
```

## Running the Examples

```bash
# Run one file
pytest test_parametrize.py -v

# Run a single test function / method
pytest test_example_func.py::test_roadster
pytest test_example_class.py::TestTeslaModelTag::test_roadster

# Select by name expression
pytest -k "TeslaModelTag and not roadster"

# Select by marker
pytest test_markers.py -m model_3

# Stop after the first failure
pytest -x

# Show local variables in tracebacks
pytest --showlocals

# Generate reports
pytest test_parametrize.py --html=parametrize_example.html
pytest test_parametrize_ids.py --junitxml=parametrize_ids.xml
```

## Sample Report

![sample_html_report](sample_html_report.PNG)

## Notes

- Several assertions fail on purpose (for example `test_model_s`), so that failure output and reports have something to show.
- `test_parametrize_ids.py` calls `pytest.set_trace()`, so the run pauses at the debugger prompt. Type `c` to continue.
- Some fixtures generate random values, so results can change between runs.
- On recent pytest versions (verified on 9.1.1), the two `test_dependency_with_parametrize_*` files fail at collection with `duplicate parametrization of 'variant'`, because the `pytest_generate_tests` hook in `conftest.py` also parametrizes `variant`.
