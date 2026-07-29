# GitHub Upload Steps

1. Create a public repository named `armans-shopify-supportops`.
2. Upload all files and folders from this package.
3. Use commit message:

```text
Day 1: Shopify Admin GraphQL connection proof
```

4. Confirm the README renders.
5. Confirm architecture and website files exist.
6. Search the repository for possible secrets.
7. Pin the repository on the GitHub profile.
8. Apply the GitHub profile line from `PROFILE_COPY.md`.

## Secret audit before commit

Search for:

```text
shpss_
shpua_
access_token
client_secret
```

The words may appear as documentation labels, but no real values may appear.
