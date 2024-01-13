Endorser Docs
=============

Install tooling:

* `pkgx +pip.pypa.io sh`

* `pip install -U sphinx && python -m venv .venv`

Setup: `pkgx +pip.pypa.io sh`

Build: `make html`

View: `open build/html/index.html`

Deploy: `scp -i ... -r build/* ubuntu@endorser.ch:uport-demo/public/doc/`
