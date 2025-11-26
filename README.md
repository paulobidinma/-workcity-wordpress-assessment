# -workcity-wordpress-assessment
WordPress Developer (SEO + Knowledge Panel  Specialist) - Assessment Test


==================================================

## Setup instructions

Install Local WP or any local server of your choice
Create a fresh WordPress site
Copy the child theme folder into wp content themes
Activate the child theme
Install Elementor and LiteSpeed Cache
Import any Elementor templates if needed
Open the Landing Page and check that all sections load well
Check mobile view inside Elementor
Turn on caching and file minify inside LiteSpeed Cache
Add your analytics code with Google Site Kit or Tag Manager

## Tools and technologies used

- WordPress
- Elementor
- LiteSpeed Cache
- Google Site Kit
- Custom child theme for clean edits
- JSON LD for schema
- Git and GitHub for version control

## Challenges encountered and how they were resolved

First challenge was keeping the layout clean on phone view.
This was solved by adjusting padding and text size for tablet and phone inside Elementor.

Another challenge was keeping images small.
This was solved by compressing all images before upload and by using LiteSpeed image tools.

There was also a need to avoid layout shifts during load.
This was solved by setting fixed image sizes in the builder and by reducing extra scripts.

Making sure schema passed validation was also important.
This was fixed by testing each JSON file in the Rich Results Test and correcting small errors.

## Knowledge Graph and SEO explanations

The JSON LD files in the schema folder help Google understand three key things:
- Workcity Africa as an entity
- Sam Ojei as a clear person linked to the brand
- The main site and its logo with social links

These signals help Google confirm identity.
Clean schema, a clear About page, correct social links and steady brand info across the web all help build trust in search results.

For SEO, the landing page is kept light, mobile friendly and cached.
Images are compressed.
CSS and JS are minified.
Analytics is added to help track visits.

All of this keeps the page fast and supports good search visibility.

====================================================