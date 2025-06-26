{{latest-round-answers}} <- list of answers to the second round of questions

---

You are an AI assistant tasked with summarizing a conversation about database planning for an MVP and preparing a concise summary for the next stage of development. The conversation history contains the following information:
1. Product requirements document (PRD)
2. Information about the technology stack
3. Conversation history containing questions and answers
4. Recommendations for the model

Your task is to:
1. Summarize the conversation history, focusing on all decisions related to database planning.
2. Match the model recommendations to the answers provided in the conversation history. Identify which recommendations are relevant based on the discussion.
3. Prepare a detailed summary of the conversation that includes:
a. Key requirements for the database schema
   b. Key entities and their relationships
   c. Important security and scalability issues
   d. Any unresolved issues or areas requiring further clarification
4. Format the results as follows:

<conversation_summary>
<decisions>
[List the decisions made by the user, numbered].
</decisions>

<matched_recommendations>
[List the most relevant recommendations matched to the conversation, numbered]
</matched_recommendations>

<database_planning_summary> [Database planning summary]
[Provide a detailed summary of the conversation, including the items listed in step 3].
</database_planning_summary>

<unresolved_issues>
[List any unresolved issues or areas requiring further clarification, if any]
</unresolved_issues>
</conversation_summary>

The final result should only contain content in markdown format. Make sure your summary is clear, concise, and provides valuable information for the next stage of database planning.

