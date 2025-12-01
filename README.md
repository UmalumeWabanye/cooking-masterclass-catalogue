

# Cooking Masterclass Catalogue

An interactive single-page Vue 3 app for browsing curated cooking workshops hosted by expert chefs. Users can explore courses, see pricing, availability, and save favorites to a wishlist.

## Features & Success Criteria
- Dynamic catalogue: courses rendered from a single array, no hard-coded duplicates
- Course cards display title, chef, price (formatted as currency), skill level, and sold out indication
- Wishlist functionality: users can save courses, counter updates in header with animation
- Filtering: toggle to show only available classes
- Responsive layout for desktop and mobile
- Hover/selection animations for interactivity
- Clean, branded color palette and minimal styling
- Organized, professional codebase

## Technical Scope
- Vue 3 with Vite setup
- Local data only (no API)
- Single-page app structure (no router)
- Component-driven design using props, data, and events

## Installation
1. Clone the repository:
	```sh
	git clone <your-repo-url>
	cd Cooking_Masterclass
	```
2. Install dependencies:
	```sh
	npm install
	```
3. Run the development server:
	```sh
	npm run dev
	```

## Usage
Open your browser to the local server URL (usually http://localhost:5173) to view and interact with the catalogue.

## Project Structure
- `src/components/CourseCard.vue`: Course card component
- `src/App.vue`: Main app layout and logic
- `src/style.css`: Global styles

## User Flow
1. Browse all courses in a responsive grid
2. View chef, skill level, price, and availability for each course
3. Save available courses to wishlist; counter animates and updates
4. Filter to show only available classes
5. Enjoy a smooth, interactive experience on desktop and mobile

## Overview
This project is the foundation for Cooking Masterclass’s future e-commerce platform. It demonstrates component-driven design, local state management, and a professional codebase ready for expansion.
