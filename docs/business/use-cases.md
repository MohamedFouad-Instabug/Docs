Given the extensive changes detailed in the `CHANGES_SUMMARY.md` file, including architectural changes like the Authentication System and Service Layer Architecture, as well as business feature changes like the User Management and Recipe Rating systems, the current documentation (`docs/business/use-cases.md`) is woefully inadequate. It should be significantly expanded or replaced with a new document outlining the capabilities of RecipeHub 2.0.

Specifically, the new documentation should:

1.  Detail the authentication process and user roles (if applicable).
2.  Explain how users can create, rate, and save recipes.
3.  Describe the search and filtering functionalities, including dietary and difficulty filters.
4.  Highlight the social features, such as recipe sharing and commenting (if implemented).
5.  Outline the user management system and how users can customize their profiles and preferences.
6. Explain the analytics features for recipe popularity. This should align with the major functional changes in the new service layer architecture `src/services/api.js`.

Also, update the project name and description in all documentation files from "test-docs-workflow" to "recipehub - A modern recipe management platform with user authentication, ratings, social features, and dietary preferences".