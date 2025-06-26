<conversation_summary>
<decisions>
1. Use the `invitations` table with a `duration_minutes` field of type INTEGER.
2. Store duration in minutes (INTEGER) rather than INTERVAL.
3. Include `name` alongside `email` in the `invitation_participants` table.
4. Do not add `error_code` or `error_message` fields to the `deliveries` table at this stage.
5. Apply a UNIQUE constraint on `invitation_participant_id` in the `confirmations` table.
6. Use an ENUM for `day_of_week` in the `user_working_hours` table.
7. Use a RANGE type with an exclusion constraint in `user_working_hours` to prevent overlapping hours.
8. Implement `audit_trail` manually in service code rather than via database triggers.
</decisions>

<matched_recommendations>
1. Define `duration_minutes` as INTEGER NOT NULL CHECK(duration_minutes > 0).
2. Add a `name` column to the `invitation_participants` table.
3. Enforce UNIQUE(invitation_participant_id) in the `confirmations` table.
4. Define a `user_day_enum` ENUM for `day_of_week`.
5. Apply a RANGE type and exclusion constraint in the `user_working_hours` table.
6. Record `audit_trail` in service code instead of using triggers.
</matched_recommendations>

<database_planning_summary>
a. Key requirements:
   - Management of users, invitations, participants, time slots, deliveries, and confirmations.
   - Storage of working hour preferences in a normalized form with exclusion constraints.
   - CRUD auditing implemented in service code.

b. Key entities and relationships:
   - users (UUID PK) → invitations (organizer_id FK) → invitation_participants (email, name, role)
   - invitation_participants → time_slots (start_time, end_time, is_suggested)
   - invitation_participants → deliveries (channel, status, sent_at, response JSONB)
   - invitation_participants → confirmations (confirmed_at)
   - users → user_working_hours (day_of_week ENUM, time RANGE)
   - audit_trail managed in service code.

c. Security and scalability:
   - Authentication and authorization via JWT tokens instead of a separate tokens table.
   - B-tree indexes on FKs and status fields, GIN on JSONB.
   - No partitioning or materialized views at the MVP stage.

d. Unresolved issues:
   - None – all main assumptions and constraints have been clarified.
</database_planning_summary>

<unresolved_issues>
None – all schema requirements and decisions have been finalized.
</unresolved_issues>
</conversation_summary>