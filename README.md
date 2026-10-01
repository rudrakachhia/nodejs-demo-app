# nodejs-demo-app — CI/CD with GitHub Actions

A small Express app with an automated pipeline: **test → build → push** to Docker Hub on every push to `main`.

## Project structure
```
.
├── app.js                       # Express app
├── __tests__/app.test.js        # Jest + Supertest tests
├── Dockerfile                   # Container image
├── .github/workflows/main.yml   # CI/CD pipeline
└── package.json
```

## Pipeline (`.github/workflows/main.yml`)
Trigger: push to `main`.

1. **test job** – checkout, set up Node 20, `npm ci`, `npm test`
2. **build-and-push job** (runs only if `test` succeeds) – log in to Docker Hub, build the image with Buildx, push `latest` and `<commit-sha>` tags

## Setup
1. Create a Docker Hub account and an **Access Token** (Account Settings → Security).
2. In this GitHub repo: **Settings → Secrets and variables → Actions → New repository secret**:
   - `DOCKERHUB_USERNAME` – your Docker Hub username
   - `DOCKERHUB_TOKEN` – the access token
3. Push to `main` and watch the **Actions** tab.

## Run locally
```bash
npm install
npm test
npm start                       # http://localhost:3000

docker build -t nodejs-demo-app .
docker run -p 3000:3000 nodejs-demo-app
```

## Test the workflow locally
Use [`act`](https://github.com/nektos/act): `act push`

## Screenshots
_Add screenshots of the successful Actions run and the image on Docker Hub here._
