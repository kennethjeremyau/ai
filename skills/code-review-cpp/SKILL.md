---
name: code-review-cpp
description: Review C++/Qt code with the built-in code-review skill plus project-specific C++ checks. Use for /code-review-cpp or when reviewing C++ changes.
---

# Code Review (C++)

Run the `code-review` skill, passing through any arguments. Also report these as findings:

- **Qt `foreach`/`Q_FOREACH`:** Replace with a C++ range-based `for` loop. Wrap Qt containers in `std::as_const()` to avoid a detach.
