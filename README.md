# Replica

Wally packages of [MadStudioRoblox/Replica](https://github.com/MadStudioRoblox/Replica), loleris' server to client state
replication module, split into a server and a client package.

```toml
[dependencies]
ReplicaClient = "furukan/replicaclient@0.5.2"

[server-dependencies]
ReplicaServer = "furukan/replicaserver@0.3.1"
```

## Changes from upstream

Both packages are based on upstream commit `9cae236`. Each package carries its own copy of `ReplicaShared` and requires
it through `script.ReplicaShared`, so it works from any location in the DataModel.

- **Generic types:** `Replica<TData, TTags>` on both sides, with typed `Replica.New`, `Replica.OnNew` and `Replica.FromId`.
- **ReplicaServer:** `OnSet`, `OnWrite` and `OnChange` listeners on the server, fired once a change has been sent to
  clients; changes made inside a `:Write()` are listened to after the whole write replicates.
- **ReplicaClient:** `Replica:Hold(write_name)` / `Replica:Release(write_name)` queue incoming `:Write()` updates of
  that name until released; the client `Replica` type includes the setter methods.

The full history, with a tag for every published version, is in this repository.

## Development

Open the repository root in VS Code; luau-lsp builds one sourcemap for both packages from the root
`default.project.json`. Tools are pinned with Rokit (`rokit install`). Each package is published from its own folder:

```sh
wally publish --project-path ReplicaClient
wally publish --project-path ReplicaServer
```

## License

Replica is licensed under the [Apache License 2.0](LICENSE), and so are these packages. Versions up to
`replicaclient@0.5.1` and `replicaserver@0.3.0` were published with an incorrect `MIT` license field; Wally does not allow
republishing a version, so the field is corrected from `replicaclient@0.5.2` and `replicaserver@0.3.1` on, and those
earlier versions are covered by the Apache License 2.0 as well.
