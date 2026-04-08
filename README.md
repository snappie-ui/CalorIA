CalorIA – Technical README
## Overview

CalorIA is a full-stack calorie tracking application designed to help users monitor their meals, nutrition, and basic health metrics such as weight and water intake. The system combines a Flask-based backend, a React frontend, and a MongoDB database. In addition, it includes a custom CLI for managing workflows and an AI-powered research module for expanding ingredient and recipe data .

The goal of the project was to build a system that is not only functional but also extensible, especially with the integration of AI-driven features.

## Walkthrough Video

This is a 10–15 minute walkthrough covering:
- Architecture and system design  
- Project structure  
- Key technical decisions  
- AI-powered features  
- Risks and future improvements  

Watch the video here:
https://drive.google.com/file/d/1joXq9kk9KRAQdaPGHXjAT_ISB8FD4_Nz/view?usp=drive_link

## Architecture

The application follows a layered architecture with clear separation of concerns:

Frontend: Built using React, responsible for user interaction and UI rendering
Backend: Flask REST API handling business logic and communication with the database
Database: MongoDB for storing users, meals, ingredients, recipes, and health data
CLI Layer: A Python-based command-line interface for running and managing the system
AI Layer: A modular research system for generating ingredients and recipes
Deployment: Docker and docker-compose for containerized execution
Flow of Data

User requests originate from the frontend, pass through the Flask API, and interact with MongoDB. The CLI can directly trigger backend processes, including AI-based research and database seeding.

## Project Structure

The project is organized to keep logic modular and maintainable:

backend/: Flask application and API logic
frontend/: React application
mixins/: Core business logic and route handlers
research/: AI-powered modules for ingredients and recipes
cli.py: Entry point for CLI commands
docker-compose.yml: Container orchestration

This structure allows independent development and testing of different parts of the system.

## Key Technical Decisions

One of the main design choices was using MongoDB instead of a relational database. Since recipes and ingredients can have varying structures, a flexible schema made it easier to store and extend data, especially when integrating AI-generated content.

Flask was chosen over heavier frameworks because it provides more control and keeps the backend lightweight. This was useful for building a clean REST API without unnecessary abstraction.

The inclusion of a custom CLI was a deliberate decision. It simplifies tasks such as starting the backend, running the frontend, seeding the database, and executing AI research. This also makes the system easier to test and automate.

AI functionality was kept as a separate layer, rather than embedding it deeply into the core application. This ensures that failures in AI services do not affect the core functionality of the app.

Finally, Docker was used to standardize the environment and make the project easier to run and evaluate across different systems.

## AI Usage

The AI component is used to automatically discover and generate new ingredients and recipes.

The process works as follows:

A CLI command triggers the research module
The system sends structured prompts to the selected AI provider
The response is parsed and validated
Duplicate entries are avoided
Valid data is stored in MongoDB

Two AI providers are supported:

OpenAI, which provides higher-quality results but requires an API key
Ollama, which allows local execution without external dependencies

The research process is structured using categories and alphabetical grouping, which ensures systematic and controlled data expansion.

AI Guidance and Constraints

Although there are no separate documentation files for prompts, the system defines AI behavior within the research modules. These include:

Category-based filtering
Letter-based iteration (e.g., A, B, C...)
Limits on the number of generated items
Validation checks before inserting into the database

This approach helps maintain consistency and prevents uncontrolled or irrelevant data generation.

## Risks and Limitations

One of the primary concerns is AI hallucination, where the model may generate incorrect or unrealistic data. This is partially handled through validation and controlled prompts, but it cannot be fully eliminated.

Another limitation is the dependency on external services when using OpenAI. This is mitigated by supporting Ollama for local execution.

Using MongoDB introduces flexibility but also the risk of inconsistent data structures. This is managed through structured handling in the backend modules.

The CLI, while powerful, may not be intuitive for all users, especially those unfamiliar with command-line tools.

Finally, the current stack is suitable for development and moderate usage, but scaling to high traffic would require further optimization.

## Extension Approach

The system is designed to be extended in multiple directions.

AI capabilities can be expanded to include personalized meal recommendations or diet planning. The frontend can be enhanced with better analytics, such as calorie trends and health insights.

Authentication can be improved with OAuth-based login systems. A mobile application could also be developed using React Native or Flutter.

From a backend perspective, scaling could involve introducing caching, load balancing, or transitioning to microservices if needed.

CalorIA combines traditional full-stack development with AI-driven functionality in a modular and extensible way. The system is designed to be practical, easy to run, and adaptable for future enhancements, while keeping the core architecture clean and maintainable.