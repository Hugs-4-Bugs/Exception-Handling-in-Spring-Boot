Here is the full `README.md` containing the exception handling methods in a Spring Boot application, along with some explanations:

```markdown
# Spring Boot Exception Handling Guide

In a Spring Boot application, exception handling is crucial for creating a robust and maintainable system. The following methods can be used to handle exceptions effectively:

## 1. Global Exception Handling with `@ControllerAdvice`

Spring provides a powerful mechanism to handle exceptions globally using the `@ControllerAdvice` annotation. This approach allows you to define a global exception handler that catches exceptions thrown in any controller.

### Example:

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleResourceNotFoundException(ResourceNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGeneralException(Exception ex) {
        return new ResponseEntity<>("An error occurred: " + ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

**Explanation:**
- `@ControllerAdvice`: A global exception handler that can handle exceptions across all controllers.
- `@ExceptionHandler`: Handles specific exceptions by specifying the exception class (e.g., `ResourceNotFoundException`).

---

## 2. Custom Exceptions

Custom exceptions allow you to define error scenarios specific to your application. By creating custom exception classes, you can better handle and categorize errors.

### Example:

```java
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

**Explanation:**
- A custom exception like `ResourceNotFoundException` extends `RuntimeException` and is thrown when a resource is not found.

---

## 3. Using `@ResponseStatus` Annotation

The `@ResponseStatus` annotation allows you to set the HTTP status code directly when a custom exception is thrown. This eliminates the need for manually returning a `ResponseEntity` with the status code.

### Example:

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

**Explanation:**
- `@ResponseStatus`: Automatically sets the HTTP status code (`HttpStatus.NOT_FOUND`) when the exception is thrown.

---

## 4. Controller-Level Exception Handling

If you need to handle exceptions at the controller level, you can use `@ExceptionHandler` inside specific controllers. This helps to localize the exception handling to the concerned controller.

### Example:

```java
@RestController
public class PostController {

    @ExceptionHandler(PostNotFoundException.class)
    public ResponseEntity<String> handlePostNotFound(PostNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```

**Explanation:**
- `@ExceptionHandler` is used within the controller to handle exceptions specific to that controller. In this case, the `PostNotFoundException` is handled.

---

## 5. Returning Custom Error Responses

Returning a detailed error response helps in providing more information about the error to the client. You can create an `ErrorResponse` class to structure the error details.

### Example:

```java
public class ErrorResponse {
    private String message;
    private int statusCode;
    private LocalDateTime timestamp;

    // Constructors, Getters, Setters
}
```

### Handler Example:

```java
@ExceptionHandler(ResourceNotFoundException.class)
public ResponseEntity<ErrorResponse> handleResourceNotFoundException(ResourceNotFoundException ex) {
    ErrorResponse error = new ErrorResponse(ex.getMessage(), HttpStatus.NOT_FOUND.value(), LocalDateTime.now());
    return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
}
```

**Explanation:**
- `ErrorResponse`: A custom class to structure the error response with attributes like `message`, `statusCode`, and `timestamp`.
- The exception handler returns this structured error response in a `ResponseEntity`.

---

## 6. Logging Errors

Logging errors is important for monitoring and debugging. You can use popular logging frameworks like SLF4J or Logback to log exceptions.

### Example:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@ControllerAdvice
public class GlobalExceptionHandler {

    private static final Logger logger = LoggerFactory.getLogger(GlobalExceptionHandler.class);

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGeneralException(Exception ex) {
        logger.error("An error occurred: ", ex);
        return new ResponseEntity<>("An error occurred: " + ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

**Explanation:**
- The `Logger` from SLF4J is used to log the exception details when an error occurs. This helps in monitoring and debugging the application.

---

## Conclusion

By combining these exception handling strategies, you can create a robust error-handling mechanism that improves both user experience and system maintainability. These approaches allow you to:
- Handle exceptions globally.
- Return custom error responses.
- Log errors for easier debugging and monitoring.

This will ensure your Spring Boot application can gracefully handle errors and provide useful feedback to clients.
```

This `README.md` file includes the following key points:
1. **Global Exception Handling** with `@ControllerAdvice`.
2. **Custom Exceptions** for specific error scenarios.
3. **Using `@ResponseStatus`** for automatic HTTP status codes.
4. **Controller-Level Exception Handling** for localized handling.
5. **Returning Custom Error Responses** with structured error information.
6. **Logging Errors** using SLF4J or Logback for monitoring and debugging.
```





### Join my Organization: 
Link: <a href="https://github.com/Tech-Hubs" target="_blank">PrabhatDevLab</a>


<p>Happy Learning! 📚✨ Keep exploring and growing your knowledge! 🚀😊</p>
