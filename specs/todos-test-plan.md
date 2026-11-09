# Todos API documentation UI test plan

## Application Overview

Explore the user-facing interface at https://dummyjson.com/docs/todos. This is an API documentation page, not an interactive todo manager: it exposes navigable endpoint examples and Show Output controls. The page explicitly says POST, PUT/PATCH, and DELETE operations are simulated and do not persist changes to server data. Each scenario starts from a fresh navigation to the documentation URL, uses its section navigation, and verifies the documented request, response shape, and relevant explanatory copy. Avoid assertions on sample IDs or data values that may vary.

## Test Scenarios

### 1. Todos core user operations

**Seed:** `tests/seed.spec.ts`

#### 1.1. Browse the todo collection and pagination options

**File:** `tests/todos/browse-todos.spec.ts`

**Steps:**
  1. Navigate to https://dummyjson.com/docs/todos and select the Get all todos section from the Todos navigation.
    - expect: The browser reaches the todos-all section on the documentation page.
    - expect: The example shows the GET request to /todos.
  2. Review the collection description and pagination link.
    - expect: The documentation says the default response contains 30 items.
    - expect: The Limit and skip link is present and navigates to the pagination section.
  3. Review the sample collection response and its output control.
    - expect: The response example shows a todos array and total, skip, and limit fields.
    - expect: Initially the control is Show Output; selecting it reveals the sample response and changes its label to Hide Output.
    - expect: Selecting Hide Output hides the sample response and restores the Show Output label.
  4. Open the Limit and skip section using its link.
    - expect: The section explains using limit and skip for pagination and documents limit=0 for requesting all items.

#### 1.2. Read a todo or filter todos by user

**File:** `tests/todos/read-todo.spec.ts`

**Steps:**
  1. Navigate directly to the documentation URL, then select Get a single todo from the Todos navigation.
    - expect: The single-item section is reached and shows the GET request to /todos/1.
  2. Review and reveal the single-todo response example.
    - expect: The response example contains id, todo, completed, and userId fields.
    - expect: The Show Output control reveals the sample response and can be toggled back to Hide Output.
  3. Select Get all todos by user id and review its request and response example.
    - expect: The section shows the GET request to /todos/user/5.
    - expect: The response example is a collection with todos, total, skip, and limit fields.

#### 1.3. Review adding a todo

**File:** `tests/todos/add-todo.spec.ts`

**Steps:**
  1. Navigate directly to the documentation URL, then select Add a new todo.
    - expect: The section presents a POST request to /todos/add with a JSON payload containing todo, completed, and userId.
  2. Check the add-operation explanation and reveal its output.
    - expect: The documentation explicitly says adding a todo is simulated and will not add it to the server.
    - expect: Show Output reveals a sample response with an id and the submitted todo fields; Hide Output closes it again.

#### 1.4. Review updating a todo

**File:** `tests/todos/update-todo.spec.ts`

**Steps:**
  1. Navigate directly to the documentation URL, then select Update a todo.
    - expect: The section presents a request to /todos/1 using PUT or PATCH and a JSON payload that updates completed.
  2. Check the update-operation explanation and reveal its output.
    - expect: The documentation explicitly says updating a todo is simulated and will not update server data.
    - expect: Show Output reveals a response with the todo fields and the modified completed value; Hide Output closes it again.

#### 1.5. Review deleting a todo

**File:** `tests/todos/delete-todo.spec.ts`

**Steps:**
  1. Navigate directly to the documentation URL, then select Delete a todo.
    - expect: The section presents a DELETE request to /todos/1.
  2. Check the delete-operation explanation and reveal its output.
    - expect: The documentation explicitly says deletion is simulated and does not delete server data.
    - expect: Show Output reveals a response containing isDeleted and deletedOn; Hide Output closes it again.
