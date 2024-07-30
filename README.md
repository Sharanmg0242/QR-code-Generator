# URL to QR Code Generator

This project allows you to convert a URL into a QR code image and save the URL to a text file using Node.js. It utilizes the `inquirer` package to get user input, the `qr-image` package to generate the QR code, and the native `fs` module to handle file operations.

## Features

- Prompt user for a URL.
- Generate a QR code image from the provided URL.
- Save the provided URL to a text file.

## Prerequisites

Make sure you have Node.js installed. You can download it from [nodejs.org](https://nodejs.org/).

## Installation

1. Clone the repository:
    ```sh
    git clone https://github.com/your-username/url-to-qr-code-generator.git
    ```
2. Navigate to the project directory:
    ```sh
    cd url-to-qr-code-generator
    ```
3. Install the required packages:
    ```sh
    npm install inquirer qr-image
    ```

## Usage

1. Run the script:
    ```sh
    node index.js
    ```
2. You will be prompted to enter a URL:
    ```
    ? Type in your URL: 
    ```
3. Enter the URL and press `Enter`. The script will generate a QR code image (`qr_img.png`) and save the URL to a text file (`URL.txt`).

## Code Explanation

The code prompts the user to enter a URL using `inquirer`, generates a QR code image from the URL using `qr-image`, and saves the URL to a text file using the `fs` module.

```javascript
import inquirer from "inquirer";
import qr from "qr-image";
import fs from "fs";

inquirer
  .prompt([
    {
      message: "Type in your URL: ",
      name: "URL",
    },
  ])
  .then((answers) => {
    const url = answers.URL;
    var qr_svg = qr.image(url);
    qr_svg.pipe(fs.createWriteStream("qr_img.png"));

    fs.writeFile("URL.txt", url, (err) => {
      if (err) throw err;
      console.log("The file has been saved!");
    });
  })
  .catch((error) => {
    if (error.isTtyError) {
      console.error("Prompt couldn't be rendered in the current environment");
    } else {
      console.error("Something went wrong:", error);
    }
  });
