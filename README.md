# Mask Response Quiz

A psychological quiz application that helps users identify their relationship patterns and "masks" - the behavioral patterns people unconsciously adopt in relationships.

## Overview

The Mask Response Quiz is an interactive web-based assessment that identifies four primary relationship masks:

- **The Performer** (Emotional Shapeshifter) - Adapts to keep connections stable, managing the room and repairing relationships quickly
- **The Analyzer** (Pattern Scanner) - Processes relationships through understanding and logic, searching for clarity when things are unclear
- **The Fixer** (Rescuer Engine) - Shows love through effort and support, often taking on others' emotional weight
- **The Vanisher** (Disappear to Regulate) - Manages intensity by creating distance, returning when feeling stable

## Features

- **24 Statement Quiz** - Quick assessment with 6 statements per type
- **Pattern Tracking** - Collects data on relationship status, conflict patterns, and attachment styles
- **Immediate Results** - Shows primary and secondary mask types instantly
- **Source Tracking** - Supports URL parameters (e.g., `?source=fb_reel_1`) to track which content attracts which personality types
- **Data Collection** - Submits anonymized results to Google Apps Script for pattern analysis
- **Responsive Design** - Clean, dark-themed interface built with Tailwind CSS

## Usage

### Running Locally

Simply open `index.html` in any modern web browser. No server or build process required.

```bash
# Option 1: Direct file open
open index.html

# Option 2: Use a simple HTTP server
python -m http.server 8000
# Then navigate to http://localhost:8000
```

### Deploying

This is a static HTML application that can be deployed to:
- GitHub Pages
- Netlify
- Vercel
- Any static hosting service

For GitHub Pages:
1. Push the repository to GitHub
2. Go to Settings → Pages
3. Select the branch to deploy from
4. The site will be available at `https://<username>.github.io/<repository-name>`

### Source Tracking

Add a `source` parameter to the URL to track which marketing content or posts attract specific personality types:

```
https://your-domain.com/?source=fb_reel_1
https://your-domain.com/?source=instagram_story_2
https://your-domain.com/?source=tiktok_post_3
```

## How It Works

1. **Quick Tracking Section** - Collects demographic and behavioral data (relationship status, conflict patterns, attachment style)
2. **Quiz Questions** - 24 statements rated on a 1-5 scale (1 = not me, 5 = that is me)
3. **Scoring Algorithm** - Aggregates responses per type, identifies primary and secondary masks
4. **Blend Detection** - Identifies when top two scores are within 3 points (indicating a blended type)
5. **Result Display** - Shows scores, primary type description, and secondary mask information
6. **Data Submission** - Sends anonymized results to webhook for pattern analysis

## Configuration

### Webhook URL

The quiz submits data to a Google Apps Script webhook. To use your own:

1. Create a Google Apps Script with a `doPost()` function
2. Deploy as a web app
3. Update the `WEBHOOK_URL` constant in `index.html` (line 151)

```javascript
const WEBHOOK_URL = "your-webhook-url-here";
```

## Data Structure

Submitted payload includes:
- `submission_id` - Unique identifier for each submission
- `timestamp_iso` - ISO timestamp
- `source` - URL parameter for tracking
- `scores` - Object with scores for each type
- `primary_type` - Highest scoring mask
- `secondary_type` - Second highest scoring mask
- `blend_flag` - "yes" if scores are close, "no" otherwise
- `tracking` - Demographic and behavioral responses
- `version` - Quiz version identifier

## Customization

### Adding Questions

Edit the `QUESTIONS` array in the JavaScript section (starting at line 160):

```javascript
{ type: "performer", text: "Your question text here." }
```

### Modifying Types

Update the `TYPES` array (line 153) and corresponding result copy in `resultCopy()` function (line 275).

### Styling

The quiz uses Tailwind CSS via CDN. Custom styles are defined in the `<style>` tag (lines 8-12).

## Browser Support

Works in all modern browsers:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+

## Privacy

- No personal identifying information is collected
- Submissions include only quiz responses and optional demographic data
- Submission ID is randomly generated
- Source tracking is based on URL parameters only

## License

MIT License - See LICENSE file for details

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Questions or Issues?

Open an issue on GitHub or contact the repository maintainer.
