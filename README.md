# KSOC Guard Action

This action is used to execute a set of policies against the files in a given repository. It is used in the following way:

```yaml
name: ksoc-guard

on:
  pull_request:

jobs:
  ksoc-guard:
    permissions:
      contents: read
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: KSOC Guard
        uses: ksoclabs/guard-action@main
        with:
          ksoc_account_id: <KSOC_ACCOUNT_ID>
          ksoc_access_key_id: ${{ secrets.KSOC_ACCESS_KEY_ID }}
          ksoc_secret_key: ${{ secrets.KSOC_SECRET_KEY }}
```

The `ksoc_access_key_id` and `ksoc_secret_key` are the credentials for the KSOC account that will be used to fetch the policies and should be stored as GitHub secrets. The `ksoc_account_id` is the only required workflow input and must match the KSOC account that the credentials are for.

There are numerous optional inputs that can be used to configure the action:
- `fail_on_severity`: The severity level that will cause the action to fail. If not provided, the action will never fail.
- `format`: The format of the output. If not provided, the default `ci-table` format will be used which is suitable for use in a CI environment.
- `ignored_paths`: A comma separated list of paths to ignore. If not provided, no paths will be ignored.
- `ksoc_api_url`: The URL of the KSOC API. If not provided, the default `https://api.ksoc.com` will be used.
- `paths`: A comma separated list of paths to scan. If not provided, all paths in the repository will be scanned.
- `policy_ids`: A comma separated list of policy IDs to execute. If not provided, all policies in the KSOC account will be executed.
- `policy_tags`: A comma separated list of policy tags to execute. If not provided, all policies in the KSOC account will be executed.
