## Motorcycle Repair Shop Directory

My motorcycle repair shop database structure is based on extracted OSM data. I use an extraction script that fetches motorcycle repair shop data from OpenStreetMap's Overpass API for all EU countries. It focuses on:

-  **Verified businesses**: Only shops with proper business information (name, location, address)
-  **Quality data**: Filters for shops that appear in both OSM and Google Maps
-  **Brand categorization**: Automatically detects and categorizes dealer-affiliated shops
-  **Duplicate prevention**: Uses OSM IDs to avoid importing the same shop twice

My script only imports shops that meets these criteria:

**Must Have**:
- Business name
- GPS coordinates
- Valid address or city

**Preferred** (improves quality):
- Phone number or email
- Website
- Proper street address

**Excluded**:
- Shops without names
- Shops without location data
- Duplicate entries (same OSM ID)

// Since OSM data is free and based on individual contribution, it still doesn't cover up for the quality data paid providers like Google places API provides.

-------
I also created some 'Login / Signup' functionality with a 'Register' page where you can register your motorcycle. the data ends up in a Supabase DB table.

Link to the Website:
https://motorcycle-booking-engine-qn4i.vercel.app/

Screenshots of the Website:

![[Pasted image 20251125145626.png]]

![[Pasted image 20251125145536.png]]

![[Pasted image 20251125145714.png]]

![[Pasted image 20251125145740.png]]

![[Pasted image 20251125145909.png]]

Screenshots of the Database:

![[Pasted image 20251125150108.png]]

![[Pasted image 20251125150140.png]]

![[Pasted image 20251125150212.png]]