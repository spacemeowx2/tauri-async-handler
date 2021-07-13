# tauri-async-handler

**Deprecated.** tauri now comes with its own asynchronous runtime.

## Usage

Cargo.toml:

```toml
[dependencies]
tauri-async-handler = "0.1"
```

src-tauri/main.rs:

```rust
mod cmd;

use serde_json::json;
use tauri_async_handler::*;

fn main() {
  tauri::AppBuilder::new()
    .async_handler(None, |cmd: cmd::Cmd| async {
      use cmd::Cmd::*;
      Ok(match cmd {
        MyCustomCommand{ argument } => {
          println!("arg {}", argument);
          let world = "world";
          json!({
            "hello": world
          })
        }
      })
    })
    .build()
    .run();
}

```

JavaScript:

```javascript
const myCustomCommand = (argument) => {
  return window.tauri.promisified({
    cmd: 'myCustomCommand',
    argument,
  })
}
myCustomCommand.then((r) => console.log('myCustomCommand', r))
```
