# Product Search Page 🚀

A simple, client-side web application that fetches product data from a public Google Sheet and allows users to search for products in real-time. The project is self-contained in a single `index.html` file, making it easy to deploy and modify.

***

## ✨ Features

* **Dynamic Data Loading**: Fetches and parses product data directly from a Google Sheet published as a CSV.
* **Live Search**: Instantly filters products by **Name** or **Product Code** as the user types.
* **Responsive Design**: Product cards are displayed in a clean, responsive grid that adapts to different screen sizes.
* **Randomized Initial Display**: Shows a random selection of products on page load to give a glimpse of the catalog.
* **Pagination**: A "Load More" button allows users to load more search results without overwhelming the initial view.
* **Zero Backend**: The entire application runs in the browser, requiring no server-side code or database.
* **Error Handling**: Displays user-friendly messages for loading errors or when no search results are found.

***

## 🛠️ How It Works

The application operates using vanilla JavaScript and the [PapaParse](https://www.papaparse.com/) library for CSV parsing.

1.  **Data Fetching**: On page load, the script makes a `GET` request to a Google Sheet URL. The `pubId` in the script specifies which published sheet to use.
2.  **Parsing**: **PapaParse** asynchronously downloads and parses the CSV data from the URL into a JavaScript array of objects.
3.  **Initial Render**: A shuffled subset of the products is displayed to the user.
4.  **Searching**: An `input` event listener on the search box filters the main product array based on the user's query.
5.  **DOM Manipulation**: The filtered results are dynamically rendered as product cards and appended to the page. The "Load More" button is shown or hidden based on whether more results are available.

***

## 🔧 Setup and Customization

Since this is a single-file project, no complex setup is required. Just open the `index.html` file in any modern web browser.

To customize the project with your own data, follow these steps:

### 1. Prepare Your Google Sheet

Your Google Sheet should have a header row with columns like `Name`, `Image URL`, `AliExpress Link`, and `Product Code`.

### 2. Publish Your Sheet to the Web

1.  In Google Sheets, go to **File** -> **Share** -> **Publish to web**.
2.  In the dialog box, select the specific sheet you want to use.
3.  Choose **Comma-separated values (.csv)** as the format.
4.  Click **Publish**.
5.  Google will provide a public URL. It will look something like this:
    `https://docs.google.com/spreadsheets/d/e/2PACX-1vS9Yg6etFwOX1L-t2lnOX08ODcj6Z4xnPCCfuqMkZLrtNknP1jNThnvh64s96eTN6hbOq_aP0NBnOSW/pub?output=csv`

### 3. Update the Script

1.  Copy the long, unique identifier from the URL you just generated. In the example above, it is:
    `2PACX-1vS9Yg6etFwOX1L-t2lnOX08ODcj6Z4xnPCCfuqMkZLrtNknP1jNThnvh64s96eTN6hbOq_aP0NBnOSW`
2.  Open `index.html` and find this line in the `<script>` tag:
    ```javascript
    const pubId = '2PACX-1vS9Yg6etFwOX1L-t2lnOX08ODcj6Z4xnPCCfuqMkZLrtNknP1jNThnvh64s96eTN6hbOq_aP0NBnOSW';
    ```
3.  Replace the existing `pubId` string with the ID from your own Google Sheet.

### 4. Customize Product Cards (Optional)

You can change the appearance and content of the product cards by editing the `renderProduct` function in the script. Modify the HTML string inside this function to use different columns from your spreadsheet.

```javascript
// Current card structure
function renderProduct(item) {
  const card = document.createElement('div'); card.className = 'product';
  card.innerHTML = `<h3>${item['Name']||'Unnamed'}</h3>
                    <img src="${item['Image URL']}" alt="${item['Name']}" />
                    <a class="buy-btn" href="${item['AliExpress Link']}" target="_blank">Buy on AliExpress</a>`;
  resultDiv.appendChild(card);
}
```

***

## 📦 Dependencies

This project relies on one external library:

* **[PapaParse](https://www.papaparse.com/)**: A powerful, in-browser CSV parser, included via a CDN link in the `<head>` of the HTML.
