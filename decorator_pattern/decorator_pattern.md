## The Decorator Pattern in Dart: A Complete Example

The Decorator Pattern is a structural design pattern that allows adding behavior to objects dynamically without affecting other objects of the same class. It achieves this by wrapping objects in additional layers of functionality, known as decorators.

**Benefits:**

-   **Dynamic Behavior Addition:** Allows adding new functionalities to existing objects without modifying their original code.
-   **Open/Closed Principle:** Follows the open/closed principle by allowing extensions without modifying the core functionality.
-   **Flexibility:** Supports composing different decorators to achieve desired levels of complexity.
-   **Loose Coupling:** Decouples the core functionality from the added behaviors, making it easier to test and maintain.

**Implementation:**

The Decorator pattern involves three main components:

-   **Component:** The abstract class or interface representing the core functionality.
-   **Concrete Component:** Concrete implementations of the component that provide the basic functionality.
-   **Decorator:** An abstract class or interface defining the additional behavior to be added.
-   **Concrete Decorator:** Concrete implementations of the decorator that add specific functionalities to the component.

**Example:**

Consider a simple example of decorating text with different formats:

Dart

```
// Component - abstract base class
abstract class TextFormat {
  String formatText(String text);
}

// Concrete component - plain text
class PlainText implements TextFormat {
  @override
  String formatText(String text) => text;
}

// Decorator - abstract base class for adding functionalities
abstract class TextDecorator implements TextFormat {
  final TextFormat _textFormat;

  TextDecorator(this._textFormat);

  @override
  String formatText(String text) => _textFormat.formatText(text);
}

// Concrete decorator - adds bold formatting
class BoldTextDecorator extends TextDecorator {
  BoldTextDecorator(TextFormat textFormat) : super(textFormat);

  @override
  String formatText(String text) => '<b>${super.formatText(text)}</b>';
}

// Concrete decorator - adds italic formatting
class ItalicTextDecorator extends TextDecorator {
  ItalicTextDecorator(TextFormat textFormat) : super(textFormat);

  @override
  String formatText(String text) => '<i>${super.formatText(text)}</i>';
}

```


**Usage:**

Dart

```
// Create a plain text component
final text = PlainText();

// Decorate with bold and italic formatting
final decoratedText = BoldTextDecorator(ItalicTextDecorator(text));

// Format the text
final formattedText = decoratedText.formatText('Hello, World!');

print(formattedText); // Output: <b><i>Hello, World!</i></b>

```


**Additional Notes:**

-   Decorators can be combined to create complex functionalities.
-   The order of decorators matters, as inner decorators are applied first and outer decorators later.

**Alternatives:**

-   Inheritance: Can be used for simple cases where behavior variations are limited.
-   Strategy pattern: Offers more flexibility for dynamically changing algorithms.

Remember, the Decorator pattern is best suited for scenarios where you need to add functionalities to existing objects dynamically without modifying their original code. It promotes flexible and extensible code design, but it's essential to avoid over-decorating objects, as it can lead to complexity and performance issues.