### This is a summary about hosting Shopify app on Vercel
    
### This APP hosts on Vercel successfully
[Vercel URL](https://vercel.com/hugh-zhou-hhs-projects/vercel-deployment-test)
    
[Shopify partner admin](https://partners.shopify.com/2560999/apps/104047247361/overview)
    
[Shopify store example](https://admin.shopify.com/store/hugh-portfolio/apps/test-vercel-deployment-2/app)
    
    
### What we need to do when hosting Shopify app on Vercel
1. In `package.json`, update `"build": "vite build && vite build --ssr"` to `"build": "prisma generate && vite build && vite build --ssr"` and add `"postinstall": "prisma generate"`;
    
2. In `app/shopify.server.js`, update `import "@shopify/shopify-app-remix/adapters/node";` to `import "@shopify/shopify-app-remix/adapters/vercel";`;
    
3. In `prisma/schema.prisma`, update `datasource db` to
```
  datasource db {
    provider = "postgresql"
    url = env("POSTGRES_PRISMA_URL") // uses connection pooling
    directUrl = env("POSTGRES_URL_NON_POOLING") // uses a direct connection
  }
```
    
4. In `prisma/migrations/.../migration.sql`, update `"expires" DATETIME` to `"expires" TIMESTAMP(3)`;
    
5. Deploy the app on Shopify partner admin "npm run deploy" and distribute it to the store(s);
    
6. Use `npm run shopify app env show` to get `SCOPES`, `SHOPIFY_API_KEY`, and the `SHOPIFY_API_SECRET` values;
    
7. Deploy the app on Vercel, adding the following environment variables:
- *NODE_ENV = production*
- *SHOPIFY_APP_URL*
- *SCOPES*
- *SHOPIFY_API_SECRET*
- *SHOPIFY_API_KEY*
    
8. Create a Postgresql on Vercel, and connect with the project;
    
9. Redeploy the project.
    
    


These docs can help: 
    
1. https://shopify.dev/docs/apps/deployment/web
    
2. https://github.com/Shopify/shopify-app-template-remix#database-tables-dont-exist
    
3. https://www.prisma.io/docs/orm/prisma-client/deployment/serverless/deploy-to-vercel



