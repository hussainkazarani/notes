## Types
we have 2 types of keys:
1. **SSH Keys** &rarr; they are used for authentication
2. **Signing Keys** &rarr; they are used for verification

we get 2 keys on Generation, a private key and a public key. the private key stays on machine while the public key is sent to clients (Github, Bitbucket) and they perform a puzzle which is only solvable with the private key.

## SSH Keys
### Creation
```
ssh-keygen -t ed25519 -C "hussainkazarani@gmail.com"

~/.ssh/id_ed25519        ← private
~/.ssh/id_ed25519.pub    ← public

```

### Usage
add it to `ssh-agent` for MacOS to remember it
```bash
# to start it
ssh-agent
ssh-add ~/.ssh/id_ed25519
```

now add the public key to the Client
```
cat ~/.ssh/id_ed25519.pub
```

## Signing Keys
### Creation & Usage
we can use the same key for signing and ssh. Add it to the `Client` as a `Signing Key`
```
cat ~/.ssh/id_ed25519.pub
```

## Testing
you can test for the different `Clients` using the following commands:
```bash
# -T is for no interactive terminal and leave
ssh -T git@github.com
ssh -T git@bitbucket.org
```
