Workflow to run linter against create react app


```yaml
name: Linter
on: [push]
jobs:
  linter:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Cache dependencies
        uses: actions/cache@v2
        with:
          path: |
            **/node_modules
          key: ${{ runner.os }}-${{ hashFiles('**/package-lock.json') }}
          
      - name: Install packages
        run: npm ci
      
      - name: Run eslint
        run: npm run lint
```