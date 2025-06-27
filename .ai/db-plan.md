# Database Schema

## 1. Tables with Columns, Data Types, and Constraints

### 1.1 users
- **id**: UUID PRIMARY KEY DEFAULT gen_random_uuid()
- **email**: VARCHAR(255) NOT NULL UNIQUE
- **encrypted_password**: VARCHAR(255) NOT NULL
- **name**: VARCHAR(255)
- **phone_number**: VARCHAR(50)
- **linkedin_profile**: VARCHAR(255)
- **created_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- **updated_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.2 invitations
- **id**: UUID PRIMARY KEY DEFAULT gen_random_uuid()
- **organizer_id**: UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE
- **title**: VARCHAR(255) NOT NULL
- **description**: TEXT
- **duration_minutes**: INTEGER NOT NULL CHECK (duration_minutes > 0)
- **secure_token**: VARCHAR(64) NOT NULL UNIQUE
- **created_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- **updated_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.3 invitation_participants
- **id**: UUID PRIMARY KEY DEFAULT gen_random_uuid()
- **invitation_id**: UUID NOT NULL REFERENCES invitations(id) ON DELETE CASCADE
- **email**: VARCHAR(255) NOT NULL
- **name**: VARCHAR(255)  -- Stores participant name
- **role**: VARCHAR(50)
- **created_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- **updated_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.4 time_slots
- **id**: UUID PRIMARY KEY DEFAULT gen_random_uuid()
- **invitation_participant_id**: UUID NOT NULL REFERENCES invitation_participants(id) ON DELETE CASCADE
- **start_time**: TIMESTAMP WITH TIME ZONE NOT NULL
- **end_time**: TIMESTAMP WITH TIME ZONE NOT NULL
- **is_suggested**: BOOLEAN NOT NULL DEFAULT false
- **created_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- **updated_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.5 deliveries
- **id**: UUID PRIMARY KEY DEFAULT gen_random_uuid()
- **invitation_participant_id**: UUID NOT NULL REFERENCES invitation_participants(id) ON DELETE CASCADE
- **channel**: VARCHAR(20) NOT NULL CHECK (channel IN ('email','sms','linkedin'))
- **status**: VARCHAR(20) NOT NULL CHECK (status IN ('pending','sent','failed'))
- **sent_at**: TIMESTAMP WITH TIME ZONE
- **response**: JSONB
- **created_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- **updated_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.6 confirmations
- **id**: UUID PRIMARY KEY DEFAULT gen_random_uuid()
- **invitation_participant_id**: UUID NOT NULL UNIQUE REFERENCES invitation_participants(id) ON DELETE CASCADE
- **confirmed_at**: TIMESTAMP WITH TIME ZONE NOT NULL
- **created_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- **updated_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.7 user_working_hours
- **id**: UUID PRIMARY KEY DEFAULT gen_random_uuid()
- **user_id**: UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE
- **day_of_week**: user_day_enum NOT NULL
- **working_hours**: TSRANGE NOT NULL  -- Represents the user's working hours range
- **created_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- **updated_at**: TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- **Constraint**: Exclusion constraint on (user_id, working_hours) to prevent overlapping time ranges

### 1.8 user_day_enum
- **Definition**: ENUM type for days of the week
  - Values: 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday'

## 2. Relationships Between Tables
- **users** → **invitations**: One-to-many (a user can create many invitations)
- **invitations** → **invitation_participants**: One-to-many (an invitation can have multiple participants)
- **invitation_participants** → **time_slots**: One-to-many (a participant can propose multiple time slots)
- **invitation_participants** → **deliveries**: One-to-many (each participant can have multiple delivery records)
- **invitation_participants** → **confirmations**: One-to-one (each participant has a unique confirmation)
- **users** → **user_working_hours**: One-to-many (a user can have multiple working hour entries)

## 3. Indexes
- **users**: Unique index on email (automatically created by UNIQUE constraint)
- **invitations**: B-tree index on organizer_id to optimize lookups by user
- **time_slots**: B-tree index on invitation_participant_id for faster join operations
- **deliveries**: GIN index on response (JSONB) to support efficient JSON queries
- **user_working_hours**: Composite index on user_id and working_hours to optimize availability queries

## 4. PostgreSQL Rules
- **Row-Level Security (RLS)**: Not implemented at MVP; may be added in future iterations if needed.
- **Audit Trail**: Managed in service code; no triggers are defined in the database.

## 5. Additional Comments
- The schema is normalized to 3NF to ensure data integrity and reduce redundancy.
- The ENUM type `user_day_enum` enforces valid day values for working hours.
- The exclusion constraint on `user_working_hours` prevents overlapping time ranges for a given user.
- Audit logging is implemented in application service code as per planning session decisions.
- Design choices are aligned with PostgreSQL optimization best practices and the Rails tech stack (including Hotwire Turbo Streams for real-time updates).