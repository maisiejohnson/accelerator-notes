# REACT: JSX

## JSX

- JSX is a syntax extension of JavaScript that combines the JavaScript and HTML-like syntax to provide highly functional, reusable markup.
- It’s used to create DOM elements which are then rendered in the React DOM.
- While not required in React, JSX provides a neat visual reqresentation of the application’s UI.
- JSX is not valid JavaScript so web browsers can’t read it. Thus, a JavaScript file containing JSX will have to be compiled before it reaches a web browser. This means that before the file reaches a web browser, a JSX compiler will translate any JSX into regular JavaScript.

## JSX Elements

- A basic unit of JSX is called an **element**
- An example of a JSX **element** is:
  ```JSX
  <h1>Hello world</h1>
  ```
- Notice that this looks just like HTML
- JSX **elements** are treated as JavaScript **expressions**. Thus, they can go anywhere that a JavaScript expression can go, e.g., they can be assigned to a variable, passed to a function, stored in an object or array etc.
- JSX elements can be _nested_ inside of each other.
- To keep nested elements readable use HTML-style line breaks and indentation. Note however that if a JSX expression takes up more than one line, then you must wrap the multi-line JSX expression in parentheses. E.g.,
  ```JSX
    (
        <div>
            <h1>
                Hello, World!
            </h1>
        </div>
    )
  ```
- Nested JSX expressions can be saved as variables, passed to functions, etc., just like non-nested JSX expressions.
- Note however, that a JSX expression but have exactly one outermost element. We can use empty tags as the outermost element if necessary, e.g.,:
  ```JSX
  (
      <>
          <h1>Hello, World!</h1>
          <p>Example text here...</p>
      </>
  )
  ```

## JSX Attributes

- JSX elements can have **attributes**
- A JSX attribute is written using HTML-like syntax: a name, followed by an equals sign, followed by a value, with the value being wrapped in quotes. E.g.,
  ```JSX
  my-attribute-name = "my-attribute-value"
  ```
- A single JSX element can have many attributes, just like in HTML

## Differences Between JSX and HTML

### class vs className

- In HTML, it’s common to use class as an attribute name.
- However, in JSX you can’t use the word class; you have to use className instead.
- This is because JSX gets translated into JavaScript, and class is a reserved word in JavaScript. When JSX is rendered, JSX className attributes are automatically rendered as class attributes.

  ```JSX
  // HTML
  <h1 class="big">Title</h1>

  //JSX
  <h1 className="big">Title</h1>
  ```

### Self-closing Tags

- When you write a self-closing tag in HTML, it is optional to include a forward slash immediately before the final angle bracket.

  ```JSX
  // Fine in HTML with a slash:
  <br />

  // Also fine, without the slash:
  <br>
  ```

- In JSX, you have to include the slash. If you write a self-closing tag in JSX and forget the slash, you will raise an error.

  ```JSX
  // Fine in JSX:
  <br />

  // NOT FINE AT ALL in JSX:
  <br>
  ```

## JavaScript in JSX

- Any code in between the tags of a JSX element will be read as JSX, not as regular JavaScript.
- Any JavaScript code in JSX must be wrapped in curly braces.
- Anything inside curly braces is treated as regular JavaScript.
- You can access JavaScript **variables** while inside of a JSX expression, even if those variables were declared outside of the JSX code block, providing that the variable is wrapped in curly braces in the JSX expression.

  ```JSX
  // Declare a variable:
  const name = 'Maisie';

  // Access your variable inside of a JSX expression:
  const greeting = <h1>Hello, my name is {name}</h1>
  ```

### JavaScript in Attributes

- When writing JSX, it is also common to use variables to set **attributes**. For example:

  ```JSX
  const pics = {
  panda: "http://bit.ly/1Tqltv5",
  owl: "http://bit.ly/1XGtkM3",
  owlCat: "http://bit.ly/1Upbczi"
  };

  const panda = (
  <img
      src={pics.panda}
      alt="Lazy Panda" />
  );

  const owl = (
  <img
      src={pics.owl}
      alt="Unimpressed Owl" />
  );

  const owlCat = (
  <img
      src={pics.owlCat}
      alt="Ghastly Abomination" />
  );
  ```

### Event Listeners in JSX

- JSX elements can have event listeners, just like HTML elements can.
- You create an event listener by giving a JSX element a special attribute.
- An event listener attribute’s value should be a function. For example:

  ```JSX
  // function defined elsewhere
  function clickAlert() {
  alert('You clicked this image!');
  }
  // event listener in JSX
  <img onClick={clickAlert} />
  ```

- Note that in HTML, event listener names are written in all lowercase, such as `onclick` or `onmouseover`. In JSX, event listener names are written in **camelCase**, such as `onClick` or `onMouseOver`.

### JSX Conditionals

- You can't inject an `if` statement into JSX.
- To get around this you can take the if statement outside of the JSX, and istead have the JSX in the if statement. For example:

  ```JSX
  // THIS WILL NOT WORK
  const text = <h1>
      {
          if (condition === true) {
              'text 1'
          } else {
              'text 2'
          };
      }
  </h1>

  // THIS WILL WORK
  if (condition === true) {
      const text = <h1>text 1</h1>
  } else {
      const text = <h1>text 2</h1>
  };
  ```

- Another way to write conditionals is using the **ternary operator**
- The ternary operator can be used inside JSX elements providing that the ternary expression is wrapped in curly braces. For example:
  ```JSX
  const text = <p>{ conditional ? valIfTrue : valIfFalse }</p>
  ```
- For '**and**' statements use the `&&` operator
- For '**or**' statements use the `||` operator
- For '**not**' statements use the `!` operator

### Using the `.map()` Operator in JSX

- The .map() array method comes up often in React so it’s good to get in the habit of using it alongside JSX.
- If you want to create a list of JSX elements, then using .map() is often the most efficient way.
- For example:

```JSX
const strings = ['Home', 'Shop', 'About Me'];
const listItems = strings.map(string => <li>{string}</li>);
<ul>{listItems}</ul>
```

## JSX `key` Attribute

- When you make a list in JSX, sometimes your list will need to include something called `keys`
- A `key` is a JSX attribute. The attribute’s name is `key`. The attribute’s value should be something unique, similar to an `id` attribute.
- keys don’t do anything visible. React uses them internally to keep track of lists. If you don’t use keys when you’re supposed to, React might accidentally scramble your list items into the wrong order.
- Not all lists need to have keys. A list needs keys if either of the following is true:
  1. The list items have memory from one render to the next. For instance, when a to-do list renders, each item must “remember” whether it was checked off.
  2. A list’s order might be shuffled. For instance, a list of search results might be shuffled from one render to the next.
