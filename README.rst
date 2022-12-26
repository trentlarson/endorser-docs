Endorser Docs
=============

Set up tooling: `pip install -U sphinx && python -m venv .venv`

Build: `make html`

View: `open build/html/index.html`

Deploy: `scp -i ... -r build/* ubuntu@endorser.ch:uport-demo/public/doc/`
