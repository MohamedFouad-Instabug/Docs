# RecipeHub 2.0 Documentation

This documentation covers the RecipeHub 2.0 application, a comprehensive recipe management platform built with React.  It details the architecture, features, and technical implementation of the application.

## Overview

RecipeHub 2.0 transforms a simple recipe viewer into a full-featured platform with user authentication, advanced search and filtering, rating and review systems, and social features. The application utilizes a modern UI design with a glassmorphism style and is built on a scalable architecture.

## Architectural Changes

### Authentication System

RecipeHub 2.0 implements a JWT-based authentication system using React Context API for global state management.  User sessions are persisted using localStorage.

Key Files:
- `src/App.js`: Manages authentication state.
- `src/context/AuthContext.js`: Provides the authentication context and reducer.
- `src/services/api.js`: Handles API requests, including authentication endpoints.

### Service Layer Architecture

The application features a centralized API service layer (`src/services/api.js`) for communication with the backend.  It includes error handling, request/response interceptors for authentication, and modular API methods for various features (authentication, user management, recipe operations, etc.)

### Enhanced Data Structure

The recipe data structure has been enhanced to include more metadata, such as category, difficulty, prep time, cook time, servings, dietary information, ratings, and tags. See `src/App.js` for the detailed recipe data structure.

### State Management

React Context and useReducer are used for complex state management. Custom hooks provide authentication and permissions. Local storage is used for persistent user data.

## Business Feature Changes

### User Management System

Users can register, log in, and manage their profiles.  Dietary restrictions, favorite recipe categories, and spice level preferences can be set in user profiles. Saved recipes functionality is also implemented.

### Recipe Rating & Review System

Users can rate recipes using a 5-star system and leave reviews. Average ratings and review counts are displayed for each recipe.

### Advanced Search & Filtering

Real-time search by recipe name and tags, category filtering, dietary filters, and difficulty level filtering are available.

### Enhanced Recipe Display

Recipe cards with metadata and recipe detail views provide comprehensive information. Dietary tags are color-coded for quick identification.

### Social Features

Recipe sharing, user comments, and discussions are supported via API (implementation pending).

## UI/UX Improvements

A complete design overhaul using a glassmorphism design with gradient backgrounds and a modern color scheme enhances the user experience. The component structure includes new components such as a Header, Search and Filter section, Recipe Cards, and Modal Dialogs.

## Package.json Updates

The `package.json` file has been updated to reflect the project's name change to "recipehub" and the addition of new dependencies, including `react-router-dom`, `axios`, `jwt-decode`, `react-hook-form`, `react-query`, `react-hot-toast`, `framer-motion`, `react-intersection-observer`, `react-virtualized`, `date-fns`, `lodash`, and `clsx`.

New scripts have been added for linting, formatting, analysis, and testing.

## n8n Implementation

The n8n-workflow-design.md provides a comprehensive guide for implementing an automated documentation workflow using n8n to analyze PR changes and generate documentation. This workflow includes data extraction, AI analysis (Gemini), documentation generation, and communication steps, offering a visual alternative to GitHub Actions.
