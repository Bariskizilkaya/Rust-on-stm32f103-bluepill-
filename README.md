```
sudo apt install openocd gdb-multiarch
```

```
rustup target install thumbv7m-none-eabi
```

```
cargo init hello_world
```

Create a new Rust project as you usually do with `cargo init`. The hello world
of embedded development is usually to blink an LED and code to do so is
available in [examples/blinky.rs](examples/blinky.rs). Copy that file to the
`main.rs` of your project.


```
[dependencies]
embedded-hal = "0.2.7"
nb = "1"
cortex-m = "0.7.6"
cortex-m-rt = "0.7.1"
# Panic behaviour, see https://crates.io/keywords/panic-impl for alternatives
panic-halt = "0.2.0"

[dependencies.stm32f1xx-hal]
version = "0.10.0"
features = ["rt", "stm32f103", "medium"]
```

.cargo/config
```
[target.thumbv7m-none-eabi]
runner = 'arm-none-eabi-gdb'
rustflags = [
  "-C", "link-arg=-Tlink.x",
]

[build]
target = "thumbv7m-none-eabi"
```
memory.x
```
/* Linker script for the STM32F103C8T6 */
MEMORY
{
  FLASH : ORIGIN = 0x08000000, LENGTH = 64K
  RAM : ORIGIN = 0x20000000, LENGTH = 20K
}
```





```
cargo build
```

```
cargo flash --chip stm32f103C8 --release
```