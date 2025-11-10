# The Pony Express Archive

A digital archive of North Mesquite High School's student newspaper from the 1974–1975 school year.

**Live Site:** https://nateeaton.github.io/PonyExpress/

---

## Origin

I'm Nathan Eaton, class of '75, and I served as school photographer during my senior year at North Mesquite High School. I kept all the issues of *The Pony Express* that I worked on, and they spent decades stored away in my attic. After attending our 50 year class reunion, I decided it was time to share these with my classmates.

## Purpose

The goal of this archive is to provide a **free, easily accessible** place for classmates to access a piece of their high school experience. This stands in contrast to how high school yearbooks and newspapers are typically made available: behind paywalls; these are your memories and you shouldn't have to pay to revisit them.

---

## Features

### Responsive Design
The archive automatically adapts to provide an optimal experience on both desktop and mobile devices:
- **Desktop (≥768px):** Full-featured experience with in-page PDF viewer, searchable catalog, and carousel navigation arrows
- **Mobile (<768px):** Streamlined interface with swipe-enabled carousel, native PDF viewing in dedicated browser tab, and device-appropriate instructions

### Interactive Carousel
Browse all available issues using the visual carousel. On desktop, use left/right navigation arrows. On mobile, swipe to browse. Click/tap any cover to open the full PDF.

### Searchable Catalog (Desktop)
A comprehensive, searchable index of all articles and photos across all issues. Search by:
- Names (students, faculty, public figures)
- Article titles
- Authors
- Topics and keywords
- Organizations and clubs
- Musical artists mentioned

The catalog uses DataTables for powerful filtering and sorting. Click any article title to jump directly to that page in the PDF viewer.

**Note:** The catalog is optimized for desktop viewing and hidden on mobile devices. Mobile users can browse the carousel and use their browser's native PDF search within individual issues.

### PDF Viewer
**Desktop:** Built-in iframe viewer with:
- Page-specific deep linking (jump to specific pages from catalog)
- Share functionality (copy direct links to specific issues)
- Open in new tab option
- Embedded OCR text for in-PDF searching (Ctrl+F / Cmd+F)

**Mobile:** Optimized for native browser PDF viewing:
- PDFs open directly in a dedicated browser tab named 'ponyExpressPDF'
- Multiple selections reuse the same tab to prevent clutter
- Access to native mobile share/save features
- Better performance and compatibility on mobile browsers

### Analytics
Privacy-respecting analytics via GoatCounter to track usage without invasive tracking.

---

## Technical Details

### Scanning Process

If you have additional issues to contribute, here's the process and specifications used for this archive:

**Tools:**
- A modern scanner (I used a Canon TR8500 series multifunction printer/scanner)
- Scanning software capable of multi-page PDFs (I used [VueScan](https://www.hamrick.com/))
- Software with OCR capability to embed searchable text in the PDF

**Scan Settings:**
- **Size:** 8.5" × 11"
- **Resolution:** 150 DPI
- **Color Mode:** Grayscale
- **Format:** PDF with embedded OCR text
- **Cover Format:** PNG image

**Note on Quality:**
The scan quality is inherently limited by the physical condition of the original newspapers. OCR accuracy may vary, so catalog searches may not always capture every instance of a name or term that appears in the scanned images.

### File Naming Convention

Files are named using the publication date in `YYYY-MM-DD.pdf` format:
- Example: `1974-09-11.pdf` (September 11, 1974)

Cover images follow the same convention: `YYYY-MM-DD.png`

### Repository Structure

```
PonyExpress/
├── index.html              # Main site page
├── style.css               # Site styling with responsive breakpoints
├── index.json              # Catalog metadata for all articles/photos
├── catalog_chat_prompt.md  # AI assistant prompt for cataloging
├── favicon.png             # Site favicon
├── PonyExpressTitle.png    # Header logo
├── catalog/                # (Optional) Individual catalog files per issue
│   └── YYYY-MM-DD.json     # Catalog entries for specific issue
├── issues/
│   ├── YYYY-MM-DD.pdf      # Newspaper PDFs
│   └── covers/
│       └── YYYY-MM-DD.png  # Cover thumbnails
└── README.md               # This file
```

### Responsive Design Implementation

The site uses CSS media queries with a 768px breakpoint to provide device-optimized experiences:

**CSS Classes:**
- `.desktop-only` - Content visible only on screens ≥768px
- `.mobile-only` - Content visible only on screens <768px

**Device-Specific Features:**
- **Desktop:** Carousel navigation arrows, searchable catalog, iframe PDF viewer, share buttons
- **Mobile:** Swipe carousel, hidden catalog with explanatory note, direct PDF tab opening, simplified instructions

**JavaScript Adaptation:**
The carousel PDF link handler detects screen width and routes to appropriate viewing method:
- Desktop: Loads PDF in iframe viewer
- Mobile: Opens PDF in dedicated reusable tab ('ponyExpressPDF')

This ensures optimal performance and user experience on all devices.

### Catalog Data Structure

The `index.json` file contains structured metadata for every article and photo:

```json
{
  "data": [
    {
      "IssueDate": "1974-09-11",
      "IssueFile": "1974-09-11.pdf",
      "Type": "Article",
      "Section": "Editorial",
      "Title": "Introduction to Volume V1, Number 1",
      "Page": 2,
      "Author": "Alice Adams",
      "Names": ["Alice Adams"],
      "Topics": ["editorial", "newspaper"],
      "Organizations": ["Pony Express"],
      "Artists": [],
      "PublicFigures": [],
      "Events": []
    }
  ]
}
```

This structured data enables powerful search across all content without requiring full-text indexing of PDFs.

---

## How to Contribute

If you have additional issues of *The Pony Express* that you'd like to contribute:

1. Review the scanning specifications above
2. Scan your issues following those guidelines
3. Email us at **ponyexpressarchive@duck.com** with:
   - Which year(s) you have
   - Condition of the issues
   - Confirmation that you've prepared scanned files per the specifications

*Note: We welcome contributions of scanned issues but are unable to scan issues for others.*

---

## Site Maintenance

### For Current Maintainers

**Adding New Issues:**

1. Scan and prepare the PDF following the specifications above
2. Create a cover image (PNG, ~200px width recommended)
3. Add files to the repository:
   - PDF: `/issues/YYYY-MM-DD.pdf`
   - Cover: `/issues/covers/YYYY-MM-DD.png`
4. Update `index.html` by adding a new carousel item:
   ```html
   <div class="carousel-item">
     <a href="#" data-pdf="issues/YYYY-MM-DD.pdf" data-date="Month DD, YYYY" class="pdf-link">
       <img src="issues/covers/YYYY-MM-DD.png" alt="Month DD, YYYY Issue" />
     </a>
     <p class="issue-date">Month DD, YYYY</p>
   </div>
   ```
5. Create catalog entries (manually or using AI - see "Updating the Catalog" below)
6. Update `index.json` with the new entries
7. Commit and push changes to GitHub
8. Site updates automatically via GitHub Pages

**Updating the Catalog:**

When adding a new issue, you'll need to extract metadata for each article and photo. You can do this manually or use AI assistance:

**Manual Entry:**
For each article/photo, record:
- Issue date and filename
- Article/photo type (Article, Photo, etc.)
- Section (Editorial, News, Sports, etc.)
- Title and page number
- Author (if bylined)
- Names mentioned (students, faculty, etc.)
- Topics/keywords
- Organizations/clubs mentioned
- Artists/public figures mentioned
- Events mentioned

Add each entry to the `data` array in `index.json` following the existing format.

**AI-Assisted Entry (Alternative):**
To streamline the process, use the AI chat prompt in `catalog_chat_prompt.md`:
1. Upload the PDF to an AI assistant (like Claude)
2. Provide the prompt from `catalog_chat_prompt.md`
3. The AI will return structured JSON entries
4. Review and refine the output
5. Add to `index.json`

This significantly reduces cataloging time while maintaining consistency.

**Individual Catalog Files (Optional):**
You can also store catalog data for each issue separately in `/catalog/YYYY-MM-DD.json` files for easier maintenance and version control, then manually merge entries into `index.json` as needed.

**Basic Troubleshooting:**

- If the site isn't updating: Check GitHub Pages settings in repository settings
- If PDFs won't load: Verify file paths match exactly (case-sensitive)
- If carousel isn't working: Check browser console for JavaScript errors
- If catalog isn't loading: Verify `index.json` is valid JSON (use a JSON validator)
- If page anchors (#page=X) aren't working: This is a known iframe limitation; the code uses iframe replacement to maximize compatibility

### Technical Stack

- **Frontend:** Pure HTML5, CSS3, and vanilla JavaScript (no build process required)
- **PDF Display:** Browser-native iframe PDF rendering
- **Data Table:** [DataTables](https://datatables.net/) 2.0.7 with jQuery
- **Hosting:** GitHub Pages (static site hosting)
- **Analytics:** [GoatCounter](https://www.goatcounter.com/) (privacy-friendly)

### Interested in Collaborating?

This archive is intended to be a community effort. Classmates who want to help maintain and expand it are welcome to participate.

**We're looking for collaborators who can:**
- Add new issues to the archive as they become available
- Extract metadata for catalog entries (manually or using AI assistance)
- Help with basic site updates and maintenance
- Ensure the archive remains accessible for future generations

**What's involved:**
- Basic familiarity with GitHub (or willingness to learn)
- Ability to follow the scanning specifications
- Attention to detail for catalog data entry
- Commitment to preserving the archive's quality and accessibility

**Time commitment:**
- Minimal ongoing maintenance (a few hours per year)
- More time initially if adding multiple issues
- Responds to occasional questions from classmates

**How to get involved:**

Email **ponyexpressarchive@duck.com** with:
- Your name and graduating class
- Your technical comfort level
- How you'd like to contribute (scanning, technical updates, data entry, etc.)
- Any relevant experience (photography, archiving, web development, etc.)

We'll set you up as a repository collaborator and provide documentation on how to make updates. The goal is to ensure this archive can be maintained by multiple people and outlast any single contributor.

---

## Future Enhancement Ideas

**Multi-Year Support:**
- Create separate pages for each school year
- Expand beyond 1974–75 if issues from other years become available

**Enhanced Search:**
- Full-text search across PDF content (in addition to catalog metadata)
- Advanced filtering (date ranges, multiple keywords, etc.)
- Search result highlighting

**Community Features:**
- Linked social media group (Facebook?) for newspaper and yearbook staff
- Platform for sharing memories and connecting with former staff members
- Comment system for reminiscing about specific articles

**Accessibility Improvements:**
- Alternative text for all images in PDFs
- Enhanced mobile experience for catalog browsing
- Text-only versions of articles for screen readers

---

## Known Limitations

- **Mobile Catalog:** The searchable catalog is hidden on mobile devices (<768px) due to the complexity of the DataTable interface on small screens. Mobile users can browse the carousel and use in-PDF search within individual issues.
- **OCR Accuracy:** OCR quality depends on the physical condition of the source newspapers. Some text may not be searchable even though it's visible.
- **Page Anchor Support:** Deep linking to specific PDF pages (#page=X) works in most modern browsers but may not work in all iframe contexts on desktop. The code uses iframe replacement to maximize compatibility.
- **Search Limitations:** Catalog search only includes manually-entered metadata, not full PDF text content.
- **Browser Compatibility:** The site is optimized for modern browsers (Chrome, Firefox, Safari, Edge). Older browsers may have reduced functionality.

---

## License

Content © North Mesquite High School Class of 1975. Scans and archive by alumni volunteers.

This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/).

---

## Contact

Questions or want to contribute? Email: **ponyexpressarchive@duck.com**
