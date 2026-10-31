# Pokémon Explorer API

A Vue 3 web application built with Vite that retrieves and displays random Pokémon information using the free PokéAPI.

The application automatically loads a random Pokémon when the page opens and allows users to discover new Pokémon without refreshing the page.

## Live Website

[View Pokémon Explorer](https://vue-pokemon-api-andres-orozco.netlify.app)

## Features

- Automatically retrieves a random Pokémon when the application loads.
- Displays Pokémon names, Pokédex numbers, types, and images.
- Uses Pokémon Legends: Z-A sprites when available.
- Automatically falls back to official Pokémon artwork when a Legends: Z-A sprite is unavailable.
- Displays Pokémon height in meters and inches.
- Displays Pokémon weight in kilograms and pounds.
- Includes a button to retrieve another random Pokémon without refreshing the page.
- Displays loading messages during API requests.
- Handles API errors and displays an appropriate error message.
- Features a custom Pokédex-inspired red-and-white design.

## Technologies Used

- **Vue 3** — Frontend JavaScript framework
- **Vite** — Development server and build tool
- **JavaScript** — API requests and application logic
- **HTML and CSS** — Page structure and styling
- **PokéAPI** — Public API providing Pokémon information
- **GitHub** — Version control and source code hosting
- **Netlify** — Website deployment and hosting

## API Information

This project uses the free [PokéAPI](https://pokeapi.co/) to retrieve Pokémon information.

Example endpoint:

`https://pokeapi.co/api/v2/pokemon/25`

The application uses JavaScript's built-in `fetch()` function to request Pokémon data.

Vue's `onMounted()` lifecycle hook automatically calls the API request function when the application loads.

The same function is called when the user clicks the button to retrieve another Pokémon.

No API key or authentication is required.

## Running the Project Locally

1. Clone the repository:

   `git clone https://github.com/Andresito096/vue-pokemon-api.git`

2. Navigate into the project directory:

   `cd vue-pokemon-api`

3. Install dependencies:

   `npm install`

4. Start the development server:

   `npm run dev`

5. Open the localhost URL provided by Vite.

## Deployment

The application is deployed using Netlify and connected to the GitHub repository.

Netlify automatically builds and deploys updates pushed to the `main` branch.

**Build command:** `npm run build`

**Publish directory:** `dist`

## Project Purpose

This application was developed as part of a Vue 3 and Vite assignment to demonstrate working with public APIs, reactive variables, lifecycle hooks, event handling, conditional rendering, and asynchronous JavaScript.

## Credits

Pokémon information and sprites are provided by [PokéAPI](https://pokeapi.co/) and its associated sprite repository.

Pokémon and related characters are trademarks of Nintendo, Game Freak, and The Pokémon Company. This project is for educational purposes and is not affiliated with or endorsed by those companies.