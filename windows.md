# Table of Contents

- [Process](#process)
  - [Listing ports are running](#listing-ports-are-running)
  - [Kill](#kill)

# Process

## Listing ports are running

get `PID` from:

```bash
netstat -ano | findstr TCP | findstr LISTENING
```

## Kill

```bash
taskkill /pid ${PID} /f
```

---
