# The Pony Express Archive

A digital archive of North Mesquite High School's student newspaper from the 1974–1975 school year.

**Live Site:** https://nateeaton.github.io/PonyExpress/

---

## Origin

I'm Nathan Eaton, class of '75, and I served as school photographer during my senior year at North Mesquite High School. I kept all the issues of *The Pony Express* that I worked on, and they spent decades stored away in my attic. After attending our 50 year class reunion in 2024, I decided it was time to share these with my classmates.

## Purpose

The goal of this archive is to provide a **free, easily accessible** place for classmates to access a piece of their high school experience. This stands in contrast to how high school yearbooks and newspapers are typically made available: behind paywalls; these are your memories and you shouldn't have to pay to revisit them.

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
- 
### File Naming Convention

Files are named using the publication date in `YYYY-MM-DD.pdf` format:
- Example: `1974-09-11.pdf` (September 11, 1974)

Cover images follow the same convention: `YYYY-MM-DD.png`

### Repository Structure

```
PonyExpress/
├── index.html
├── style.css
├── favicon.png
├── PonyExpressTitle.png
├── issues/
│   ├── YYYY-MM-DD.pdf
│   └── covers/
│       └── YYYY-MM-DD.png
└── README.md
```

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
5. Commit and push changes to GitHub
6. Site updates automatically via GitHub Pages

**Basic Troubleshooting:**

- If the site isn't updating: Check GitHub Pages settings in repository settings
- If PDFs won't load: Verify file paths match exactly (case-sensitive)
- If carousel isn't working: Check browser console for JavaScript errors

### Interested in Collaborating?

This archive is intendeed to be a community effort. Classmates who want to help maintain and expand it are welcome to participate.

**We're looking for collaborators who can:**
- Add new issues to the archive as they become available
- Help with basic site updates and maintenance
- Ensure the archive remains accessible for future generations

**What's involved:**
- Basic familiarity with GitHub (or willingness to learn)
- Ability to follow the scanning specifications
- Commitment to preserving the archive's quality and accessibility

**Time commitment:**
- Minimal ongoing maintenance (a few hours per year)
- More time initially if adding multiple issues
- Responds to occasional questions from classmates

**How to get involved:**

Email **ponyexpressarchive@duck.com** with:
- Your name and graduating class
- Your technical comfort level
- How you'd like to contribute (scanning, technical updates, both)
- Any relevant experience (photography, archiving, web development, etc.)

We'll set you up as a repository collaborator and provide documentation on how to make updates. The goal is to ensure this archive can be maintained by multiple people and outlast any single contributor.

---

## Future Enhancement Ideas

**Multi-Year Support:**
- Create separate pages for each school year
- Expand beyond 1974–75 if issues from other years become available

**Search Functionality:**
- Full-text search across all archived PDFs
- Find specific names, events, or topics across the entire collection

**Community Features:**
- Linked social media group (Facebook?) for newspaper and yearbook staff
- Platform for sharing memories and connecting with former staff members

**Alternative Hosting:**
- Explore hosting options that can handle larger archives (multiple years)
- Identify perpetual hosting solutions that could outlast the original contributors
- Ensure long-term accessibility if the archive expands to include later graduating classes

---

## License

Content © North Mesquite High School Class of 1975. Scans and archive by alumni volunteers.

This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/).

---

## Contact

Questions or want to contribute? Email: **ponyexpressarchive@duck.com**
