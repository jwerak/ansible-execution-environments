# Example EEs

To just build the EE context.

```bash
ansible-builder build -v 3
```

Two build both the EE context and the container image.

```bash
ansible-builder create -v 3
podman build -f context/Containerfile -t ansible-execution-env:latest context
```

In case your are either pulling or pushing to a private registry.

```bash
ansible-builder create -v 3
podman build --authfile .authfile -f context/Containerfile -t ansible-execution-env:latest context
```

## Build all EEs

```bash
for dir in `ls -d */ | sed 's/\///'`; do
    echo "Building EE from directory $dir"
    cd "$dir"
    ansible-builder build --tag quay.io/jwerak/ansible-ee-$dir
    cd -
done
```
