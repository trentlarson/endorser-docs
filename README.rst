Endorser Docs
=============

Install tooling:

```
pkgx +python +pip.pypa.io sh
pip install -U sphinx && python -m venv .venv
`

Setup & Build:

```
pkgx +python +pip.pypa.io sh
source .venv/bin/activate
make html
open build/html/index.html
```

Deploy: `scp -i ~/.ssh/.....pem -r build/* ubuntu@endorser.ch:uport-demo/build/doc/`
