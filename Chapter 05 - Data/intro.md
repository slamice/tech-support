h2. Data

h3. corruption

h4. Causes:

- Power outages or other power-related problems.
- Out of sync services (e.g. postgres replication issue, etc.)
- Bad programming (e.g. a bug, caching issues)

h4. The Legal ramifications:

- Entire system shutdown => money loss
- 

h4. Analyzing Data corruption:

- Logs
- Saved queries

h4. Preventing data corruption:

- Backups
- Tests
- Data requests
- Giving access to others