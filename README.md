# ColdFusion + WebLogic + Oracle XE Compose

This compose brings up:
- Oracle XE (gvenzl/oracle-xe)
- ColdFusion (adobe/coldfusion:2021) — pull/build may require Adobe licensing
- WebLogic (store/oracle/weblogic) — Oracle images may require acceptance/login

Quick start

1. (Optional) Copy Oracle JDBC driver for ColdFusion to `docker/coldfusion/jdbc`:

```bash
mkdir -p docker/coldfusion/jdbc
# place ojdbc8.jar into docker/coldfusion/jdbc
```

2. Start services

```bash
docker compose -f docker/docker-compose.yml up -d
```

3. Access services

- ColdFusion admin (default): http://localhost:8500/
- WebLogic admin console: http://localhost:7001/console
- Oracle listener: localhost:1521 (service XE)

Notes

- The `adobecoldfusion/coldfusion:2021` and `store/oracle/weblogic:12.2.1.4` images may not be publicly pullable without agreeing to vendor terms. If you cannot pull them, obtain/build the images per vendor instructions and update the `image:` fields or provide local `build:` contexts.
- ColdFusion connecting to Oracle requires the Oracle JDBC driver (e.g. `ojdbc8.jar`) placed in the mounted `docker/coldfusion/jdbc` folder so ColdFusion can load it on startup.
- Adjust admin passwords and environment variables for production use.

Troubleshooting

- If Oracle takes time to initialize, wait until the DB is ready before ColdFusion/WebLogic attempts DB connections.
- Check logs:

```bash
docker compose -f docker/docker-compose.yml logs -f oraclexe
docker compose -f docker/docker-compose.yml logs -f coldfusion
docker compose -f docker/docker-compose.yml logs -f weblogic
```
