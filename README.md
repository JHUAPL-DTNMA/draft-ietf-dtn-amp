Prerequisites to building can be installed on Ubuntu with:
```
sudo apt-get install -y cmake python3-pip python3-wheel ruby xmlstarlet aspell
pip3 install abnf xml2rfc
crate install cddl
```
and update the user's path similar to
```
export PATH="${PATH}:$HOME/.cargo/bin
```

The `deps.cddl` should be copied from built ARI document `combined.cddl` without its start rule
```sh
grep -v "start =" ../ari/build/default/combined.cddl >deps.cddl
```
and then the document can be built with
```
cmake -S . -B build/default
cmake --build build/default
```
finally opened with
```
xdg-open build/default/draft-*.html
```

Examples can be checked after building with ACE tool:
```
cat amp/build/default/uri.txt | ace_ari --log-level=warning --inform=text --outform=text
cat amp/build/default/cborhex.txt | xxd -r -p | ace_ari --log-level=warning --inform=cbor --outform=text
```