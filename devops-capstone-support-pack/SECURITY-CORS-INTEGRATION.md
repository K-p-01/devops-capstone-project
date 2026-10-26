# Talisman security headers and CORS integration

Apply this change to the **existing** IBM template rather than replacing `service/__init__.py` with a short snippet.

## 1. Add dependencies to `requirements.txt`

Add these runtime dependencies:

```text
Flask-Talisman
Flask-Cors
```

Then install dependencies with the environment activated:

```bash
pip install -r requirements.txt
```

## 2. Update `service/__init__.py`

Keep the template's existing application creation, config, route imports, logging and database initialization. After `app = Flask(__name__)` and `app.config.from_object(config)`, add:

```python
from flask_cors import CORS
from flask_talisman import Talisman

# CORS policy for the API. Restrict origins to your front end in production.
CORS(app)

# Preserve HTTP access in the training/local environment while enabling headers.
Talisman(app, force_https=False)
```

If Flake8/Pylint reports import order, keep imports grouped consistently with the existing file and add the narrowest necessary per-file configuration. Do not remove the model initialization or route imports.

## 3. Test after the change

Run the existing suite from the repository root:

```bash
nosetests -vv --with-spec --spec-color --with-coverage --cover-package=service
```

For the assignment's `security-headers-done` response, capture the real terminal output from this command after your tests pass. Do not paste an illustrative output as if it were a test run.
