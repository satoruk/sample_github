# Event

`github.event`

```yaml
name: Event Dump
on:
  pull_request_review:
  pull_request:
jobs:
  dump:
    runs-on: ubuntu-latest
    steps:
      - name: dump event
        run: |
          mkdir -p artifacts
          cat <<EOD > artifacts/event_${{ github.event_name }}_${{ github.event.action }}.json
            ${{ toJSON(github.event) }}
          EOD
        if: always()
      - uses: actions/upload-artifact@v2
        with:
          name: my-artifact
          path: artifacts/
        if: always()
```
