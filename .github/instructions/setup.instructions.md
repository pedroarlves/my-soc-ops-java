---
description: Setup and run the local Soc Ops Spring Boot workspace.
---

# Workspace Setup Instructions

## Mandatory dev checklist
- [ ] `./mvnw -q -DskipTests=false test`
- [ ] `./mvnw clean package`
- [ ] `./mvnw spring-boot:run`

## Quick start
1. `cd socops`
2. `./mvnw -v`
3. `./mvnw clean package`
4. `./mvnw spring-boot:run`
5. Open `http://127.0.0.1:8080`

## Notes
- Use the included Maven wrapper for consistency.
- Run tasks: `shell: mvn: build`, `shell: mvn: run`
- Key folders:
  - `socops/src/main/java/com/socops/`
  - `socops/src/main/resources/templates/game.html`
  - `socops/src/main/resources/static/css/app.css`
