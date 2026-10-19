# Architecture

- apps/web: Next.js frontend
- apps/game-server: Socket.IO multiplayer server
- packages/shared: shared types and schemas
- packages/game-engine: deterministic game rules
- PostgreSQL: planned persistence

The server is authoritative for multiplayer matches.