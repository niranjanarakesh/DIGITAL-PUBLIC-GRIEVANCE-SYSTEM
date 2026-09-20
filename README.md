# Digital Public Grievance Redressal System

This started from a pretty simple, everyday frustration — when you report a civic issue like a pothole, a power outage, or no water supply, there's usually no real way to know what happens to it afterward. So this project is an attempt to fix that on a small scale: a desktop app where citizens can file complaints and actually track them, and where admins have one organized place to manage everything coming in instead of scattered records.

It's built as a two-part system — one app for citizens, one for admins — both talking to the same Oracle database underneath.

**What it does?**

**For citizens:**

Register an account and log in (passwords are hashed, never stored as plain text)
File a complaint with a title, description, department, and priority
Track the status of everything they've submitted
Edit or delete a complaint if needed

**For admins:**

See every complaint across all citizens and departments in one dashboard, with priority filtering
Look up any complaint by ID and view its full details
Update a complaint's status as it gets worked on
Escalate a complaint that's been ignored too long
Delete complaints (along with any linked escalation/closure records)
Pull a department-wise report to see how each department is actually doing

Running quietly in the background:

Closing a complaint automatically flips its status to "Closed" — no one has to remember to update that manually
Escalating a complaint automatically bumps its priority to "High"
A stored procedure can auto-escalate complaints that have been sitting open past a set number of days

**Tech stack:**
Database: Oracle SQL + PL/SQL (triggers, functions, procedures, a reporting view)

App: Python, using Tkinter and CustomTkinter for the UI

DB connectivity: oracledb


**Project structure:**


├── sql/

│   ├── schema.sql            -- tables, constraints, sequences

│   ├── sample_data.sql       -- sample data (loaded via a normalization pass)

│   ├── plsql_programs.sql    -- triggers, functions, procedures

│   ├── sample_queries.sql    -- demo queries + the reporting view

│   ├── password_column.sql   -- sets demo citizen passwords

│   └── run_all.sql           -- runs all five in order

├── styles.py         -- shared config: DB connection, colors, fonts

├── citizen_app.py    -- citizen-facing app

├── admin_app.py       -- admin-facing app

└── README.md
