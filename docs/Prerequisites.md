Before you get started with Azul, you will have to install it first:

## Installing a supported Rust compiler (version 1.26 or later)

### Windows

!!! warning
    If you get prompted to install the MSVC toolchain, please download both the
    Visual C++ tools (available here) and install the Windows 8 or 10 SDK
    (which contains the actual linker) from the Visual Studio Tools installer.

!!! warning
    If you choose the MinGW / GNU toolchain on windows, 32-bit support is missing,
    due to problems with a C dependency. Because of this, we recommend you to use
    the MSVC toolchain on Windows.

```
DownloadFile https://win.rustup.rs/ -FileName rustup-init.exe
rustup-init -yv --default-toolchain stable --default-host x86_64-pc-windows-msvc
```

...or download the windows installer from here.

### Linux / Mac

```
curl https://sh.rustup.rs -sSf | sh
```

## Creating a new project

Once you have Rust and Cargo installed, create a new project in the
directory of your choice:

```bash
cargo new --bin my_first_azul_app
cd my_first_azul_app
cargo run
```

## Adding azul to your dependencies

Open the /my_first_azul_app/Cargo.toml file and paste the following
lines beneath the [dependencies] section:

```toml
[dependencies]
azul = "*"
```

This will pull in the latest stable version of azul. Open the
`/my_first_azul_app/src/main.rs` file and edit it to look like this:

```rust
extern crate azul;

fn main() {
    println!("Hello world!");
}
```

Ensure that azul builds correctly by running cargo run again. Azul
does not require third-party dependencies (dynamic libraries), it
should build out-of-the-box. If that's the case, you are ready to
move on to the next page, starting to actually build your first GUI
app with azul. If not, please report this as a bug.