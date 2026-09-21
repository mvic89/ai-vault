## OSM Data Update Agent

I built an AI agent in order to automate and update the OSM data for my 'Motorcycle Booking Engine' project. In order to do so, I used n8n.

Overview:
-  n8n cloud (Schedule) - Triggers the data update
-  my Next.js App (Vercel) - Recieves POST request with API and runs OSM extraction script
-  Supabase DB - New repair shops added (duplicates are skipped automatically)

The solution to stay within Vercels free tier limits was to set up 4 separate n8n workflows to process all EU countries in batches.

Instead of one workflow processing all 27 countries (which times out), I created **4 workflows** that each processed a region:

Week 1 (1st Monday): Nordic & Baltic Countries
Week 2 (2nd Monday): Central Europe
Week 3 (3rd Monday): Western Europe
Week 4 (4th Monday): Eastern & Southern Europe

Workflow 1: Nordic & Baltic Countries:
-  Sweden (SE)
-  Denmark (DK)
-  Finland (FI)
-  Norway (NO)
-  Estonia (EE)
-  Latvia (LV)
-  Lithuania (LT)

Workflow 2: Central Europe
-  Germany (DE)
-  Austria (AT)
-  Netherlands (NL)
-  Belgium (BE)
-  Luxembourg (LU)
-  Czech Republic (CZ)
-  Poland (PL)

Workflow 3: Western Europe
-  France (FR)
-  Spain (ES)
-  Portugal (PT)
-  Italy (IT)
-  Ireland (IE)
-  Switzerland (CH)

Workflow 4: Eastern & Southern Europe
-  Greece (GR)
-  Romania (RO)
-  Bulgaria (BG)
-  Hungary (HU)
-  Croatia (HR)
-  Slovenia (SI)
-  Slovakia (SK)
-  Cyprus (CY)
-  Malta (MT)

Updated automatic email posts with all the updated regions and countries list.

--------------
Summary:

1. So my n8n workflow consist of a 'Schedule Trigger' that triggers:
	| Nordic & Baltic | 1st Monday, 2 AM | SE, DK, FI, EE, LV, LT |
	| Central Europe | 2nd Monday, 2 AM | DE, AT, NL, BE, LU, CZ, PL |
	| Western Europe | 3rd Monday, 2 AM | FR, ES, PT, IT, IE |
	| Eastern & Southern | 4th Monday, 2 AM | GR, RO, BG, HU, HR, SI, SK, CY, MT |

2. An updated HTTP Request Body with a JSON object, containing the 'countries'.
	example.   {
	     "countries": ["GR", "RO", "BG", "HU", "HR", "SI", "SK", "CY", "MT"]
	   }

3. Email that posts automatically updated data each Monday.

------------
Screenshots:

![[Pasted image 20251124230545.png]]

![[Pasted image 20251124230616.png]]

![[Pasted image 20251124230704.png]]