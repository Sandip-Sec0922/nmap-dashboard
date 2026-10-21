# Nmap Dashboard

This project is a lightweight security dashboard for reviewing Nmap scan results. It includes a secure-style login flow and a dashboard that summarizes hosts, ports, and scan health in a single interface.

## Project status

This repository was initially a minimal login demo but had structural, dependency, and architectural issues. The current work converts it into a usable MVP dashboard with:

- React frontend for the login screen and dashboard UI
- Express API for authentication, Nmap imports, live scans, and persistent history
- JSON report export for selected scan snapshots
- Basic project documentation and plan
- Architecture aligned with a real dashboard workflow

## Architecture overview

- Frontend: React + React Router
- Backend: Express.js API
- Data flow: login -> auth API -> dashboard summary -> chart/table UI
- Current scope: local demo data and secure-by-default login flow design

## Directory structure

```text
.
├── README.md
├── docs/
│   ├── ARCHITECTURE.md
│   └── PROJECT-PLAN.md
├── package.json
├── src/
│   ├── backend/
│   │   └── server.js
│   └── frontend/
│       ├── package.json
│       ├── public/
│       └── src/
│           ├── App.js
│           ├── components/
│           │   ├── Dashboard.js
│           │   └── Login.js
│           └── index.js
└── webchat.py
```

## Quick start

1. Install root dependencies:
   ```bash
   npm install
   ```

2. Start the backend:
   ```bash
   npm start
   ```

3. In another terminal, start the frontend:
   ```bash
   npm --prefix src/frontend start
   ```

4. Open the app at `http://localhost:3000` and log in with:
   - Username: `admin`
   - Password: `admin123`

## Scripts

### Root project

```bash
npm start         # runs the Express backend
npm run frontend  # runs the frontend from src/frontend
npm run dev       # runs backend + frontend together
```

### Frontend

```bash
npm --prefix src/frontend start
npm --prefix src/frontend build
```

## Notes

- The initial app included broken file placement, missing router dependency, and mismatched API ports.
- This MVP is intentionally focused on a clean foundations-first implementation rather than full scanner automation.
- The dashboard now supports importing a real Nmap XML file and converting it into a summary table + alert list.
- Live scans can be run against a target, and each result is saved to a local scan history store with JSON export support.
- Live scans use Nmap service/version detection and return reported port state, service, product, and version data when Nmap can identify them. Hostname scans include every resolved address.
- Host filtering, sorting, and service hotspot summaries provide a more realistic multi-host view.
- Recent scan trend cards help compare host and port exposure across the latest scan history.
- Scan notes can be attached to selected results and saved with the local history store.
- Exposure labels are a port-based triage heuristic, not vulnerability findings. No sample hosts or scan findings are shown when there is no real scan data.
- Only scan hosts and networks you own or are authorized to assess. Nmap service probes may not identify virtual-hosted HTTPS applications without their expected SNI/Host context.
- Future enhancements can include richer charts, saved report metadata, and production-ready authentication.
