# Restaurant Menu API - Postman Documentation Guide

## Overview
This guide explains how to use the Postman collection to test, document, and publish API documentation for the Restaurant Menu API.

## Files Provided
- `postman_collection_complete.json` - Complete collection with endpoints, descriptions, and example responses

## Steps to Import & Test in Postman

### 1. Import the Collection
1. Open Postman
2. Click **Collections** (left sidebar)
3. Click **Import** button
4. Choose **Upload Files** tab
5. Select `postman_collection_complete.json`
6. Click **Import**

### 2. Configure Environment Variables
1. Ensure the collection variables are set:
   - `baseUrl` = `http://localhost:3000`
   - `itemId` = `1` (or any valid menu item ID)

### 3. Run Requests & Save Examples
Follow this workflow for each endpoint:

#### Getting All Menu Items
1. In the collection, open **GET Endpoints** → **Get All Menu Items**
2. Click **Send** to test the endpoint
3. Right side shows the response
4. Click **Save Response** → **Save as example**
5. The example "Successful GET - All menu items" will be populated

#### Getting Menu Item by ID
1. Open **GET Endpoints** → **Get Menu Item by ID**
2. Click **Send** (tests with itemId variable)
3. Click **Save Response** → **Save as example**
4. Test 404 case by changing `{{itemId}}` to `999` in the URL
5. Click **Send** and **Save Response** → **Save as example** with name "Error 404 - Menu item not found"

#### Creating a Menu Item (POST)
1. Open **POST Endpoint** → **Create Menu Item**
2. Modify the request body if desired
3. Click **Send**
4. You'll get a 201 response with auto-generated `id`
5. Click **Save Response** → **Save as example** as "Successful POST - Create menu item"
6. Test validation error by clearing the `name` field
7. Click **Send** and **Save Response** with name "Error 400 - Validation error (missing name)"
8. Test invalid price by setting `"price": "invalid"`
9. Click **Send** and **Save Response** with name "Error 400 - Validation error (invalid price)"

#### Updating a Menu Item (PUT)
1. Open **PUT Endpoint** → **Update Menu Item**
2. Click **Send** to test update
3. Click **Save Response** → **Save as example**
4. Test 404 by changing `{{itemId}}` to `999`
5. Click **Send** and **Save Response** with name "Error 404 - Menu item not found"
6. Test validation error by setting `"price": "invalid"`
7. Click **Send** and **Save Response** with name "Error 400 - Validation error (invalid price)"

#### Deleting a Menu Item (DELETE)
1. Open **DELETE Endpoint** → **Delete Menu Item**
2. Click **Send** to delete
3. Click **Save Response** → **Save as example**
4. Test 404 by changing `{{itemId}}` to `999`
5. Click **Send** and **Save Response** with name "Error 404 - Menu item not found"

## Generate & Publish Documentation

### View Documentation
1. In Postman, right-click on the collection name
2. Select **View Documentation**
3. A web page opens with:
   - All endpoints listed
   - Request/response examples
   - Descriptions and parameters

### Publish Documentation (Public Website)
1. In the documentation view, click **Publish** (top right)
2. Choose:
   - **Published Collection** workspace
   - Custom domain (optional)
   - Authentication level (Public/Private)
3. Click **Publish Collection**
4. Postman generates a public URL like: `https://documenter.postman.com/view/xxxxx/yyyy/zzz`
5. Share this URL with your team or stakeholders

## What's in the Collection

### Endpoint Descriptions
Each endpoint includes:
- **What it does** (use case)
- **Parameters** (path, query, body)
- **Validation rules**
- **Success & error responses**

### Example Responses Included
✅ **Success Examples:**
- GET /api/menu → 200 (all items)
- GET /api/menu/:id → 200 (single item)
- POST /api/menu → 201 (created item)
- PUT /api/menu/:id → 200 (updated item)
- DELETE /api/menu/:id → 200 (deleted message)

❌ **Error Examples:**
- GET /api/menu/999 → 404 (not found)
- POST /api/menu → 400 (missing name)
- POST /api/menu → 400 (invalid price)
- PUT /api/menu/:id → 400 (invalid price)
- PUT /api/menu/999 → 404 (not found)
- DELETE /api/menu/999 → 404 (not found)

## API Endpoints Summary

| Method | Endpoint | Status | Description |
|--------|----------|--------|-------------|
| GET | `/api/menu` | 200 | Get all menu items |
| GET | `/api/menu/:id` | 200/404 | Get menu item by ID |
| POST | `/api/menu` | 201/400 | Create new menu item |
| PUT | `/api/menu/:id` | 200/400/404 | Update menu item |
| DELETE | `/api/menu/:id` | 200/404 | Delete menu item |

## Request/Response Format

### Request Body (POST/PUT)
```json
{
  "name": "string (required for POST)",
  "description": "string (optional)",
  "price": "number (required for POST, must be > 0)",
  "category": "string (optional)",
  "ingredients": ["string array (optional)"],
  "available": "boolean (optional, default: true)"
}
```

### Success Response
```json
{
  "id": 1,
  "name": "Menu Item Name",
  "description": "Description",
  "price": 12.99,
  "category": "entree",
  "ingredients": ["ingredient1", "ingredient2"],
  "available": true
}
```

### Error Response (400)
```json
{
  "errors": [
    {
      "type": "field",
      "msg": "Error message",
      "path": "field_name",
      "location": "body"
    }
  ]
}
```

### Error Response (404)
```json
{
  "error": "Menu item not found"
}
```

## Tips for Best Documentation

1. **Keep Descriptions Clear** - Use markdown formatting in endpoint descriptions
2. **Provide Real Examples** - Save actual responses from your running server
3. **Test All Paths** - Include both success and error scenarios
4. **Use Readable Names** - Name examples descriptively (e.g., "Error 404 - Menu item not found")
5. **Document Edge Cases** - Include validation errors and not found cases
6. **Set Default Variables** - Use collection variables for baseUrl and itemId
7. **Add Comments** - In the request body, explain what each field does

## Sharing Your Documentation

**Public Link Format:**
```
https://documenter.postman.com/view/{workspace-id}/{collection-id}/{version-id}
```

You can:
- Share link in emails
- Embed in your website
- Include in README files
- Share with API consumers

## Server Requirements
- Server must be running on `http://localhost:3000`
- All endpoints must be accessible
- Request logging will be visible in server console
