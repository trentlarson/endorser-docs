Endorser Docs
=============

Install tooling:

* `pkgx +python +pip.pypa.io sh`

* `pip install -U sphinx && python -m venv .venv`

Setup:

```
pkgx +pip.pypa.io sh
source .venv/bin/activate
```

Build: `make html`

View: `open build/html/index.html`

Deploy: `scp -i ... -r build/* ubuntu@endorser.ch:uport-demo/public/doc/`
