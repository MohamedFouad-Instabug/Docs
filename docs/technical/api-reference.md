# API Reference

Below are the main API endpoints for **test-docs-workflow**.

## Endpoints

### `GET /api/items`
- **Description:** Retrieve a list of items.
- **Response Example:**
  ```json
  [
    { "id": 1, "name": "Item 1" },
    { "id": 2, "name": "Item 2" }
  ]
  ```

### `POST /api/items`
- **Description:** Create a new item.
- **Request Example:**
  ```json
  { "name": "New Item" }
  ```
- **Response Example:**
  ```json
  { "id": 3, "name": "New Item" }
  ``` 