## 226. What is DispatcherServlet?

**Answer:**
**DispatcherServlet** is the **Front Controller** in Spring MVC.
*   **Role:** It receives **all** incoming HTTP requests and delegates them to the appropriate controllers.
*   **Workflow:**
    1.  Receive Request.
    2.  Consult `HandlerMapping` to find the correct Controller.
    3.  Call the Controller method.
    4.  Receive Model and View name.
    5.  Consult `ViewResolver` to find the physical view file (JSP/Thymeleaf).
    6.  Render the view and return the response.

---

## 227. Explain Spring MVC architecture.

**Answer:**
Spring MVC is request-driven, designed around a central servlet that dispatches requests to controllers.
1.  **Request** -> **DispatcherServlet**
2.  **DispatcherServlet** -> **HandlerMapping** (Which controller?)
3.  **DispatcherServlet** -> **Controller** (Execute logic)
4.  **Controller** -> **DispatcherServlet** (Return Model & View Name)
5.  **DispatcherServlet** -> **ViewResolver** (Which file?)
6.  **DispatcherServlet** -> **View** (Render HTML)
7.  **Response** -> **Client**

---

## 228. What is @Controller?

**Answer:**
`@Controller` is a stereotype annotation used to mark a class as a Spring MVC Controller.
*   **Component:** It is a specialization of `@Component`, so it is auto-detected by component scanning.
*   **Role:** Handles web requests.
*   **Return Value:** By default, methods return a **String** representing the **View Name** (e.g., "home" -> `home.jsp`), which needs a ViewResolver.

---

## 229. What is @RestController?

**Answer:**
`@RestController` is a convenience annotation that combines `@Controller` and `@ResponseBody`.
*   **Purpose:** Used for creating **RESTful Web Services**.
*   **Return Value:** Methods return **Data** (domain objects/collections) directly written to the HTTP response body as JSON/XML (not a View Name).
*   **Equivalence:** `@RestController` = `@Controller` + `@ResponseBody`.

---

## 230. What is @RequestMapping?

**Answer:**
`@RequestMapping` is used to map HTTP requests to handler methods of MVC and REST controllers.
*   **Attributes:**
    *   `value` / `path`: URL pattern (`/users`).
    *   `method`: HTTP method (`GET`, `POST`).
    *   `consumes`: Content-Type accepted (`application/json`).
    *   `produces`: Content-Type returned.
*   **Shortcuts:** `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`.

---



---

## 231. Difference between GET and POST mapping?

**Answer:**
*   **@GetMapping:** Maps HTTP GET requests. Used for **retrieving** data. Safe and Idempotent.
*   **@PostMapping:** Maps HTTP POST requests. Used for **creating** new resources. Not Idempotent.
*   **Technical:** `@GetMapping` is a shortcut for `@RequestMapping(method = RequestMethod.GET)`.

---

## 232. What is @PathVariable?

**Answer:**
**@PathVariable** extracts values from the URI path segment.
*   **Usage:** When the URL contains dynamic values identifying a resource.
*   **Example:**
    ```java
    @GetMapping("/users/{id}")
    public User getUser(@PathVariable("id") Long id) { ... }
    ```
    URL: `/users/101` -> `id = 101`.

---

## 233. What is @RequestParam?

**Answer:**
**@RequestParam** extracts query parameters from the URL.
*   **Usage:** Filtering, sorting, or optional parameters.
*   **Example:**
    ```java
    @GetMapping("/users")
    public List<User> search(@RequestParam("name") String name) { ... }
    ```
    URL: `/users?name=John` -> `name = "John"`.

---

## 234. What is @RequestBody?

**Answer:**
**@RequestBody** maps the **HTTP Request Body** to a Java Object.
*   **Usage:** Typically used in POST/PUT methods to send complex data (JSON/XML).
*   **Converter:** Uses `HttpMessageConverter` (like Jackson) to deserialize JSON to Java.

---

## 235. What is @ResponseBody?

**Answer:**
**@ResponseBody** indicates that the return value of a method should be written directly to the **HTTP Response Body** rather than resolving to a view.
*   **Usage:** REST APIs returning JSON/XML.
*   **Default:** implicitly added in `@RestController`.

---

## 236. What is ResponseEntity?

**Answer:**
**ResponseEntity** represents the entire HTTP response: **Status Code**, **Headers**, and **Body**.
*   **Control:** It gives you full control over the response.
*   **Example:**
    ```java
    return ResponseEntity.status(HttpStatus.CREATED)
            .header("Custom-Header", "foo")
            .body(newUser);
    ```

---

## 237. What is HttpMessageConverter?

**Answer:**
**HttpMessageConverter** is a strategy interface that converts data between HTTP requests/responses and Java objects.
*   **Serialization:** Object -> JSON/XML (Response).
*   **Deserialization:** JSON/XML -> Object (Request).
*   **Common Impls:** `MappingJackson2HttpMessageConverter` (JSON), `StringHttpMessageConverter`.
*   **Trigger:** Automatically selected based on `Content-Type` and `Accept` headers.

---

## 238. What is content negotiation?

**Answer:**
**Content Negotiation** is the mechanism to determine the best representation for a given resource when multiple representations are available.
*   **Driver:** The Client sends an `Accept` header (e.g., `application/json` or `application/xml`).
*   **Server:** Spring MVC checks the `Accept` header and uses the appropriate `HttpMessageConverter` to produce the response.

---

## 239. What is @ModelAttribute?

**Answer:**
**@ModelAttribute** binds a method parameter or method return value to a named model attribute, exposed to a web view.
*   **Parameter:** Maps form data / query params to a Java bean. `public String save(@ModelAttribute User user)`.
*   **Method:** Populates the model with attributes before controller methods run. `@ModelAttribute("categories") public List<String> getCategories() { ... }`.

---

## 240. What is data binding?

**Answer:**
**Data Binding** is the process of binding HTTP request parameters (strings) to Java Objects (typed fields).
*   **Component:** `DataBinder`.
*   **Mechanism:** It uses PropertyEditors or Converters to convert String values (from URL/Form) to types like `int`, `Date`, `boolean`.
*   **Errors:** Validation errors are captured in `BindingResult`.

---

## 241. What is validation in Spring MVC?

**Answer:**
**Validation** ensures that the data received from the client meets specific criteria before processing.
*   **JSR-303/JSR-380 (Bean Validation):** Standard API (Hibernate Validator is the reference implementation).
*   **Annotations:** `@NotNull`, `@Size`, `@Email`, `@Min`, `@Max`.
*   **Usage:** Annotate fields in your DTO/Model, and use `@Valid` in the controller method.

---

## 242. What is @Valid vs @Validated?

**Answer:**
*   **@Valid:** Standard JSR-303 annotation. Put it on a method parameter to trigger validation.
*   **@Validated:** Spring's variant.
    *   **Features:** Supports **Validation Groups** (validate different fields for Create vs Update).
    *   **Scope:** Can be used on **Class level** (for validating `@RequestParam`/`@PathVariable`) which `@Valid` cannot handle directly.

---

## 243. What is BindingResult?

**Answer:**
**BindingResult** is a Spring object that holds the result of the validation and binding and contains any errors that may have occurred.
*   **Order:** It **must** immediately follow the model object being validated in the method signature.
*   **Usage:**
    ```java
    public String save(@Valid User user, BindingResult result) {
        if (result.hasErrors()) {
            return "error-page";
        }
        // ...
    }
    ```

---

## 244. What is @ExceptionHandler?

**Answer:**
**@ExceptionHandler** is an annotation used to handle exceptions thrown during the execution of request handlers.
*   **Scope:** By default, it handles exceptions only from the **same controller**.
*   **Usage:** Define a method that takes the Exception type as an argument and returns an appropriate error response/view.

---

## 245. What is @ControllerAdvice?

**Answer:**
**@ControllerAdvice** allows you to share `@ExceptionHandler`, `@InitBinder`, and `@ModelAttribute` methods across **multiple controllers**.
*   **Purpose:** Global Exception Handling.
*   **Benefit:** Centralized error handling logic, reducing code duplication in individual controllers.

---

## 246. What is Interceptor in Spring?

**Answer:**
**HandlerInterceptor** intercepts requests **before** they reach the DispatcherServlet's handler (Controller) and **after** the handler finishes.
*   **Methods:**
    1.  `preHandle()`: Before controller. Return `false` to abort request.
    2.  `postHandle()`: After controller, before view render.
    3.  `afterCompletion()`: After view render (cleanup).
*   **Use Case:** Logging, authentication, modifying the model globally.

---

## 247. Filter vs Interceptor difference?

**Answer:**

| Feature | Filter (Servlet) | Interceptor (Spring) |
| :--- | :--- | :--- |
| **Level** | **Low-level** (Servlet Container). | **High-level** (Spring Context). |
| **Scope** | Runs for *all* web requests (including static resources). | Runs only for requests handled by **DispatcherServlet**. |
| **Access** | `ServletRequest`, `ServletResponse`. | `HttpServletRequest`, `HttpServletResponse`, plus **Handler** (Controller bean) and **ModelAndView**. |
| **Dependency Injection** | Harder (historically), now easier in Boot. | Native Spring Bean (Easy DI). |

---

## 248. How does Spring handle CORS?

**Answer:**
**CORS (Cross-Origin Resource Sharing)** is handled via:
1.  **@CrossOrigin:** Annotation on Controller class or method.
    *   `@CrossOrigin(origins = "http://localhost:3000")`
2.  **Global Configuration:** Override `addCorsMappings` in `WebMvcConfigurer`.
    *   `registry.addMapping("/api/**").allowedOrigins("*")`

---

## 249. How to handle file upload?

**Answer:**
Use `MultipartFile` to handle uploaded files.
*   **Configuration:** `spring.servlet.multipart.max-file-size` (default 1MB).
*   **Controller:**
    ```java
    @PostMapping("/upload")
    public void upload(@RequestParam("file") MultipartFile file) {
        // file.getInputStream() or file.transferTo(dest)
    }
    ```

---

## 250. What is view resolver?

**Answer:**
**ViewResolver** translates a logical view name (returned by Controller) into a physical view resource.
*   **Example:** Returns "home" -> Resolves to `/WEB-INF/templates/home.html` (Thymeleaf) or `/WEB-INF/jsp/home.jsp` (InternalResourceViewResolver).
*   **Chain:** You can chain multiple resolvers (e.g., check for explicit bean name first, then JSP).
