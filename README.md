### usage

```
go get github.com/vektah/ior

cd $GOPATH/src/github.com/you/yourapp
ior -listen ":1234" -- [args passed through to your app]
```

### What it does

1. Wait for a request.
2. Hashes all go files, excluding vendor, and other common large directories
3. If the hash changes, do a `go install`, show errors if it fails otherwise restart the server

Thats it. No inotify, no fsevents, no polling, no CPU chewing. 100% docker safe. 100% nfs friendly.

### How long does it take really?

On a project with ~30k lines across ~300 files it adds about 50ms to every request, this is just the time it takes to hash.

Because its using `go install` rather than `go build` it also leverages the pkg cache, so small changes are pretty quick to compile.