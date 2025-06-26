# .ai/db-plan.md

# Database Schema

## 1. Tables

### 1.1 users
- id UUID PRIMARY KEY DEFAULT gen_random_uuid()
- email VARCHAR(255) NOT NULL UNIQUE
- encrypted_password VARCHAR(255) NOT NULL
- name VARCHAR(255)
- phone_number VARCHAR(50)
- linkedin_profile VARCHAR(255)
- created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.2 invitations
- id UUID PRIMARY KEY DEFAULT gen_random_uuid()
- organizer_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE
- title VARCHAR(255) NOT NULL
- description TEXT
- duration_minutes INTEGER NOT NULL CHECK (duration_minutes > 0)
- secure_token VARCHAR(64) NOT NULL UNIQUE
- created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.3 invitation_participants
- id UUID PRIMARY KEY DEFAULT gen_random_uuid()
- invitation_id UUID NOT NULL REFERENCES invitations(id) ON DELETE CASCADE
- email VARCHAR(255) NOT NULL
- name VARCHAR(255)
- created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- UNIQUE(invitation_id, email)

### 1.4 time_slots
- id UUID PRIMARY KEY DEFAULT gen_random_uuid()
- invitation_participant_id UUID NOT NULL REFERENCES invitation_participants(id) ON DELETE CASCADE
- start_time TIMESTAMP WITH TIME ZONE NOT NULL
- end_time TIMESTAMP WITH TIME ZONE NOT NULL
- is_suggested BOOLEAN NOT NULL DEFAULT FALSE
- created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- CHECK (end_time > start_time)

### 1.5 deliveries
- id UUID PRIMARY KEY DEFAULT gen_random_uuid()
- invitation_participant_id UUID NOT NULL REFERENCES invitation_participants(id) ON DELETE CASCADE
- channel VARCHAR(20) NOT NULL CHECK (channel IN ('email','sms','linkedin'))
- status VARCHAR(20) NOT NULL CHECK (status IN ('pending','sent','failed'))
- sent_at TIMESTAMP WITH TIME ZONE
- response JSONB
- created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.6 confirmations
- id UUID PRIMARY KEY DEFAULT gen_random_uuid()
- invitation_participant_id UUID NOT NULL UNIQUE REFERENCES invitation_participants(id) ON DELETE CASCADE
- confirmed_at TIMESTAMP WITH TIME ZONE NOT NULL
- created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()
- updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now()

### 1.7 user_day_enum
```sql
CREATE TYPE user_day_enum AS ENUM (
  'monday','tuesday','wednesday','thursday','friday','saturday','sunday'
);