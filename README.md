# Filtering flows timeout test

This repository is a scanner stress fixture for the `filteringFlowsTimeout` use case.

`src/stress.js` is generated code. It creates sensitive `accountPassword` sources and sends each source repeatedly to logging, HTTP, and browser-storage sink patterns. The default fixture contains 102,400 sink calls.

## Regenerate the fixture

```bash
npm run generate
```

To change the workload size:

```bash
SOURCE_COUNT=80 REPEATS_PER_SOURCE=80 npm run generate
```

Commit the regenerated `src/stress.js` before scanning through the UI. For CI, run the generator before the scanner step if a different workload size is needed.

## Validation

Run the same fixture with the baseline scanner image and the image containing the flow-filtering fix. Compare the scanner log entries for `Filtering flows 2`; the fixed image must complete that stage and finish the scan before the configured timeout.
