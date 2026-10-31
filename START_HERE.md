# TrafficSense final project folder

- **Code/** — Python/backend, dashboard, Arduino firmware, tests, model files, and saved demo calibration.
- **Docx/** — Word project report(s).
- **Demo Video/** — exactly the two chosen input videos: Front and Right.
- **Presentation/** — PowerPoint presentation.
- **Diagrams/** — transparent hardware schematic and working flowchart.
- **Demo Recording/** — your existing recorded walkthrough.

## Run the project

The working installation remains in the original TrafficSense folder. This is an organized copy; its Python environment is not included or tested on a different computer. Install the dependencies in Code/.venv before launching this copy. From Code, use:

```sh
python3 run.py --port 8773 --runtime runtime/user-session
```

Only one server can use port 8773 at a time. The selected videos in Demo Video are referenced by relative paths in the copied session. Right-road carriageway calibration and the explicitly simulated ambulance scenario are included. The current demo signal recommendations are separate from physical Arduino control.

The served dashboard is Code/trafficsense/static/TrafficSense.html. Code/TrafficSense.html preserves the previously supplied standalone file. Submission document contents were not changed. Development caches, the old QA runtimes, and the machine-specific virtual environment were not copied.
