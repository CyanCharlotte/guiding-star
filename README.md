# Project Guiding Star

A CTF contest platform aiming at **maximized possibility of customization** and **a fluid experience for users and developers**.

This platform hosts the 3rd [PKU GeekGame](https://geekgame.pku.edu.cn) with ≥2000 users and ≥10000 submissions. The server achieves a peak `load_5` of ≤0.5 when all features are turned on.

## Project Index

Backend (in Python) → [PKU-GeekGame/gs-backend](https://github.com/PKU-GeekGame/gs-backend)

Frontend (in React) → [PKU-GeekGame/gs-frontend](https://github.com/PKU-GeekGame/gs-frontend)

Challenge Docker → [PKU-GeekGame/geekgame-challenge-docker](https://github.com/PKU-GeekGame/geekgame-challenge-docker)

Live demo → [geekgame.pku.edu.cn](https://geekgame.pku.edu.cn)

Misc files → This repo

## Architecture

**Overall backend architecture:**

![architecture](figures/architecture.png)

**Case study: when a user submits a flag**

![submit_flag](figures/submit_flag.svg)

## Setup

Set up the backend: [refer to README from gs-backend](https://github.com/PKU-GeekGame/gs-backend)

Set up the frontend: [refer to README from gs-frontend](https://github.com/PKU-GeekGame/gs-frontend)

Start the backend processes. We use systemd: example configuration for [reducer](gs-reducer.service) and [worker](gs-worker.service) processes.

Use a reverse proxy (we use `nginx`) to proxy requests to backend or frontend: [an example configuration file](example.nginx-host.conf). Remember to also set a large value for both `worker_rlimit_nofile` and `worker_connections` in `nginx.conf`, because each online user will has a websocket connection to the backend.

To register the first user manually, visit `/service/auth/manual?identity=<your_name>`.
Manual login should be disabled in production environment by configuring `MANUAL_AUTH_ENABLED = False` in `src/secret.py` in the backend codebase.

Visit admin panel at `/<ADMIN_URL>`.
`ADMIN_URL` and `IS_ADMIN` can be configured in `src/secret.py` in the backend codebase.

## License

Both backend and frontend is distributed under MIT License. See their LICENSE files for more information.