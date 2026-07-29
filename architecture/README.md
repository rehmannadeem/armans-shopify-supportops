# Day 1 Architecture Explanation

1. Manual Trigger starts a controlled test.
2. Token node sends the app identity securely to Shopify.
3. Shopify verifies the installed app and permissions.
4. Shopify returns a temporary token.
5. GraphQL node passes that token in `X-Shopify-Access-Token`.
6. Shopify checks the query and `read_products` scope.
7. Shopify returns permitted store and product data as JSON.

## Plain-English model

- Store = protected business server
- App = trusted service identity
- Scope = permission
- Client Secret = service-account password
- Access token = temporary security badge
- GraphQL query = precise data request
- JSON response = structured result
