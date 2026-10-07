# Profile repository environment

Copy [environment.example.json](environment.example.json) to `.local/environment.json` if local settings are needed. Keep actual paths and credentials ignored. This is a configuration template, with no automatic loader.

The documentation checks need Git and Python 3.10 or newer, with no additional packages:

```sh
python scripts/check-portability.py
python scripts/check-docs.py
```

Public documents use repository-relative paths or public URLs. Review staged content before publishing. The portability check scans machine paths and private local files; it is not a general secret or content-disclosure scanner.
