# Final run and demonstration

1. Extract the project ZIP and open the root folder in VS Code.
2. Create/activate `.venv` and install `requirements.txt`.
3. Run `START_APPLICATION.bat` or `python -m uvicorn course_organizer.main:app --host 127.0.0.1 --port 8002 --reload`.
4. Open `http://127.0.0.1:8002/` and sign in.
5. Use the single Academic AI Assistant input to invoke all fourteen capabilities; prompt examples are in `DEMO_GUIDE.md`.
6. Expand the execution trace and JSON details after each request.
7. Run `RUN_TESTS.bat` before the demonstration.

The application does not mount the former `/labs` showcase. The fourteen capabilities are integrated behind one assistant, not exposed as separate launch controls.
