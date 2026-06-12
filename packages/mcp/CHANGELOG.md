# @better-auth/mcp

## 1.7.0-beta.6

### Minor Changes

- [#9992](https://github.com/better-auth/better-auth/pull/9992) [`e53582c`](https://github.com/better-auth/better-auth/commit/e53582ce55a0ddbca62f52efeb3459523816f222) Thanks [@gustavovalverde](https://github.com/gustavovalverde)! - The MCP plugin moves out of `better-auth` into its own package, `@better-auth/mcp`, built on `@better-auth/oauth-provider`. Import the server plugin and its helpers from `@better-auth/mcp`, and the remote client and adapters from `@better-auth/mcp/client` and `@better-auth/mcp/client/adapters` (previously imported from `better-auth/plugins` and `better-auth/plugins/mcp/client`). The OAuth endpoints move from `/mcp/*` to `/oauth2/*`, with discovery at `/.well-known/oauth-authorization-server` and protected resource metadata at `/.well-known/oauth-protected-resource`. Discovery-based MCP clients pick up the new locations on their own.

  The route helper is renamed `requireMcpAuth` (was `withMcpAuth`), and the remote client is `createMcpResourceClient` (was `createMcpAuthClient`). `requireMcpAuth` verifies the bearer token against the published JWKS and passes the verified JWT claims to your handler.

  To migrate, install `@better-auth/mcp`, add the `jwt()` plugin (now required for token signing), and move options that were nested under `oidcConfig` to flat options on `mcp({ ... })`. The database models change: `oauthApplication` becomes `oauthClient`, with new `oauthRefreshToken` and `oauthClientAssertion` tables. Regenerate or migrate your schema with `npx auth migrate` or `npx auth generate`.

### Patch Changes

- Updated dependencies [[`b36c38f`](https://github.com/better-auth/better-auth/commit/b36c38f9842d3416689340552989449a32007819), [`73541c1`](https://github.com/better-auth/better-auth/commit/73541c119041113b1909fe244ff4b8210618b5b5), [`bf39cbf`](https://github.com/better-auth/better-auth/commit/bf39cbf13f3b934f728cde72b1e7ebdc4c85f641), [`e53582c`](https://github.com/better-auth/better-auth/commit/e53582ce55a0ddbca62f52efeb3459523816f222), [`652fa53`](https://github.com/better-auth/better-auth/commit/652fa53e4912837fe234651e7c7705fb35abe188)]:
  - better-auth@1.7.0-beta.6
  - @better-auth/oauth-provider@1.7.0-beta.6
  - @better-auth/core@1.7.0-beta.6
