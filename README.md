# Mutagen Sync

```shell
brew install mutagen-io/mutagen/mutagen
mutagen daemon start
mutagen sync list

mutagen sync create \
 --name=<name of sync> \
 /local/path/to/code docker://<container user>@<container name>/container/path/to/code
```

## References

- [https://medium.com/@marickvantuil/speed-up-docker-for-mac-with-mutagen-14c2a2c9cba7](https://medium.com/@marickvantuil/speed-up-docker-for-mac-with-mutagen-14c2a2c9cba7)
