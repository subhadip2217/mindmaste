# Mind Master — real 1v1 multiplayer setup

The repo now contains a real Supabase/Realtimes-based Math Rush client. It is intentionally not a fake opponent.

## 1. Create a Supabase project
Create a project at https://supabase.com/.

## 2. Create the database
Open **SQL Editor** and run all of `supabase-schema.sql` from this repository.

This creates `mm_rooms` and `mm_events` and enables Realtime.

## 3. Add the public client configuration
Open `multiplayer.html` and replace:

`YOUR_SUPABASE_PROJECT_URL`

and

`YOUR_SUPABASE_ANON_KEY`

with the project's **Project URL** and **anon/public key** from Supabase API settings.

Only use the anon/public key in browser code. **Never put a Supabase service-role key in this HTML file.**

## 4. Play
Open `multiplayer.html` from your deployed site. Player 1 creates a room and shares the 5-character code. Player 2 joins it. Both press READY.

The game uses Supabase realtime events for room state and match events. Questions are generated from the same round sequence, and meaningful state is synchronized rather than streaming animation frames.

## Security note
The supplied SQL is suitable for a personal prototype. Before making the game a public competitive service, add authenticated users and server/Edge-Function validation for match results, question seeds, timing and anti-cheat rules. Do not trust client-reported scores.

## Deployment note
GitHub Pages can serve the HTML, and Vercel can also host the repository. If you use a framework later, move the Supabase values into environment variables rather than hardcoding them. The anon key is designed to be public when Row Level Security is configured correctly; the service-role key is secret.
