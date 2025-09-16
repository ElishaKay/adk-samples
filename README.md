[Bol Agency Multi-Agent Flows](https://docs.google.com/document/d/1SnntqAbgNT40JbJyyh4wbwgSzuV6pq6-O7bc0So_Jqs/edit?tab=t.0)

## Running in Dev Mode

To activate virtual env on windows:

```bash
cd adk-samples/python/agents/data-science
.venv\Scripts\Activate.ps1
adk web --port 8080
```

To run adk locally with google cloud storage: 
```bash
adk web --port 8080 --artifact_service_uri="gs://bol-agent-artifacts-bucket"`
```

To run the full-stack:

In 1 terminal: 

```bash
cd frontend
npm run serve --backend=http://localhost:8080
```

In 2nd terminal:
```bash
cd backend
adk web --port 8080 --allow_origins=http://localhost:4200
```