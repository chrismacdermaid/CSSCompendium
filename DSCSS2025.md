```markdown
# Data Science Coding and Software Development Standards (2025)  

## Core Programming Standards  

### Python (PEP 8 Compliance)  
Adopt **PEP 8** for all Python code[3][5]:  
- Use `snake_case` for variables/functions (`calculate_rmse`)  
- Enforce 88-character line limits via **Black** formatter[3]  
- Require Google-style docstrings for API documentation:  

```
def preprocess_data(df: pd.DataFrame) -> pd.DataFrame:  
    """Clean raw dataset by removing nulls and outliers.  

    Args:  
        df: Input DataFrame with raw data  

    Returns:  
        Processed DataFrame with valid records  
    """  
    return df.dropna()  
```

### R (tidyverse Conventions)  
- Follow **tidyverse** style guidelines for readability[2][8]:  
  ```
  calculate_bmi <- function(weight, height) {  
    # Use snake_case for function names  
    bmi <- weight / (height^2)  
    return(bmi %>% round(1))  # Prefer pipes  
  }  
  ```  

---

## Project Structure  

Adopt the **cookiecutter-data-science** template[3]:  
```
project-root/  
├── data/               # Versioned via DVC  
├── models/             # Serialized model binaries  
├── notebooks/          # Exploratory analysis  
├── src/                # Production-ready code  
└── tests/              # pytest/unit tests  
```  

*Best Practices*[3][6]:  
1. Store raw data as immutable artifacts  
2. Separate experimental notebooks from production code  
3. Use `environment.yml` for Conda dependencies  

---

## Version Control Strategy  

| Practice              | Implementation                          | Tools                          |  
|-----------------------|-----------------------------------------|--------------------------------|  
| **Branch Management** | Git Flow with short-lived feature branches | GitHub/GitLab[1][7]           |  
| **Commit Messages**   | Conventional Commits (`feat:`, `fix:`)  | pre-commit hooks[4][5]        |  
| **Data Versioning**   | DVC-tracked datasets/models             | DVC[3]                        |  

*Example CI Pipeline*[1][5]:  
```
# .github/workflows/ci.yml  
jobs:  
  test:  
    steps:  
      - run: pytest --cov=src/  
      - uses: codecov/codecov-action@v3  
```  

---

## Testing and Validation  

1. **Unit Tests**: >80% coverage for critical paths[3][6]  
2. **Data Checks**: Schema validation via `pandera`:  
   ```
   schema = DataFrameSchema({"age": Column(int, Check.ge(0))})  
   schema.validate(df)  
   ```  
3. **Model Monitoring**: Track drift with **Evidently AI**[3]  

---

## Documentation Standards  

| Document Type         | Requirements                            | Tools                          |  
|-----------------------|-----------------------------------------|--------------------------------|  
| Project README        | Installation, usage examples            | GitHub-flavored MD[1][8]      |  
| Model Cards           | Ethics statements, performance metrics | MLflow[3]                     |  
| API Documentation     | Auto-generated from docstrings          | Sphinx (Python)[3], roxygen2 (R)[2] |  

---

## Security Practices  

1. **NIST SSDF Compliance**[7]:  
   - Conduct threat modeling for ML pipelines  
   - Scan dependencies weekly via `safety check` (Python)[3]  
2. **Secret Management**:  
   ```
   # BAD: Hardcoded credentials  
   API_KEY = "sk-12345"  

   # GOOD: Environment variables  
   import os  
   api_key = os.getenv("OPENAI_KEY")  
   ```  

---

## Collaboration Workflow  

1. **Pull Request Requirements**[1][6]:  
   - Small changes (<400 LOC)  
   - Passing CI checks  
   - Linked JIRA ticket in description  
2. **Code Review Focus Areas**:  
   - Security vulnerabilities  
   - Performance bottlenecks  
   - Documentation completeness  

---

## Recommended Toolchain  

| Category              | Tools                                  |  
|-----------------------|----------------------------------------|  
| Version Control       | Git + DVC[3]                          |  
| CI/CD                 | GitHub Actions[1]                     |  
| Documentation         | MkDocs + Material Theme[3]            |  
| Experiment Tracking   | MLflow[3]                             |  

---

## References  
[1] GitHub Docs (2022)  
[2] R Markdown Templates (2017)  
[3] Cookiecutter Data Science (2015)  
[4] Markdown Table Guide (2024)  
[5] Markdown Cheatsheet (2022)  
[6] Coding Standards (2023)  
[7] Open Knowledge Foundation (2015)  
[8] Markdown Syntax Guide (2021)  
```

**Instructions for Use:**  
1. Copy this markdown into a `.md` file (e.g., `CODING_STANDARDS.md`).  
2. Replace bracketed citations (e.g., ``) with actual references from your organization.  
3. Customize code examples and tool recommendations to match your team's stack.

Sources
