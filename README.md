# QueueMe

![QueueMe logo](./QueueMe.png)

QueueMe is a mobile-first queue management app built with Expo and Supabase. Businesses can create and manage live queues, while customers can discover active queues, join them, and track their place in line in real time.

## Project Background

QueueMe started as a hackathon project at JAMHacks 9. The original idea was simple: digitize physical lines so people do not have to stand around waiting in person for clinics, restaurants, campus help desks, and similar walk-in services.

The first hackathon version focused on quick queue creation, code-based joining, and live queue tracking. Since then, the project in this repository has evolved beyond that prototype and now includes authenticated customer/business roles, profile management, Supabase-backed persistence, and realtime syncing across devices.

## What It Does

- Supports email/password sign-in with separate customer and business roles
- Lets businesses create queues with a generated queue code, description, estimated service time, and optional real address
- Lets customers search active queues by business name or location, or join directly with a queue code
- Syncs queue membership and queue state in real time through Supabase Realtime
- Shows live queue position and estimated wait time for customers
- Includes profile editing with role switching, display name updates, and optional profile photo selection

## Stack

- Expo 54
- React Native 0.81
- React 19
- Expo Router
- Supabase Auth + Postgres + Realtime
- TypeScript
- OpenStreetMap Nominatim for address suggestions

## Hackathon Context

The original JAMHacks version of QueueMe was pitched as a way to give people their time back by replacing physical waiting with a simple digital queue experience:

- Providers could create a queue and share a code on the spot
- Clients could join quickly with basic information
- Users could track their live position and estimated wait time
- The interface was designed to stay simple for both businesses and consumers

The early prototype used a different stack than the current repository:

- Frontend: React Native + TypeScript
- Backend: Python Flask
- Data layer: hosted JSON object
- Supporting tools: Git and Figma

This repo now reflects the newer implementation built on Expo Router and Supabase.

## Project Structure

```text
app/                    Expo Router screens
app/(tabs)/             Main tab flows for create, join, manage, profile, and status
context/                Auth and queue state providers
components/             Reusable UI bits like the profile menu
utils/                  Supabase client, queue helpers, profile helpers, location search
supabase/schema.sql     Database schema and policies
SUPABASE_SETUP.md       Short Supabase setup reference
```

## Main Flows

### Business flow

1. Sign up or switch profile role to `business`
2. Create a queue with a name, service time, and optional real address
3. Share the generated queue code with customers
4. Manage the line from the Manage tab
5. Call the next person, remove people manually, or end the queue

### Customer flow

1. Sign up or switch profile role to `customer`
2. Search for active queues by company name or location, or enter a queue code
3. Join with a display name and optional contact info
4. Track your live position, estimated wait time, and queue details
5. Leave the queue if needed

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment variables

Copy `.env.example` to `.env` and set:

```bash
EXPO_PUBLIC_SUPABASE_URL=your_supabase_project_url
EXPO_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### 3. Set up Supabase

1. Create a Supabase project.
2. Run the SQL in [`supabase/schema.sql`](/Users/matthewkim/Documents/GitHub/QueueMe/supabase/schema.sql).
3. In Supabase Auth, keep Email enabled.
4. In Realtime publications, enable:
   - `public.queues`
   - `public.queue_members`

More detail is in [`SUPABASE_SETUP.md`](/Users/matthewkim/Documents/GitHub/QueueMe/SUPABASE_SETUP.md).

### 4. Start the app

```bash
npm run dev
```

Then open the Expo app on iOS, Android, or web.

## Available Scripts

- `npm run dev` starts the Expo development server
- `npm run build:web` exports the web build
- `npm run lint` runs Expo linting

## Notes

- The app requires valid Supabase environment variables at startup.
- Location lookup uses OpenStreetMap Nominatim and requires network access from the client.
- Queue updates are driven by Supabase Realtime, so queue state stays in sync across signed-in devices.

## Future Improvements

- Push notifications when a customer is close to the front of the line
- Stronger business discovery and filtering
- Clipboard/share integration for queue codes
- Media upload storage for profile photos instead of inline image data

## Target Use Cases

QueueMe is designed for walk-in services where physical lines are common and waiting is inefficient:

- Clinics
- Campus service desks
- Salons
- Restaurants
- Government services

## Team

Built at JAMHacks 9 by:

- Sunny Wu - Frontend, product vision, pitch
- Vrinda Joshi - Full stack, pitch
- Jusraj Toor - Full stack, UI/UX
- Matthew Kim - Backend

## Acknowledgements

Special thanks to the JAMHacks 9 organizers at the University of Waterloo Engineering 7 building for creating the space to build, learn, and ship the original version of QueueMe.
