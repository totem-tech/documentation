### Trying out Totem Meccano

#### Running a node on the Meccano network

The code in this repository will enable you to join and support Meccano as a simple node.

If you wish to become a validator or authority on the network, please contact us at mailto:info@totemaccounting.com?subject=Inquiry:%20Becoming%20a%20Validator%20or%20Authority%20on%20Totem[info@totemaccounting.com]

We recommend you use on of the current binaries which can be found here.
If you are running the binaries, skip to the  <<#binary>> section.

Otherwise if you would like to compile and run the code from source follow the instructions below.

#### Dependencies

Totem is built using the Rust languange, but you will need to prepare your environment first. 

 - Linux:
[source, shell]
sudo apt-get update
sudo apt install build-essential
sudo apt install cmake pkg-config libssl-dev git clang libclang-dev

 - Mac:
[source, shell]
brew install cmake pkg-config openssl git llvm

 - Windows (PowerShell):
+
[source, shell]
----
#### Install LLVM
#### Download and install the Pre Build Windows binaries
##### of LLVM  from http://releases.llvm.org/download.html

#### Install OpenSSL (through vcpkg)

```shell
  mkdir \Tools
  cd \Tools
  git clone https://github.com/Microsoft/vcpkg.git
  cd vcpkg
  .\bootstrap-vcpkg.bat
  .\vcpkg.exe install openssl:x64-windows-static

  $env:OPENSSL_DIR = 'C:\Tools\vcpkg\installed\x64-windows-static'
  $env:OPENSSL_STATIC = 'Yes'
  [System.Environment]::SetEnvironmentVariable('OPENSSL_DIR', $env:OPENSSL_DIR, [System.EnvironmentVariableTarget]::User)
  [System.Environment]::SetEnvironmentVariable('OPENSSL_STATIC', $env:OPENSSL_STATIC, [System.EnvironmentVariableTarget]::User)
```

Now you can install `Rustup` which installs `Rust` and its package manager `Cargo`. These commands also switch to the `nightly` rust toolchain and a special `C` compiler for `wasm` (WebAssembly).

```shell
  curl https://sh.rustup.rs -sSf | sh
  # on Windows download and run rustup-init.exe
  # from https://rustup.rs instead

  rustup update nightly
  rustup target add wasm32-unknown-unknown --toolchain nightly
  rustup update stable
  cargo install --git https://github.com/alexcrichton/wasm-gc
```

Then, clone this repo to get the Totem source code:

```shell
  git clone https://gitlab.com/totem-tech/totem-substrate.git
  cd totem-substrate
```

Then build the code:

```shell
  ./scripts/build.sh  		# Builds the WebAssembly binaries
  cargo build --release 				# Builds all native code
```

Detailed logs may be shown by running the node with the following environment variables set: `RUST_LOG=debug RUST_BACKTRACE=1 cargo run`.


#### Joining the Totem Meccano network

Starting the runtime for the Totem network maybe slightly different depending on if you compiled the code or if you are executing the binary that you downloaded.

[#compiled]
#### Executing the self-compiled code
Below we describe how to execute the code if you compiled the code from this repo.

Below is an example of some parameters you can use to start your node. These are not mandatory as the node will start without these if you execute either `cargo run --release` or `./target/release/totem-meccano` you can also navigate directly to the node binary that you have compiled and execute 

[source, shell]
  cd /target/release/
  ./totem-meccano

Any of these will execute the binary.

####= Execution options

Because Totem is built on Parity's Substrate framework, you can execute all the flags and options that you would expect with a Substrate blockchain. See the possibilities by appending `--help`. (For clarity Meccano is based on Substrate v1.0).

In the following example we are running a Totem node called Alice on TCP port of 30334 with her chain database stored locally at `/tmp/alice`. 

[source, shell]
cargo run --release \-- \
  --base-path /tmp/alice \
  --alice \
  --port 30334 \

[#binary]
####= Executing the binary

Once you have downloaded the binary all you have to do is navigate to the directory and execute the code:

[source, shell]
  cd /target/release/
  ./totem-meccano

If you are running in a desktop you can also simply open the binary to begin execution. The options mentioned in <<#compiled>> only apply if you are running on the command line.

If you are successful, you will see your node syncing at https://telemetry.polkadot.io/#/Totem%20Meccano


### License

Totem is building under the same https://github.com/paritytech/substrate/blob/master/LICENSE[license] as the Substrate framework.

### Contributing Guidelines

include::CONTRIBUTING.adoc[]

#### Contributor Code of Conduct

include::CODE_OF_CONDUCT.adoc[]
