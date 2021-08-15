# Start Developing on Plutus
Plutus is a smart contract platform that allows you to develop dApps on the Cardano blockchain.

Setting up your development environment for Plutus takes a bit of time. Follow instructions in the [Plutus Starter Project Template] to set it up.

In this repo, I only include things that aren't obvious from the official Plutus documentation. There are also quick reference links at the end of the README.

## Local Plutus Playground
Plutus offers an online playground for you to test your smart contracts, however you may want to run the Plutus Playground locally. To do that, you'll need:
- matching Plutus version
- Nix shell
- plutus playground server

### Matching Plutus Version
You need to make sure the Plutus repo hash specified in your project's `project.cabal` matches your local Plutus repo checkout.

For example, if you have this in your project.cabal,
```cabal
source-repository-package
  type: git
  location: https://github.com/input-output-hk/plutus.git
  subdir:
    ...
    ...
  tag: ea0ca4e9f9821a9dbfc5255fa0f42b6f2b3887c4
```
make sure `tag` matches your local Plutus's git hash (use `git log -n1` to check). If they don't match, simply go to your Plutus repo and `git checkout <hash>`.

### Install Nix on OSX
On [Nix website], it suggests this command to install NIX:
```sh
$ curl -L https://nixos.org/nix/install | sh
```
However, this won't work if you are on the latest OSX version. Use the following instead:

```sh
$ sh <(curl -L https://nixos.org/nix/install) --darwin-use-unencrypted-nix-store-volume
```

### Plutus Playground Server
In your local [Plutus] checkout,
1. start nix shell. If this is your first time running nix-shell, give it some time to pull down and install dependencies. This can take quite a while.
    ```sh
    $ nix-shell
    ```
2. go to subfolder `plutus-playground-client`, run
    ```sh
    $ plutus-playground-server

    $ npm start
    ```
3. go to `http://localhost:8009` to visit your local Plutus playground.

## Resources
[Plutus Official Docs]

[Plutus Code Repo]

[Online Plutus Playground]

[Plutus Pioneer Program videos]

[Plutus Pioneer Program Code]

[Plutus Starter Project Template]


[Nix website]: https://nixos.org/download.html#nix-quick-install
[Online Plutus Playground]: https://playground.plutus.iohkdev.io/
[Plutus]: https://github.com/input-output-hk/plutus
[Plutus Code Repo]: https://github.com/input-output-hk/plutus
[Plutus Official Docs]: https://plutus.readthedocs.io/en/latest/
[Plutus Starter Project Template]: https://github.com/input-output-hk/plutus-starter
[Plutus Pioneer Program Code]: https://github.com/input-output-hk/plutus-pioneer-program
[Plutus Pioneer Program videos]: https://youtu.be/wqC8oiurqsI?list=PLnPTB0CuBOBypVDf1oGcsvnJGJg8h-LII
