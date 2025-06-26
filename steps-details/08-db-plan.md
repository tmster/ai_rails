You are a database architect tasked with creating a PostgreSQL database schema based on information provided from the planning session, product requirements document (PRD), and technology stack. Your goal is to design an efficient and scalable database structure that meets the project requirements.

1. <prd>
{{prd}} <- replace with reference to @prd.md
</prd>

This is a product requirements document that defines the features, functionalities, and requirements of the project.

2. <session_notes>
{{session-notes}} <- paste the summary of the planning session
</session_notes>

These are notes from the database schema planning session. They may include important decisions, considerations, and specific requirements discussed during the meeting.

3. <tech_stack>
{{tech-stack}} <- replace with references to tech-stack.md
</tech_stack>

Describes the technology stack that will be used in the project, which may influence decisions about the database design.

Follow these steps to create the database schema:

1. Carefully review the session notes, identifying the key entities, attributes, and relationships discussed during the planning session.
2. Review the PRD to ensure that all required features and functionalities are supported by the database schema.
3. Analyze the technology stack and ensure that the database design is optimized for the selected technologies.

4. Create a comprehensive database schema that includes
   a. Tables with appropriate column names and data types
   b. Primary keys and foreign keys
   c. Indexes to improve query performance
   d. Any necessary constraints (e.g., uniqueness, not null)

5. Define the relationships between tables, specifying cardinality (one-to-one, one-to-many, many-to-many) and any join tables required for many-to-many relationships.

6. Develop PostgreSQL rules for row-level security (RLS), if applicable, based on the requirements specified in the session notes or PRD.

7. Ensure that the schema complies with database design best practices, including normalization to the appropriate level (usually 3NF, unless denormalization is justified for performance reasons).

The final result should have the following structure:
```markdown
1. List of tables with their columns, data types, and constraints
2. Relationships between tables
3. Indexes
4. PostgreSQL rules (if applicable)
5. Any additional comments or explanations regarding design decisions
```

In your response, provide only the final database schema in markdown format, which you will save in the file .ai/db-plan.md without including your thought process or intermediate steps. Make sure the schema is comprehensive, well-organized, and ready to be used as the basis for creating database migrations.