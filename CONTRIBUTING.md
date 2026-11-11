# Contributing

Issues and pull requests are welcome.

- Keep it standard library only, read only and offline.
- Add a test for every change: `python3 -m unittest discover -s tests -v`.
- Never add a field that can carry prompt text, file paths or file content.
