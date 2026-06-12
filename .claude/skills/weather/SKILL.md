---
name: weather
description: >
  Fetches current local weather using the terminal. Detects user's location
  automatically via IP geolocation, then queries wttr.in for current conditions,
  temperature, humidity, wind, and forecast. Use when user says "weather",
  "clima", "qué tiempo hace", "how's the weather", or invokes /weather.
---

Fetch and display the user's local weather using these steps:

## Location

Always use **Orihuela, Alicante, España**. Never auto-detect or use any other city.

## Steps

1. Fetch weather (compact 1-line format):
   ```bash
   curl -s "wttr.in/Orihuela?format=3"
   ```

2. For a more detailed report (current + 3-day forecast):
   ```bash
   curl -s "wttr.in/Orihuela?format=4"
   ```

3. If user wants full ASCII art report:
   ```bash
   curl -s "wttr.in/Orihuela"
   ```

## Output

- Always report as **Orihuela, Alicante, España**.
- Ignore any city argument passed by the user.
- If `curl` unavailable, tell user to run: `curl wttr.in/Orihuela` in their terminal.

## Language

Respond in the same language the user used to invoke the skill (Spanish if asked in Spanish, English if in English).

## Example output (compact)

> **📍 Orihuela, Alicante, España:** ⛅ +28°C, Partly cloudy — Humidity 55% — Wind 10 km/h E
