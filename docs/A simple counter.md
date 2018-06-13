In this tutorial we are going to build a simple application where the user can
click on a button and increment a counter.

## The data model

As in the previous tutorial, we're going to start designing what the data model
should look like. In our case it's going to be really simple:

```rust
struct CounterApplication {
    counter: usize,
}
```

Once your app grows beyond the hello-world case, you will possibly also store
UI-related information in here, i.e. how many pixels wide a certain window pane
is open and so on.

## Layout

The layout part is split in two parts: The CSS and the DOM tree. Now



## Handling callbacks



## Unit testing our app

This is one of the places that azul shines at - because the callback is a simple
function, you can test in which places the callback modifies your data model. This
partly solves the problem of scalability: How do you, in a large application verify
what callbacks work correctly in any order? How do you know what data they modify,
what state they touch?

Azul allows (by default) that any callback modifies the whole application state.
This has the advantage that if one component has to talk to another component,
it doesn't need to know about the other component - both share the same data model.

```rust
#[test]
fn test_it_should_increment_the_button() {
    let mut app_state = AppState::new(CounterApplication { counter: 0 });
    my_button_click_handler(&mut app_state, WindowEvent::default());
    assert_eq!(app_state.data.lock().unwrap().counter, 1);
}
```

It is highly, **highly** recommended that you implement the `Default` trait on your
data model, because it makes the testing functions and initializing the data model
a lot easier:

```rust
let mut app_state = AppState::default();
my_button_click_handler(&mut app_state, WindowEvent::default());
assert_eq!(app_state.data.lock().unwrap().counter, 1);
```

and:

```rust
let mut app = App::new(AppState::default());
app.create_window(WindowCreateOptions::default(), Css::native());
app.run().unwrap();
```