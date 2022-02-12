# Blazor
Blazor apps are composed of reusable web UI components built using C#, HTML, and CSS. You can use Blazor to generate Server-side code that handles UI interactions over a WebSocket connection and also client-side web app that runs directly in the browser via WebAssembly.

## WebAssembly
WebAssembly (WASM) is an open binary standard. It defines a portable code format for programs designed to run in web browsers. It's designed to run alongside JavaScript so that both work together. 

## Blazor WebAssembly
With Blazor WebAssembly, developers can run .NET code in a browser. .NET code executed via WebAssembly in a browser runs in the browser's JavaScript sandbox. The code includes all the security and protection that the sandbox provides. A Blazor WebAssembly app is restricted to the capabilities of the browser that executes the app. But the app can access full browser functionality via JavaScript interop.

## Blazor Server
Blazor Server provides support for hosting Razor components on the server in an ASP.NET Core app. UI updates are handled over a SignalR connection. The connection used by Blazor Server to communicate with the browser is also used to handle JavaScript interop calls.


# Demo Application Setup

check for dotnet sdks
```
dotnet --list-sdks
```
Install .net sdk 6 [Download](https://dotnet.microsoft.com/en-us/download)

1. Create a folder name BlazorDemo
2. Open folder in Visual Studio Code
3. In the terminal run the below command
    ```
    dotnet new blazorserver -f net6.0
    ```
    this creates a basic Blazor server project.
4. Run the app with the below command in terminal
    ```
    dotnet watch run
    ```    
    this will build and start the app

## Razor
Razor is a markup syntax that uses HTML and C# for writing UI components of Blazor web apps.

## Razor components
A Razor file defines components that make up a portion of the app UI. Components in Blazor are analogous to user controls in ASP.NET Web Forms. At compile time, each Razor component is built into a .NET class. The class includes common UI elements like state, rendering logic, lifecycle methods, and event handlers.

1. Run the application and try the counter typing /counter in the browser
2. Add Counter component to the index page Index.razor and see the change in the browser
    ```
    <Counter />
    ```
3. Modify the component
    a. Add a public property for IncrementAmount with a [Parameter] attribute.
    b. Change the IncrementCount method to use the IncrementAmount when incrementing the value of currentCount.
    ```
    @page "/counter"

    <h1>Counter</h1>

    <p role="status">Current count: @currentCount</p>

    <button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

    @code {
        private int currentCount = 0;

        [Parameter]
        public int IncrementAmount { get; set; } = 1;

        private void IncrementCount()
        {
            currentCount += IncrementAmount;
        }
    }
    ```
 4. In the Index.razor update the <Counter> element to add an IncrementAmount attribute   
    ```
    <Counter IncrementAmount="10" />
    ```

## Razor directives
Razor directives are component markup used to add C# inline with HTML. With directives, developers can define single statements, methods, or larger code blocks.

### Code 
1. @expression() to add a C# statement inline with HTML.
2. @code directive to add multiple statements enclosed by parentheses.
3. @functions section to the template for methods and properties. They're added to the top of the generated class, where the document can reference them.

### Page
The @Page directive is special markup that identifies a component as a page. Use this directive to specify a route.

## Data Binding and Events
1. Create a TodoItem class named TodoItem.cs in the root.
    ```
    public class TodoItem
    {
        public string? Title { get; set; }
        public bool IsDone { get; set; }
    }
    ```
2. Create the ToDo page with the following command
    ```
    dotnet new razorcomponent -n Todo -o Pages
    ```
3. copy the below code into Todo.razor
    ```
    @page "/todo"

    <h3>Todo (@todos.Count(todo => !todo.IsDone))</h3>

    <ul>
        @foreach (var todo in todos)
        {
            <li>
                <input type="checkbox" @bind="todo.IsDone" />
                <input @bind="todo.Title" />
            </li>
        
        }
    </ul>

    <input placeholder="Something todo" @bind="newTodo" />
    <button @onclick="AddTodo">Add todo</button>

    @code {
        private List<TodoItem> todos = new();
        private string? newTodo;

        private void AddTodo()
        {
            if (!string.IsNullOrWhiteSpace(newTodo))
            {
                todos.Add(new TodoItem { Title = newTodo });
                newTodo = string.Empty;
            }
        }
    }
    ```
4. Create a link in the navigation In Shared/NavMenu.razor file
    ```
    <div class="nav-item px-3">
            <NavLink class="nav-link" href="todo">
                <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
            </NavLink>
    </div>
    ```
