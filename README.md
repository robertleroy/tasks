# Rewrite of tasks app ~ June 2026 ~

- A multi list tasks app
  - bcrypt password hashing
  - Sqlite / Drizzle database management
  - Sortablejs drag / persistant sort order
  - containerized & deployed to homelab

<br>

### Init:
```sh
# push to main branch
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/robertleroy/Checklist.git
git push -u origin main
```
   
<br>

---


### Deploy:

1. Commit to github
```bash
git add .
git commit -m "update"
git push
```
2. Create directory structure in homelab
```
tasks/
├── app/          (cloned repo)
├── data/         (db bind mount)
└── docker-compose.yml
```
3. Clone repo to `tasks/app/`
```bash
git clone https://github.com/robertleroy/tasks.git app
```
4. docker-compose.yml
```yaml
services:
  tasks:
    build: ./app
    ports:
      - "3002:3000"
    volumes:
      - ./data:/app/data
    environment:
      - DATABASE_URL=file:/app/data/local.db
      - ORIGIN=http://100.73.161.19:3002
    restart: unless-stopped
```
5. `docker compose up -d`

   
<br>

---

### Update:

1. edit, add, commit, push to github
```bash
git add . && git commit -m "update" && git push
```
2. Pull the repo into the `task/app/` folder: `git pull`
3. Re-build from the `tasks` folder
`docker compose up -d --build`


