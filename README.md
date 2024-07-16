### GitHub Profile Fetcher
GitHub Profile Fetcher is a simple web application that allows users to fetch and display GitHub profile information and repositories by entering a GitHub username.

## Table of Contents

Features
Technologies Used
File Structure
Getting Started
Usage

## Features
Fetches GitHub profile information including avatar, name, bio, and profile link.
Displays a list of public repositories with links and descriptions.
User-friendly interface.
## Technologies Used
HTML5
CSS3
JavaScript
GitHub API
## File Structure
plaintext
Copy code
GitHub-Profile-Fetcher/
├── img/
│   └── (optional images directory)
├── index.html
├── style.css
├── script.js
└── README.md
Getting Started
P## rerequisites
Ensure you have a modern web browser installed to view the web application.

Installation
Clone the repository:

sh
Copy code
git clone https://github.com/Preethipa19/github-profile-fetcher.git
Navigate to the project directory:

sh
Copy code
cd github-profile-fetcher
Open index.html in your web browser to view the application.

## Usage
Enter a GitHub username in the input field.
Click the "Fetch Profile" button.
View the fetched profile information and repositories.
## HTML Structure
html
Copy code
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>GitHub Profile Fetcher</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <h1>GitHub Profile Fetcher</h1>
    <input type="text" id="text" placeholder="Enter GitHub Username" />
    <button onclick="git()">Fetch Profile</button>

    <div id="result"></div>
    <div id="repos"></div>

    <script src="script.js"></script>
  </body>
</html>

JavaScript Function
## javascript
Copy code
function git() {
    var originalName = document.getElementById("text").value;
    console.log(originalName);

    // Fetch user information
    fetch("https://api.github.com/users/" + originalName)
        .then((result) => result.json())
        .then((data) => {
            console.log(data);
            document.getElementById("result").innerHTML = `
                <img src="${data.avatar_url}" alt="user_avatar">
                <h1>${data.name}</h1>
                <p>${data.bio}</p>
                <p><a href="${data.html_url}" target="_blank">View Profile</a></p>
            `;
        });

    // Fetch user repositories
    fetch("https://api.github.com/users/" + originalName + "/repos")
        .then((result) => result.json())
        .then((data) => {
            console.log(data);
            let repoList = "<h2>Repositories:</h2><ul>";
            data.forEach(repo => {
                repoList += `
                    <li>
                        <a href="${repo.html_url}" target="_blank">${repo.name}</a> - ${repo.description}
                    </li>`;
            });
            repoList += "</ul>";
            document.getElementById("repos").innerHTML = repoList;
        });
}