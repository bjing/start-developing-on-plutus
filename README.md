# Start Developing on Plutus
Plutus is a smart contract platform that allows you to develop dApps on the Cardano blockchain.

Setting up your development environment for Plutus takes a bit of time. Follow instructions in the [Plutus Starter Project Template] to set it up.

In this repo, I only include things that aren't obvious from the official Plutus documentation. There are also quick reference links at the end of the README.

## Haskell Development Environment
### GHC
The [Plutus Starter Project Template] uses Cabal and relies on a global GHC setup. As a Haskell Stack user, I really don't like having global compiler/tool installations. They quickly get out of date and can causes issues if your various projects use different versions of GHC. Use the following instruction to set up GHC unless your project uses Stack.

The quickest way to get started is to follow these instructions to install GHC: https://www.haskell.org/ghcup/

Or if you are a Stack user like me,

* install Stack, on OSX,
  ```
  brew install haskell-stack
  ```
* install ghc
  ```sh
  stack install ghc
  ```
* Put `~/.stack/programs/x86_64-osx/ghc-<your-version>/bin/` into your shell's `$PATH`, so that GHC can be found when you do `cabal install` in your Cabal project. If you are unsure of your compiler path, run `stack path | grep compiler-exe` to find out.


### IDE Setup
Refer to my [Haskell IDE Setup repo] for instructions on various editors/IDEs, including VSCode, VIM, Spacemacs and Atom (no longer updated).

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
curl -L https://nixos.org/nix/install | sh
```
However, this won't work if you are on the latest OSX version. Use the following instead:

```sh
sh <(curl -L https://nixos.org/nix/install) --darwin-use-unencrypted-nix-store-volume
```

### Plutus Playground Server
In your local [Plutus] checkout,
1. start a nix shell. If this is your first time running nix-shell, give it some time to pull down and install dependencies. This can take quite a while.
    ```sh
    nix-shell
    ```
   and run:
    ```sh
    cd plutus-playground-client && plutus-playground-server
    ```
2. in a new nix-shell, run:
    ```sh
    cd plutus-playground-client && npm start
    ```
3. go to `http://localhost:8009` to visit your local Plutus playground.

## Q&A
If you have trouble downloading `purty` while building Plutus on OSX, and are getting something like this:
```
curl: (22) The requested URL returned error: 403 Forbidden
error: cannot download download_file?file_path=purty-6.2.0-osx.tar.gz from any mirror
```
do the following:
```sh
sudo mkdir /etc/nix
sudo touch /etc/nix/nix.conf
```
and put the following two lines in the file you just created:
```
substituters        = https://hydra.iohk.io https://iohk.cachix.org https://cache.nixos.org/
trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iohk.cachix.org-1:DpRUyj7h7V830dp/i6Nti+NEO2/nhblbov/8MW7Rqoo= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=
```
I suggest doing this before you start the build. It will make your life much easier.


## Resources
[Plutus Official Docs] - start from here

[Plutus Community Docs] - amazing community docs. If you have trouble setting up your dev env, whatever your system is, be sure to look here first.

[Plutus Code Repo]

[Online Plutus Playground]

[Plutus Pioneer Program videos] - comprehensive intro to Plutus

[Plutus Pioneer Program Code]

[Plutus Starter Project Template] - start a new project from here



[Haskell IDE Setup repo]: https://github.com/bjing/haskell-ide-setup
[Nix website]: https://nixos.org/download.html#nix-quick-install
[Online Plutus Playground]: https://playground.plutus.iohkdev.io/
[Plutus]: https://github.com/input-output-hk/plutus
[Plutus Code Repo]: https://github.com/input-output-hk/plutus
[Plutus Community Docs]: https://docs.plutus-community.com/
[Plutus Official Docs]: https://plutus.readthedocs.io/en/latest/
[Plutus Starter Project Template]: https://github.com/input-output-hk/plutus-starter
[Plutus Pioneer Program Code]: https://github.com/input-output-hk/plutus-pioneer-program
[Plutus Pioneer Program videos]: https://youtu.be/wqC8oiurqsI?list=PLnPTB0CuBOBypVDf1oGcsvnJGJg8h-LII
