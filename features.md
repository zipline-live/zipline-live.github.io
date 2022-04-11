---
title: zipline-live
description: On premise live trading with zipline
---
zipline-live currently supports the Interactive Brokers (IB) API only. With IB you can:
 - Access your IB portfolio via `context.portfolio`
 - See the active positions
 - Create new orders for equities
 - Access real-time data through `data.current`

## Limitations
zipline-live is a relatively new project and it is still in the alpha stage.
The following features are planned, but not yet implemented:
 - Order guards
 - Pipeline API support
 - Fundamentals data support
 - Data capture (continuous ingestion)
