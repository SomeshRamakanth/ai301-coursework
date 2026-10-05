Hi, I'd like to take this issue as a first contribution to PathReview. I've reproduced the bug locally (report below) and plan to trace through the output parser logic to understand how top-level JSON arrays should be normalized into the expected object shape.

## Reproduction Report

**Environment:** Python 3.12.4, conda 26.7.0, Ubuntu 24.04, repo at main branch (commit f89c06f)

### Steps and Observed Behavior

The bug is located in `rag/generator/output_parser.py` at lines 43-64:

1. `json.loads(raw)` at line 43 parses JSON and can return either a dict `{}` or a list `[]`
2. The result is passed to `_parse_json_output(data)` at line 44 without type checking
3. The function signature at line 52 expects `data: dict`
4. At line 64, the code calls `data.items()` which fails when `data` is a list

**To trigger the bug:**
```python
import json
from rag.generator.output_parser import parse_review_output

json_array = json.dumps([
    "First feedback item",
    "Second feedback item"
])

result = parse_review_output(json_array)  # Crashes here
```

**Actual output:**
```
AttributeError: 'list' object has no attribute 'items'
  File "rag/generator/output_parser.py", line 64, in _parse_json_output
    for key, value in data.items():
AttributeError: 'list' object has no attribute 'items'
```

**Expected:** parse_review_output handles array responses gracefully, either normalizing them into the object shape the parser expects or falling back to plaintext parsing. The test `test_json_array_fallback` (line 137 of `tests/unit/test_output_parser.py`) should pass, returning a list of FeedbackSection objects without crashing.
