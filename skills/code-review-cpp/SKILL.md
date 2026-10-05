---
name: code-review-cpp
description: Review C++/Qt code with the built-in code-review skill plus project-specific C++ checks. Use for /code-review-cpp or when reviewing C++ changes.
---

# Code Review (C++)

Run the `code-review` skill, passing through any arguments. Also report these as findings:

- **Qt `foreach`/`Q_FOREACH`:** Replace with a C++ range-based `for` loop. Wrap Qt containers in `std::as_const()` to avoid a detach.
- **`main()` location:** Define `main()` only in a file named `main.cc`. Report a `main()` definition in any other file.
- **Top-level catch-all:** Do not wrap `main()` or a thread entry point in `catch (...)` or `catch (const std::exception&)` to swallow unhandled exceptions. Let the exception terminate the application so it writes a core file for later debugging.
- **`NULL` pointers:** Replace `NULL` and `0` used as a null pointer with `nullptr`.
- **Member variable comments:** In header files, give each member variable its own comment. Report a member variable that has no comment or shares one comment with other members.
- **Other header variable comments:** In header files, also give every variable outside a class its own comment. This includes namespace-scope, global, `extern`, `static`, `constexpr`, and `inline` variables. Report a variable that has no comment or shares one comment with other variables.
