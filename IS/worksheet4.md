# Systems Integration

## Part 1 – XML Structure and XML Schemas

Based on the XML example shown below:

```xml
<?xml version="1.0" encoding="utf-8"?>
<bookstore>
  <book category="CHILDREN">
    <title>Charlottes Web</title>
    <author>E.B. White</author>
    <year>1952</year>
    <price>12.60</price>
  </book>
  <book category="WEB">
    <title>Beginning XML</title>
    <author>Joe Fawcett</author>
    <year>2012</year>
    <price>31.30</price>
    <rate>4</rate>
  </book>
  <book category="WEB">
    <title>Programming .NET Web Services</title>
    <author>Alex Ferrara</author>
    <year>2002</year>
    <price>38.36</price>
    <rate>3</rate>
  </book>
</bookstore>
```

### 1. Existing Elements and Attributes

In the given XML example, the existing elements and attributes are:

- **Elements:**
  - `<bookstore>`: The root element that contains all books.
  - `<book>`: Represents each book in the bookstore.
  - `<title>`: The title of the book.
  - `<author>`: The author of the book.
  - `<year>`: The publication year of the book.
  - `<price>`: The price of the book.
  - `<rate>` (optional): The rating of the book (only present in some books).

- **Attributes:**
  - `category` (in `<book>`): Specifies the category of the book (e.g., "CHILDREN" or "WEB").

### 2. Changes to the XML Structure

#### 2.1. Identify the Book Publisher

To add information about the book publisher, a new `<publisher>` element can be included inside the `<book>` element. This could look like:

```xml
<book category="CHILDREN">
    <title>Charlotte's Web</title>
    <author>E.B. White</author>
    <year>1952</year>
    <price>12.60</price>
    <publisher>Harper and Brothers</publisher>
</book>
```

This structure introduces a `<publisher>` element to store the publisher's name.

#### 2.2. Allow a Book to Have Several Authors

To accommodate multiple authors for a book, the `<author>` element can be repeated or wrapped within an `<authors>` container element to better organize them. Here’s how it could be implemented:

```xml
<book category="WEB">
    <title>Programming .NET Web Services</title>
    <authors>
        <author>Alex Ferrara</author>
        <author>Matthew MacDonald</author>
    </authors>
    <year>2002</year>
    <price>38.36</price>
    <rate>3</rate>
    <publisher>O'Reilly Media</publisher>
</book>
```

In this version:

- The `<authors>` container element groups multiple `<author>` elements.
- This allows the XML structure to clearly represent books that have multiple authors.

### Revised XML Example

Here’s a revised XML example incorporating both changes:

```xml
<?xml version="1.0" encoding="utf-8"?>
<bookstore>
    <book category="CHILDREN">
        <title>Charlotte's Web</title>
        <authors>
            <author>E.B. White</author>
        </authors>
        <year>1952</year>
        <price>12.60</price>
        <publisher>Harper & Brothers</publisher>
    </book>
    <book category="WEB">
        <title>Beginning XML</title>
        <authors>
            <author>Joe Fawcett</author>
        </authors>
        <year>2012</year>
        <price>31.30</price>
        <rate>4</rate>
        <publisher>Apress</publisher>
    </book>
    <book category="WEB">
        <title>Programming .NET Web Services</title>
        <authors>
            <author>Alex Ferrara</author>
            <author>Matthew MacDonald</author>
        </authors>
        <year>2002</year>
        <price>38.36</price>
        <rate>3</rate>
        <publisher>O'Reilly Media</publisher>
    </book>
</bookstore>
```

### What is an XML Schema (.xsd file)?

An XML Schema, defined using the XML Schema Definition (XSD) language, is a way to describe the structure, content, and data types of XML documents. It provides a formal blueprint that defines how an XML document should be structured. By specifying element types, attributes, and their relationships, an XSD ensures the validity and consistency of XML documents used within an application or across integrated systems.

XML Schemas enable developers to define:

- **Elements**: The building blocks of an XML document, including their names and data types.
- **Attributes**: Characteristics or properties associated with elements.
- **Complex Types**: Structured types composed of multiple elements and attributes.
- **Simple Types**: Data types that contain text content, such as strings, integers, or dates.
- **Constraints**: Rules for element occurrences, value restrictions, and relationships.

### Structure of an XML Schema

The root element in an XML Schema file is `<xs:schema>`, which contains definitions for the elements and types used in an XML document. The `xs` prefix indicates the namespace for XML Schema elements, where "xs" stands for "XML Schema."

#### Example of Basic XML Schema Syntax

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="name" type="xs:string"/>
    <xs:attribute name="language" type="xs:string"/>
</xs:schema>
```

- `<xs:element>` defines an element in the XML document, specifying its name and data type.
- `<xs:attribute>` defines an attribute, also specifying a name and type.

### Defining Complex Types

Complex types in an XML Schema are used to describe elements that contain other elements, attributes, or a mixture of text and other content. There are four types of complex elements:

1. **Empty Elements**: Contain no content.
2. **Elements Containing Other Elements Only**: Used to create structured data.
3. **Elements Containing Only Text**: Have a text value but can include attributes.
4. **Elements Containing Both Other Elements and Text**: Mix of text and sub-elements.

### Examples of Complex Types

#### Example 1: Defining a Complex Type Directly

The XML example below represents an `<employee>` element with child elements `<firstname>` and `<lastname>`:

```xml
<employee>
    <firstname>John</firstname>
    <lastname>Smith</lastname>
</employee>
```

The corresponding XML Schema (XSD) definition is:

```xml
<xs:element name="employee">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="firstname" type="xs:string"/>
            <xs:element name="lastname" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

In this example:

- `<xs:complexType>` defines a structured type containing multiple elements.
- `<xs:sequence>` indicates that the child elements must appear in the specified order.

#### Example 2: Using Named Complex Types

A named complex type allows for the definition of reusable structures:

```xml
<xs:element name="employee" type="personinfo"/>

<xs:complexType name="personinfo">
    <xs:sequence>
        <xs:element name="firstname" type="xs:string"/>
        <xs:element name="lastname" type="xs:string"/>
    </xs:sequence>
</xs:complexType>
```

In this example:

- The `employee` element references the `personinfo` complex type.
- This approach allows multiple elements to reuse the `personinfo` definition, enhancing modularity and reusability.

### Benefits of XML Schemas

- **Data Validation**: Ensures that XML documents conform to the expected structure and data types.
- **Interoperability**: Facilitates consistent data exchange across different systems.
- **Type Safety**: Defines strict data types, preventing incorrect data formats.
- **Reusability**: Complex types can be defined once and used across multiple elements.

XML Schemas play a crucial role in systems integration, ensuring that data shared between systems adheres to a well-defined structure, thereby reducing errors and improving data quality.

### 3.1. Create the XML File

- Open **Visual Studio**.
- Create a new XML file in Visual Studio:
  - Go to **File > New > File**.
  - Select **XML File** and write the XML content shown in Figure 1 (e.g., a basic XML document such as a list of books).

### 3.2. Generate the XML Schema

- Once you have your XML file, go to the **XML** menu at the top of Visual Studio and choose **Create Schema**.
- Visual Studio will automatically generate the corresponding XML Schema file (.XSD).
- The generated Schema file should resemble **Alternative 1** as described in your question.

### 3.3. Identify How Elements and Attributes Are Defined

In the generated `.xsd` file:

- **Elements**: Defined using `<xs:element>`. For example:

  ```xml
  <xs:element name="title" type="xs:string"/>
  ```

- **Attributes**: Defined using `<xs:attribute>`. For example:

  ```xml
  <xs:attribute name="category" type="xs:string"/>
  ```

The `name` attribute of the `<xs:element>` or `<xs:attribute>` tag defines the element/attribute's name, and the `type` specifies its data type (e.g., `xs:string` for text).

### 3.4. What is a Complex Type?

A **complex type** is an XML schema construct that defines elements that can contain other elements and/or attributes. Complex types are used to describe elements that have nested content (such as child elements), text content, or a mixture of both, often with specific ordering.

In the auto-generated file, the complex type for an element such as `<employee>` would look like this:

```xml
<xs:element name="employee">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="firstname" type="xs:string"/>
            <xs:element name="lastname" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

This structure indicates that the `employee` element contains the sub-elements `firstname` and `lastname`.

### 3.5. Difference Between `<sequence>`, `<choice>`, and `<all>`

- **`<sequence>`**: Specifies that the child elements must appear **in the specified order**. All elements in the sequence are required by default.

  Example:

  ```xml
  <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
  ```

- **`<choice>`**: Specifies that **one and only one** of the child elements may appear. The child elements are mutually exclusive.

  Example:

  ```xml
  <xs:choice>
      <xs:element name="book" type="xs:string"/>
      <xs:element name="magazine" type="xs:string"/>
  </xs:choice>
  ```

- **`<all>`**: Specifies that all child elements must appear, but their order **does not matter**. This is less common than `<sequence>`.

  Example:

  ```xml
  <xs:all>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
  </xs:all>
  ```

### 3.6. Where Are the Element Details Changed?

- **Number of Minimum and Maximum Occurrences**: Defined by `minOccurs` and `maxOccurs` attributes in the element tag.

  Example:

  ```xml
  <xs:element name="author" type="xs:string" minOccurs="1" maxOccurs="unbounded"/>
  ```

  This allows the `author` element to appear at least once (`minOccurs="1"`) and as many times as needed (`maxOccurs="unbounded"`).

- **Element Type**: The type of an element is defined using the `type` attribute in the `<xs:element>` tag.

  Example:

  ```xml
  <xs:element name="year" type="xs:integer"/>
  ```

### 3.7. Modify the Schema to Use Named Complex Types

Example:

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified"
  xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <!-- Complex Type Definition -->
  <xs:complexType name="bookType">
    <xs:sequence>
      <xs:element name="title" type="xs:string" />
      <xs:element name="author" type="xs:string" />
      <xs:element name="year" type="xs:unsignedShort" />
      <xs:element name="price" type="xs:decimal" />
      <xs:element minOccurs="0" name="rate" type="xs:unsignedByte" />
    </xs:sequence>
    <xs:attribute name="category" type="xs:string" use="required" />
  </xs:complexType>

  <!-- Root Element Definition -->
  <xs:element name="bookstore">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="book" type="bookType" maxOccurs="unbounded"></xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

This XML Schema defines a structure for a bookstore that contains multiple books. It uses a named complex type, `bookType`, which defines the structure of each individual book. Here’s an explanation of each component:

#### Complex Type Definition (`bookType`)

- The `bookType` complex type defines the structure of a book, containing the following elements and attributes:
  - **Elements:**
    - `<title>`: The title of the book, defined as a string (`xs:string`).
    - `<author>`: The author of the book, also a string (`xs:string`).
    - `<year>`: The publication year of the book, defined as an unsigned short integer (`xs:unsignedShort`), meaning it accepts non-negative values.
    - `<price>`: The price of the book, defined as a decimal (`xs:decimal`).
    - `<rate>` (optional): The rating of the book, defined as an unsigned byte (`xs:unsignedByte`), which can take values from 0 to 255. It has `minOccurs="0"`, making it optional.
  - **Attributes:**
    - `category`: A required attribute that specifies the category of the book. It is a string (`xs:string`) and is marked as `use="required"`, making it mandatory for each book.

#### Root Element Definition (`<bookstore>`)

- The `<bookstore>` element serves as the root of the XML document and contains a sequence of `<book>` elements.
  - **`<book>` Element:**
    - Each `<book>` element uses the previously defined `bookType` complex type.
    - `maxOccurs="unbounded"` allows for an unlimited number of book elements within the bookstore.

#### Additional Schema Settings

- **`attributeFormDefault="unqualified"`**: This means that attributes are not namespace-qualified by default.
- **`elementFormDefault="qualified"`**: This indicates that all elements within the XML document must be namespace-qualified.

#### Example XML That Conforms to This Schema

Here is an example XML document that would validate against the provided schema:

```xml
<?xml version="1.0" encoding="utf-8"?>
<bookstore xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="bookstore.xsd">
    <book category="CHILDREN">
        <title>Charlotte's Web</title>
        <author>E.B. White</author>
        <year>1952</year>
        <price>12.60</price>
    </book>
    <book category="WEB">
        <title>Beginning XML</title>
        <author>Joe Fawcett</author>
        <year>2012</year>
        <price>31.30</price>
        <rate>4</rate>
    </book>
    <book category="WEB">
        <title>Programming .NET Web Services</title>
        <author>Alex Ferrara</author>
        <year>2002</year>
        <price>38.36</price>
        <rate>3</rate>
    </book>
</bookstore>
```

**Explanation**:

- **Named Complex Type (`bookType`):**
  - The `bookType` complex type is defined to represent the structure of a book.
  - It includes the elements `<title>`, `<authors>`, `<year>`, `<price>`, `<rate>`, and `<publisher>`.
  - The `<authors>` element is defined as a complex type containing multiple `<author>` elements to support multiple authors.
  - The attributes `category` and `isbn` are defined within the `bookType` complex type.

- **Root Element (`<bookstore>`):**
  - The `<bookstore>` element is defined as a complex type containing a sequence of `<book>` elements.
  - The `<book>` element uses the `bookType` named complex type, allowing the schema to be easily extended or reused.

This modification improves the schema's flexibility and maintainability by separating the definition of the book structure from its usage, allowing for potential reuse in other parts of the schema.

### 3.8. Add `bookformat` Element and `isbn` Attribute

Modify the schema to include the `bookformat` element and an `isbn` attribute for books:

```xml
. . .
<xs:complexType name="bookType">
  <xs:sequence>
    <xs:element name="title" type="xs:string" />
    <xs:element name="author" type="xs:string" />
    <xs:element name="year" type="xs:unsignedShort" />
    <xs:element name="price" type="xs:decimal" />
    <xs:element name="rate" type="xs:unsignedByte" minOccurs="0" />
    <xs:element name="bookformat" type="xs:string"/>
  </xs:sequence>
  <xs:attribute name="category" type="xs:string" use="required" />
  <xs:attribute name="isbn" type="xs:string"/>
</xs:complexType>
. . .
```

### 3.9. Add Restrictions to the Schema

- **3.9.1. Restrict `category` Attribute Values**: Modify the `category` attribute to allow only specific values (`WEB`, `CHILDREN`, `SCIENCE`, `ROMANCE`, etc.).

  ```xml
  <xs:attribute name="category">
      <xs:simpleType>
          <xs:restriction base="xs:string">
              <xs:enumeration value="WEB"/>
              <xs:enumeration value="CHILDREN"/>
              <xs:enumeration value="SCIENCE"/>
              <xs:enumeration value="ROMANCE"/>
          </xs:restriction>
      </xs:simpleType>
  </xs:attribute>
  ```

- **3.9.2. Restrict `rate` Element Values (1 to 5)**:

  ```xml
  <xs:element name="rate">
      <xs:simpleType>
          <xs:restriction base="xs:integer">
              <xs:minInclusive value="1"/>
              <xs:maxInclusive value="5"/>
          </xs:restriction>
      </xs:simpleType>
  </xs:element>
  ```

- **3.9.3. Restrict `year` Element to 4 Digits**:

  ```xml
  <xs:element name="year">
      <xs:simpleType>
          <xs:restriction base="xs:integer">
              <xs:pattern value="\d{4}"/>
          </xs:restriction>
      </xs:simpleType>
  </xs:element>
  ```

- **3.9.4. Restrict `bookformat` Element**:

  ```xml
  <xs:element name="bookformat">
      <xs:simpleType>
          <xs:restriction base="xs:string">
              <xs:enumeration value="paperback"/>
              <xs:enumeration value="electronic book text"/>
              <xs:enumeration value="hardback"/>
              <xs:enumeration value="e book"/>
              <xs:enumeration value="loose-leaf"/>
          </xs:restriction>
      </xs:simpleType>
  </xs:element>
  ```
