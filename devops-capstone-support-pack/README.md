# DevOps Capstone Support Pack

This is a **supplementary pack** for IBM's Customer Accounts DevOps Capstone. Start from the official IBM template using GitHub's **Use this template** button; do not use this pack as a replacement for the starter repository.

Official template: <https://github.com/ibm-developer-skills-network/aolwx-devops-capstone-template>

## Apply these files

1. Copy `.github/workflows/ci-build.yaml` into the matching path in your template repository.
2. Compare/apply `setup.cfg` at the repository root. It configures nose, coverage, Flake8 and Pylint as required by the assignment.
3. Add `user-story.md` at the repository root.
4. Use `README-badge-snippet.md` to update your own README **after** you have a successful GitHub Actions run. Replace `OWNER` and `REPOSITORY` with your actual values.
5. Review `SECURITY-CORS-INTEGRATION.md` before changing `service/__init__.py` and `requirements.txt`.
6. Add `Dockerfile` at the repository root when you reach the containerization task.
7. Use `SUBMISSION-FILE-MAP.md` and `EVIDENCE-GENERATION.md` to save outputs under the exact filenames requested by Coursera.

## What this pack does not include

The screenshots and terminal outputs in the assignment must be captured from your actual GitHub, Kanban board, running Accounts API, Docker/Kubernetes environment and Tekton run. This pack intentionally does not fabricate those items.

## Before using the workflow

The GitHub Actions workflow expects the starter repository's `service/`, `tests/`, `requirements.txt`, and Postgres-backed test setup. It uses Python 3.9 to match the official template. Run the workflow in your repository and fix any project-specific lint/test failures it reports.
