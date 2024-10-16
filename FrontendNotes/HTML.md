# HTML

### 1. **Basic Structure**

- **Definition**: The foundation of an HTML document, which includes the `<!DOCTYPE html>`, `<html>`, `<head>`, and `<body>` tags.
- **Components**:
  - `<!DOCTYPE html>`: Declares the document type.
  - `<head>`: Contains metadata like title, links to CSS, or scripts.
  - `<body>`: Contains all the visible content.
- **Example in Projects**:
  - **Websites**: Every web page starts with this structure, ensuring the document is recognized as HTML5 and that metadata is properly processed (e.g., linking stylesheets, setting page titles).
  - **Web apps**: Proper structure ensures that JavaScript, SEO meta tags, and other components are loaded correctly.
- **Code Example**:
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>My Webpage</title>
    </head>
    <body>
      <h1>Welcome to My Website</h1>
      <p>This is a paragraph inside the body section.</p>
    </body>
  </html>
  ```

### 2. **Text Elements**

- **Definition**: Used to define and format text within an HTML document.
- **Common Tags**:
  - `<p>`: Paragraphs.
  - `<h1> - <h6>`: Headers, ranging from largest (`h1`) to smallest (`h6`).
  - `<span>`: Inline container.
  - `<strong>`: Strong emphasis (bold).
  - `<em>`: Emphasis (italic).
- **Example in Projects**:
  - **Blogs**: Using headings for blog post titles (`<h1>`) and sections (`<h2> - <h6>`), paragraphs for content (`<p>`), and `<strong>` or `<em>` for emphasizing certain text.
  - **E-commerce websites**: Titles and descriptions for products, using headers and paragraph tags for layout.
- **Code Example**:
  ```html
  <h1>Heading 1</h1>
  <p>
    This is a paragraph of text. <strong>This text is bold.</strong>
    <em>This text is italicized.</em>
  </p>
  <span>This is an inline span element.</span>
  ```

### 3. **Lists**

- **Definition**: Used to create lists, both ordered and unordered.
- **Common Tags**:
  - `<ol>`: Ordered list (numbered).
  - `<ul>`: Unordered list (bulleted).
  - `<li>`: List item.
- **Example in Projects**:
  - **Product listings**: Unordered lists (`<ul>`) used for product features, specifications.
  - **Steps in a process**: Ordered lists (`<ol>`) are used in instructional articles, showing step-by-step guides.
- **Code Example**:

  ```html
  <h2>Unordered List</h2>
  <ul>
    <li>First item</li>
    <li>Second item</li>
    <li>Third item</li>
  </ul>

  <h2>Ordered List</h2>
  <ol>
    <li>Step 1</li>
    <li>Step 2</li>
    <li>Step 3</li>
  </ol>
  ```

### 4. **Links**

- **Definition**: Used to create hyperlinks to navigate between different pages or sections.
- **Tag**:
  - `<a>`: Anchor tag to define links.
- **Example in Projects**:
  - **Navigation menus**: Anchor tags are used for internal links to other pages or sections.
  - **External links**: Linking to external resources, documentation, or social media.
  - **SPA (Single Page Application)**: `<a>` tags for smooth navigation within a single page.
- **Code Example**:
  ```html
  <a href="https://example.com">Visit Example.com</a>
  <a href="#section1">Go to Section 1</a>
  ```

### 5. **Images and Media**

- **Definition**: Tags to embed images, audio, and video content within a webpage.
- **Common Tags**:
  - `<img>`: Displays images.
  - `<video>`: Embeds video content.
  - `<audio>`: Embeds audio files.
- **Attributes**: `alt`, `src`, `controls`, etc.
- **Example in Projects**:
  - **E-commerce sites**: Product galleries using `<img>` tags.
  - **Streaming services**: Using `<video>` tags to play video content.
  - **Podcasts**: Embedding audio files using `<audio>` tags.
- **Code Example**:
  ```html
  <img src="image.jpg" alt="Description of the image" />
  <video src="video.mp4" controls></video>
  <audio src="audio.mp3" controls></audio>
  ```

### 6. **Forms**

- **Definition**: Used for collecting user input and sending it to a server.
- **Common Tags**:
  - `<form>`: Form element to wrap input fields.
  - `<input>`: Input fields (e.g., text, password, checkbox).
  - `<button>`: Buttons to submit the form.
  - `<select>`: Drop-down lists.
- **Example in Projects**:
  - **Contact forms**: Forms that collect user names, emails, and messages.
  - **E-commerce checkout**: Forms for inputting billing, shipping details.
  - **Login systems**: Forms for username and password inputs.
- **Code Example**:

  ```html
  <form action="/submit" method="POST">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" />

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" />

    <button type="submit">Submit</button>
  </form>
  ```

### 7. **Semantic Elements**

- **Definition**: HTML5 introduced semantic elements to clearly define the structure of the page.
- **Common Tags**:
  - `<section>`: Groups related content.
  - `<article>`: Contains self-contained content like a blog post.
  - `<nav>`: Defines navigation links.
  - `<header>`: Defines the header for a section or page.
  - `<footer>`: Footer of the document.
  - `<aside>`: Side content, like a sidebar.
  - `<main>`: Main content of the page.
- **Example in Projects**:
  - **Blog or news site**: Using `<article>` to wrap individual blog posts or news articles.
  - **Website layouts**: Using `<header>` and `<footer>` for consistent page headers and footers.
  - **Navigation bars**: Using `<nav>` for creating a navigation menu that helps in search engine optimization (SEO).
- **Code Example**:

  ```html
  <header>
    <h1>Website Header</h1>
    <nav>
      <a href="#home">Home</a>
      <a href="#about">About</a>
    </nav>
  </header>

  <main>
    <section>
      <h2>Section Title</h2>
      <p>This is the main content.</p>
    </section>

    <article>
      <h2>Article Title</h2>
      <p>This is an article.</p>
    </article>
  </main>

  <footer>
    <p>Website Footer</p>
  </footer>
  ```

### 8. **Tables**

- **Definition**: Used to display data in a tabular format.
- **Common Tags**:
  - `<table>`: Main table tag.
  - `<tr>`: Table row.
  - `<td>`: Table data/cell.
  - `<th>`: Table header.
  - `<thead>`: Table header group.
  - `<tbody>`: Table body group.
  - `<tfoot>`: Table footer group.
- **Example in Projects**:
  - **Data dashboards**: Displaying datasets or reports using tables.
  - **Product comparison charts**: Listing features and specifications side by side for easy comparison.
- **Code Example**:
  ```html
  <table>
    <thead>
      <tr>
        <th>Product</th>
        <th>Price</th>
        <th>Quantity</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Item 1</td>
        <td>$10</td>
        <td>5</td>
      </tr>
      <tr>
        <td>Item 2</td>
        <td>$20</td>
        <td>3</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td colspan="3">Total: $80</td>
      </tr>
    </tfoot>
  </table>
  ```

### 9. **Meta Information**

- **Definition**: Tags that provide metadata about the HTML document, such as SEO data or viewport settings.

- **Common Tags**:
  - `<meta>`: Used to define metadata such as character sets, viewport settings, description, and keywords.
- **Example in Projects**:
  - **SEO**: Using meta tags for defining page descriptions and keywords that help in improving search engine rankings.
  - **Mobile responsiveness**: Using viewport meta tags to ensure the website scales properly on mobile devices.
- **Code Example**:
  ```html
  <meta
    name="description"
    content="This is a description of the webpage for SEO purposes."
  />
  <meta name="keywords" content="HTML, CSS, JavaScript" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  ```
