---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Testing Tuners Using Files

If you need to test with a system that you that you don't have access to, for example, testing ATSC functionality on a DVB system, you can use a TS recording to emulate the tuner type.

```
./tvheadend --tsfile_tuners 1 --tsfile test.ts
```

The TS file should contain the whole mux and not just one service.

A new 'network' will be created for the file as well as a number of 'mux', 'service' and 'channel' objects matching the services found within the TS file.

The contents of the TS file will be played on a continuous loop.
