# Cloudflare Pages Deployment

Recommended path: GitHub integration.

1. Commit this repository to GitHub.
2. Open Cloudflare → Workers & Pages.
3. Create application → Pages.
4. Import the `armans-shopify-supportops` GitHub repository.
5. Configure:
   - Production branch: `main`
   - Framework preset: None
   - Build command: blank
   - Build output directory: `website`
6. Deploy.
7. Test the generated Pages URL on desktop and phone.
8. Add `armans.ai` after the Pages deployment works.
9. Confirm HTTPS.
