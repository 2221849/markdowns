# Systems Integration

## Enabling Internet Information Services in Windows Features

1. **Access the Start Menu**: Click the **Start** button or press the **Windows key**.
2. **Search for "Windows Features"**: Type **"Windows Features"** into the search field.
3. **Choose "Turn Windows features on or off"**: From the search results, click on **"Turn Windows features on or off"**.
4. **Enable Internet Information Services (IIS)**

## Building a RESTful Web Service with ASP.NET Web API

In this section, we will create a simple ASP.NET Web API project called "ProductsAPI" that returns a list of products.

### Steps to Create a RESTful Web Service (ASP.NET Web API)

#### 1. **Start a New ASP.NET Web API Project**

1. Launch **Visual Studio**.
2. Go to **File** -> **New** -> **Project**.
3. In the dialog, select **ASP.NET Web Application (.NET Framework)**.
   - **Project name**: `ProductsAPI`.
   - **Solution name**: `ProductsAPI`.
4. Click **OK**.

5. In the template selection window, choose **Empty Template**.
   - Only select **Web API** (deselect MVC, WebForms, etc.).
   - Click **OK** to create the project.

#### 2. **Add a Product Model**

1. In **Solution Explorer**, right-click the project or a `Models` folder (for better organization).
2. Select **Add** -> **Class**.
   - **Class name**: `Product`.
   - Click **Add**.

3. Insert the following code into `Product.cs`:

```csharp
namespace ProductsApp.Models
{
    public class Product
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string Category { get; set; }
        public decimal Price { get; set; }
    }
}
```

This `Product` class represents the product data that will be returned from the API.

#### 3. **Create a Web API Controller**

1. Right-click the **Controllers** folder in **Solution Explorer** (create this folder if it doesn’t exist).
2. Select **Add** -> **Controller**.
3. Choose **Web API 2 Controller - Empty**.
   - **Name the controller**: `ProductsController`.
   - Click **Add**.

#### 4. **Update ProductsController with the Code Below**

Replace the contents of `ProductsController.cs` with the following:

```csharp
using ProductsApp.Models;
using System.Collections.Generic;
using System.Linq;
using System.Web.Http;

namespace ProductsAPI.Controllers
{
    public class ProductsController : ApiController
    {
        // Sample product data, typically this would come from a database
        List<Product> products = new List<Product>
        {
            new Product { Id = 1, Name = "Tomato Soup", Category = "Groceries", Price = 1 },
            new Product { Id = 2, Name = "Yo-yo", Category = "Toys", Price = 3.75M },
            new Product { Id = 3, Name = "Hammer", Category = "Hardware", Price = 16.99M }
        };

        // GET: api/products
        public IEnumerable<Product> GetAllProducts()
        {
            return products;
        }

        // GET: api/products/{id}
        public IHttpActionResult GetProduct(int id)
        {
            var product = products.FirstOrDefault(p => p.Id == id);
            if (product == null)
            {
                return NotFound();
            }
            return Ok(product);
        }
    }
}
```

- The `GetAllProducts()` method returns all products at the `/api/products` endpoint.
- The `GetProduct(int id)` method returns a specific product by its ID at `/api/products/{id}`.

#### 5. **Configure Routing**

Web API uses routing to map requests to controller actions.

1. Open `WebApiConfig.cs` in the `App_Start` folder.

2. Ensure the route configuration looks like this:

```csharp
public static class WebApiConfig
{
    public static void Register(HttpConfiguration config)
    {
        // Web API routes
        config.MapHttpAttributeRoutes();

        config.Routes.MapHttpRoute(
            name: "DefaultApi",
            routeTemplate: "api/{controller}/{id}",
            defaults: new { id = RouteParameter.Optional }
        );
    }
}
```

This routing setup ensures URLs like `/api/products` and `/api/products/1` will work correctly with the controller.

#### 6. **Register the Route in Global.asax.cs**

Ensure the `WebApiConfig` is registered in `Global.asax.cs` inside the `Application_Start()` method:

```csharp
protected void Application_Start()
{
    GlobalConfiguration.Configure(WebApiConfig.Register);
}
```

#### 7. **Run the Web API**

1. Press **F5** to launch the project.

   If you encounter an error like `HTTP Error 403.14 – Forbidden`, this is due to a lack of a default page (like HTML or ASPX), but the API endpoints are still accessible.

2. To test, add `/api/products` to the URL in your browser.
   - Example: `http://localhost:port_number/api/products`
   - You should see a JSON response with the list of products.

3. To retrieve a product by ID, append the product ID to the URL.
   - Example: `http://localhost:port_number/api/products/1`

This will return details for the product with ID 1.

#### Testing the API Endpoints

1. **Get All Products:**

   Use the following URL:

   ```text
   GET: http://localhost:port_number/api/products
   ```

   Response:

   ```json
   [
       { "Id": 1, "Name": "Tomato Soup", "Category": "Groceries", "Price": 1 },
       { "Id": 2, "Name": "Yo-yo", "Category": "Toys", "Price": 3.75 },
       { "Id": 3, "Name": "Hammer", "Category": "Hardware", "Price": 16.99 }
   ]
   ```

2. **Get Product by ID:**

   Use this URL:

   ```text
   GET: http://localhost:port_number/api/products/1
   ```

   Response:

   ```json
   { "Id": 1, "Name": "Tomato Soup", "Category": "Groceries", "Price": 1 }
   ```

If the product isn't found, you will receive a `404 Not Found` error.

#### Conclusion

By following these instructions, you have built a basic ASP.NET RESTful Web API that serves a list of products. You can expand this further by connecting to a database or implementing additional CRUD operations like `POST`, `PUT`, and `DELETE`.

### Create a Simple JavaScript Client

Next, let's interact with the Web API using jQuery in JavaScript:

1. Right-click on the project, go to **Add**, and select **New Item**. Under **C# | Web**, choose **HTML Page** and name it `index.html`.
2. Replace the content of the HTML page with the following code (source: [www.asp.net]):

```html
<!DOCTYPE html>
<html>
<head>
    <title>RESTful Web Service - Products App</title>
    <meta charset="utf-8" />
</head>
<body>
    <div>
        <h2>All Products</h2>
        <ul id="products"></ul>
    </div>
    <div>
        <h2>Search by ID</h2>
        <input type="text" id="prodId" size="5" />
        <input type="button" value="Search" onclick="find();" />
        <p id="product"></p>
    </div>

    <!-- jQuery -->
    <script src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js"></script>

    <script>
        // Update this URL to the actual running URL of your API
        var uri = 'http://localhost:63927/api/products';

        // Function to fetch and display all products
        $(document).ready(function () {
            $.get(uri)
                .done(function (data) {
                    // Loop through the list of products
                    $.each(data, function (key, item) {
                        // Append each product to the list
                        $('<li>', { text: formatItem(item) }).appendTo($('#products'));
                    });
                })
                .fail(function (jqxhr, textStatus, error) {
                    alert("Request failed: " + textStatus + ", " + error);
                });
        });

        // Format product details
        function formatItem(item) {
            return item.Name + ": " + item.Price + "€";
        }

        // Fetch a product by its ID
        function find() {
            var id = $('#prodId').val();
            $.getJSON(uri + '/' + id)
                .done(function (data) {
                    $('#product').text(formatItem(data));
                })
                .fail(function (jqxhr, textStatus, error) {
                    alert("Request failed: " + textStatus + ", " + error);
                });
        }
    </script>
</body>
</html>
```

Now, re-run the Web API application. The `index.html` page will load, allowing you to retrieve products using the form.

### Adding Additional GET Routes for Product Categories

Extend the `ProductsController` to include a new action that allows users to request all products from a specific category by using the route `/api/products/{category}`.

### 1. **Implementing the GET Action for Category Filtering**

To implement category-based filtering, modify the `ProductsController` to include a new route and action for filtering products by category. We will use ASP.NET Web API routing for this feature.

1. Open `ProductsController.cs`.
2. Add the following `GetProductByCategory` method:

```csharp
using ProductsApp.Models;
using System.Collections.Generic;
using System.Linq;
using System.Web.Http;

namespace ProductsAPI.Controllers
{
    public class ProductsController : ApiController
    {
        // Sample product data
        List<Product> products = new List<Product>
        {
            new Product { Id = 1, Name = "Tomato Soup", Category = "Groceries", Price = 1 },
            new Product { Id = 2, Name = "Yo-yo", Category = "Toys", Price = 3.75M },
            new Product { Id = 3, Name = "Hammer", Category = "Hardware", Price = 16.99M }
        };

        // GET: api/products/{id:int}
        [Route("api/products/{id:int}")]
        public IHttpActionResult GetProduct(int id)
        {
            var product = products.FirstOrDefault(p => p.Id == id);
            if (product == null)
            {
                return NotFound();
            }
            return Ok(product);
        }

        // GET: api/products/{category}
        [Route("api/products/{category}")]
        public IEnumerable<Product> GetProductByCategory(string category)
        {
            var productsInCategory = products.Where(p => p.Category == category).ToList();
            return productsInCategory.Any() ? productsInCategory : new List<Product>();
        }

        // GET: api/products
        public IEnumerable<Product> GetAllProducts()
        {
            return products;
        }
    }
}
```

In this updated `ProductsController`, you can simplify routing by adding a class-level route prefix. For example, applying `[RoutePrefix("api/products")]` would allow you to shorten route definitions in the methods. Instead of writing `[Route("api/products/{id:int})]`, you can use `[Route("{id:int}")]` as the base path is handled by the prefix. This makes the routes cleaner and more concise. The `GetAllProducts()` method remains unchanged, responding to a simple GET request to `/api/products`.

**Explanation of the Code:**

1. **`GetProductByCategory` Method:**
   - This action accepts a `category` parameter from the URL and filters the products based on the provided category.
   - It uses LINQ's `Where` method to find products that match the category.
   - If no products are found, an empty list is returned.

2. **Routing:**
   - The `[Route("api/products/{category}")]` matches requests such as `/api/products/Toys` or `/api/products/Groceries`.
   - The `[Route("api/products/{id:int}")]` ensures that when an integer `id` is provided, the correct product is retrieved.

#### Example Test URLs

1. **Fetch Products by Category:**

   ```text
   GET: http://localhost:port_number/api/products/Toys
   ```

   Response if the category exists:

   ```json
   [
       { "Id": 2, "Name": "Yo-yo", "Category": "Toys", "Price": 3.75 }
   ]
   ```

   If no products are found for the category, the response will be:

   ```json
   []
   ```

2. **Fetch Product by ID:**

   ```text
   GET: http://localhost:port_number/api/products/1
   ```

   Expected JSON response:

   ```json
   { "Id": 1, "Name": "Tomato Soup", "Category": "Groceries", "Price": 1 }
   ```

## RESTful API with SQL Server Database Integration

This section outlines the process of creating a new ASP.NET Web API project that establishes a connection to a SQL Server database for data persistence, along with implementing CRUD operations through a controller.

### 1. **Set Up a New WebAPI Project**

- In Visual Studio:
  - Navigate to **File > New > Project**.
  - Choose **ASP.NET Web Application** (.NET Framework).
  - Name the project `ProductsDatabaseAPI`.
  - Select the **Web API** template.
  - Before clicking Create, click the checkbox labeled Configure for HTTPS to unselect it (this will disable HTTPS).
  - Then, click Create to set up the project.

### 2. **Add a SQL Server Database to the Project**

- In **Solution Explorer**, right-click the **App_Data** folder and choose **Add > New Item**.
- Select **SQL Server Database** and name it `DBProds.mdf`.
- In **Server Explorer**, right-click the new database and click **Open**.
- Create a `Prods` table using this SQL script:

```sql
CREATE TABLE [dbo].[Prods] (
    Id INT IDENTITY (1, 1) NOT NULL PRIMARY KEY,
    Name NVARCHAR(50) NOT NULL,
    Category NVARCHAR(50) NULL,
    Price DECIMAL(18, 2) NULL
);
```

### 3. **Configure the Connection String**

- Open the `Web.config` file.
- Inside the `<connectionStrings>` section, add the connection string using `|DataDirectory|` to refer to the database location:

```xml
<configuration>
  . . .
  <connectionStrings>
    <add name="ConnStr"
         connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\DBProds.mdf;Integrated Security=True"
         providerName="System.Data.SqlClient" />
  </connectionStrings>
</configuration>
```

- This configuration allows your application to connect to the SQL Server database.

### 4. **Define the Product Model**

- In the **Models** folder, create a `Product.cs` file to define the product structure:

```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Category { get; set; }
    public decimal Price { get; set; }
}
```

### 5. **Build the ProductsController**

- In the **Controllers** folder, create a `ProductsController.cs` file.
- Import the required namespaces:

```csharp
using System.Collections.Generic;
using System.Data.SqlClient;
using System.Web.Http;
using ProductsDatabaseAPI.Models;
```

#### 5.1. **Implement GET Operations**

- **Retrieve All Products**:

```csharp
[Route("api/products")]
public IEnumerable<Product> GetAllProducts()
{
    List<Product> products = new List<Product>();
    string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["ConnStr"].ConnectionString;

    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        SqlCommand cmd = new SqlCommand("SELECT * FROM Prods", conn);
        conn.Open();
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Product product = new Product
            {
                Id = (int)reader["Id"],
                Name = reader["Name"].ToString(),
                Category = reader["Category"].ToString(),
                Price = (decimal)reader["Price"]
            };
            products.Add(product);
        }
    }

    return products;
}
```

- **Retrieve Product by ID**:

```csharp
[Route("api/products/{id:int}")]
public IHttpActionResult GetProduct(int id)
{
    Product product = null;
    string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["ConnStr"].ConnectionString;

    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        SqlCommand cmd = new SqlCommand("SELECT * FROM Prods WHERE Id = @Id", conn);
        cmd.Parameters.AddWithValue("@Id", id);
        conn.Open();
        SqlDataReader reader = cmd.ExecuteReader();
        if (reader.Read())
        {
            product = new Product
            {
                Id = (int)reader["Id"],
                Name = reader["Name"].ToString(),
                Category = reader["Category"].ToString(),
                Price = (decimal)reader["Price"]
            };
        }
    }

    if (product == null)
    {
        return NotFound();
    }

    return Ok(product);
}
```

#### 5.2. **Add POST Operation**

```csharp
[Route("api/products")]
public IHttpActionResult PostProduct([FromBody] Product product)
{
    if (!ModelState.IsValid)
        return BadRequest(ModelState);

    string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["ConnStr"].ConnectionString;

    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        SqlCommand cmd = new SqlCommand("INSERT INTO Prods (Name, Category, Price) VALUES (@Name, @Category, @Price)", conn);
        cmd.Parameters.AddWithValue("@Name", product.Name);
        cmd.Parameters.AddWithValue("@Category", product.Category);
        cmd.Parameters.AddWithValue("@Price", product.Price);

        conn.Open();
        cmd.ExecuteNonQuery();
    }

    return CreatedAtRoute("DefaultApi", new { id = product.Id }, product);
}
```

#### 5.3. **Add PUT Operation**

```csharp
[Route("api/products/{id:int}")]
public IHttpActionResult PutProduct(int id, [FromBody] Product product)
{
    if (!ModelState.IsValid)
        return BadRequest(ModelState);

    string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["ConnStr"].ConnectionString;

    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        SqlCommand cmd = new SqlCommand("UPDATE Prods SET Name = @Name, Category = @Category, Price = @Price WHERE Id = @Id", conn);
        cmd.Parameters.AddWithValue("@Name", product.Name);
        cmd.Parameters.AddWithValue("@Category", product.Category);
        cmd.Parameters.AddWithValue("@Price", product.Price);
        cmd.Parameters.AddWithValue("@Id", id);

        conn.Open();
        int rowsAffected = cmd.ExecuteNonQuery();
        if (rowsAffected == 0)
        {
            return NotFound();
        }
    }

    return StatusCode(System.Net.HttpStatusCode.NoContent);
}
```

#### 5.4. **Add DELETE Operation**

```csharp
[Route("api/products/{id:int}")]
public IHttpActionResult DeleteProduct(int id)
{
    string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["ConnStr"].ConnectionString;

    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        SqlCommand cmd = new SqlCommand("DELETE FROM Prods WHERE Id = @Id", conn);
        cmd.Parameters.AddWithValue("@Id", id);

        conn.Open();
        int rowsAffected = cmd.ExecuteNonQuery();
        if (rowsAffected == 0)
        {
            return NotFound();
        }
    }

    return StatusCode(System.Net.HttpStatusCode.NoContent);
}
```

### 6. **Test the API**

- Test the API using **Postman**.
- Test all HTTP methods (GET, POST, PUT, DELETE) to verify the functionality.

For instance, to **POST** a new product:

```json
{
  "Name": "Product 1",
  "Category": "Category 1",
  "Price": 12.99
}
```

## Swagger

Swagger is an open-source framework that simplifies API development and documentation. It provides a user-friendly interface for interacting with APIs, allowing developers and users to explore available endpoints, request parameters, and response formats. With Swagger, you can easily visualize and test your API, enhancing the overall developer experience by making it more accessible and understandable.

### Installing Swashbuckle via NuGet

- Right-click on your project in **Solution Explorer** and choose **Manage NuGet Packages**.
- In the **Browse** tab, look for **Swashbuckle**.
- Click on **Swashbuckle** and then select **Install**.

### Running Your Project and Accessing Swagger UI

1. **Start the Project**:
   - Press `F5` to begin debugging your application, which will launch your Web API.

2. **Open Swagger UI**:
   - In your web browser, go to `http://localhost:<your-port>/swagger` (make sure to replace `<your-port>` with the actual port number your application is using).
   - The Swagger UI will load, showing your API documentation.

### Final Testing

1. **Check Documentation**:
   - Refresh the Swagger UI page (`http://localhost:<your-port>/swagger`) and ensure that your API methods appear with their corresponding descriptions from the XML comments.

2. **Test the API**:
   - From the Swagger UI, you can directly interact with your API by clicking on the endpoints and experimenting with sample inputs.
