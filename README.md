# QueueMe

![QueueMe logo](./QueueMe.png)

> If time is money, QueueMe puts hours back in people's wallets.

QueueMe is a mobile-first queue management app that digitizes physical lines for businesses and customers. Instead of waiting around in person, users can join a queue, track their place live, and show up when it is actually their turn.

## 📌 Overview

QueueMe started at **JAMHacks 9** as a hackathon project focused on one practical problem: people waste too much time standing in line.

The original prototype made it easy to create a queue, share a code, and let customers monitor their position remotely. This repository reflects the newer version of that idea, with:

- 🔐 authenticated customer and business accounts
- 📲 realtime queue syncing across devices
- 🧑 profile management with role switching
- 📍 searchable queue discovery by business name or location
- ☁️ Supabase-backed persistence instead of a lightweight prototype backend

## 🚀 Features

- 🔑 **Role-based auth** for customers and businesses with email/password sign-in
- 🏪 **Queue creation** with generated queue codes, service-time estimates, descriptions, and optional real addresses
- 🙋 **Fast join flow** through queue code entry or queue discovery search
- 📍 **Live queue search** by business name or location
- ⏱️ **Realtime position tracking** with estimated wait times
- 🔄 **Realtime sync** through Supabase Realtime
- 👤 **Profile editing** with name, avatar, and role management
- 🧑‍💼 **Business controls** to call the next person, remove someone, or end the queue

## 🛠 Tech Stack

### Current repo

- **Frontend:** Expo 54, React Native 0.81, React 19, Expo Router
- **Backend/Data:** Supabase Auth, Postgres, Realtime
- **Language:** TypeScript
- **Location search:** OpenStreetMap Nominatim

### Original hackathon prototype

- **Frontend:** React Native, TypeScript
- **Backend:** Python Flask
- **Database:** Hosted JSON object
- **Tools:** Git, Figma

## 🏁 Hackathon Context

QueueMe was built at **JAMHacks 9** and designed for walk-in services where physical lines slow everyone down.

### 🎯 Target use cases

- Clinics
- Campus service desks
- Salons
- Restaurants
- Government services

### 💡 Original pitch

- Providers could create a queue and share a simple code on the spot
- Clients could join in seconds with basic info
- Users could view their live position and estimated wait time
- The experience stayed simple for both businesses and consumers

## 🧭 Main User Flows

### 🏪 Business flow

1. Sign up or switch profile role to `business`
2. Create a queue with a name, wait-time estimate, and optional real address
3. Share the generated queue code with customers
4. Manage the queue from the app
5. Call the next person, remove someone, or end the queue

### 🙋 Customer flow

1. Sign up or switch profile role to `customer`
2. Search active queues by business name or location, or enter a queue code
3. Join with a display name and optional contact info
4. Track your live position and estimated wait time
5. Leave the queue if needed

## 📁 Project Structure

```text
app/                    Expo Router screens
app/(tabs)/             Main tab flows for create, join, manage, profile, and status
context/                Auth and queue state providers
components/             Reusable UI pieces
utils/                  Supabase client, queue helpers, profile helpers, location search
supabase/schema.sql     Database schema and policies
SUPABASE_SETUP.md       Supabase setup reference
```

## ⚡ Getting Started

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

1. Create a Supabase project
2. Run [`supabase/schema.sql`](/Users/matthewkim/Documents/GitHub/QueueMe/supabase/schema.sql)
3. In Supabase Auth, keep Email enabled
4. In Realtime publications, enable:
   - `public.queues`
   - `public.queue_members`

More setup detail is in [`SUPABASE_SETUP.md`](/Users/matthewkim/Documents/GitHub/QueueMe/SUPABASE_SETUP.md).

### 4. Run the app

```bash
npm run dev
```

Then open it in Expo on iOS, Android, or web.

## 📜 Available Scripts

- `npm run dev` starts the Expo development server
- `npm run build:web` exports the web build
- `npm run lint` runs Expo linting

## 📝 Notes

- The app requires valid Supabase environment variables at startup
- Location lookup uses OpenStreetMap Nominatim and needs client-side network access
- Queue state stays in sync across devices through Supabase Realtime

## 📈 Future Plans

- 🔔 Push notifications when a customer is close to the front
- 🔎 Stronger business discovery and filtering
- 📋 Better clipboard/share support for queue codes
- 🖼️ Proper media storage for profile photos instead of inline image data
- 📊 Wait-time analytics and smarter queue insights

## 👩‍💻 Meet the Team

Built at JAMHacks 9 by:

- **Sunny Wu** - Frontend, product vision, pitch
- **Vrinda Joshi** - Full stack, pitch
- **Jusraj Toor** - Full stack, UI/UX
- **Matthew Kim** - Backend

## 💬 Acknowledgements

Special thanks to the **JAMHacks 9** organizers at the **University of Waterloo Engineering 7** building for creating the space to build, learn, and ship the original version of QueueMe.
